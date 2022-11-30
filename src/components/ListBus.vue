<template>
    <div>
        <div v-for="bus in buses">
            <div class="ticket result-tickets-items">
                <div class="row row-cols-1 row-cols-md-5 mb-3">
                    <div class="bus__column col">
                        <div class="d-inline-block">
                            <span class="fw-bold">{{HoursBus(bus.dtDep)}}</span>
                            <span>{{DateBus(bus.dtDep)}}</span>
                        </div>
                        <div class="d-inline-block">
                            <span>{{" " + bus.stDepName + " "}}</span>
                            <span>{{" " + bus.stDepAddr + " "}}</span>
                        </div>
                    </div>
                    <div class="bus__column col">
                        <div class="d-inline-block">
                            <span class="fw-bold">{{TimeWay(bus.dtDep, bus.dtArr)}}</span>
                        </div>
                        <div class="cd-inline-blockol">
                            <span class="fw-bold">прямий рейс</span>
                        </div>
                    </div>
                    <div class="bus__column col">
                        <div class="d-inline-block">
                            <span class="fw-bold">{{HoursBus(bus.dtArr)}}</span>
                            <span>{{DateBus(bus.dtArr)}}</span>
                        </div>
                        <div class="d-inline-block">
                            <span>{{" " + bus.stArrName + " "}}</span>
                            <span>{{" " + bus.stArrAddr + " "}}</span>
                        </div>
                    </div>
                    <div class="bus__column col">
                        <div class="d-inline-block">
                            <span>{{bus.places}}</span>
                        </div>
                    </div>
                    <div class="bus__column col">
                        <div class="d-inline-block">
                            <p>
                                <span>{{bus.price}}</span>
                            </p>
                        </div>
                    </div>
                </div>
                <div class="bus__bottom row row-cols-1 row-cols-md-3">
                    <div class="bus__column col-8 col-md-8">
                        <p class="carrier">
                            Перевізник:
                            <span>{{bus.carrier}}</span>
                        </p>
                    </div>
                    <div class="bus__column col-2 col-md-2">
                        <p class="fw-bold">
                            Детально
                        </p>
                    </div>
                    <div class="bus__column col-2 col-md-2">
                        <button type="button" class="btn btn-danger" @click="ViewTickets(bus)">Обрати</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default{
    props: ['buses'],
    methods:{
        HoursBus(value){
            var date = new Date(value);
            var options = {hour:'2-digit', minute:'2-digit' };
            let res = " "+ date.toLocaleString('uk-UA', options) +" "
            return res;
        },

        DateBus(value){
            var date = new Date(value);
            var options = {weekday: 'short', year: 'numeric', month: 'long', day: 'numeric', hour:'2-digit', minute:'2-digit' };
            let res = " "+ date.toLocaleString('uk-UA', options) +" "
            return res;
        },

        TimeWay(startD, endD){
            let timeW = (new Date(endD) - new Date(startD))/1000/60;
            return ((timeW/60 | 0) + "г " + (timeW % 60) + 'хв');
        },

        ViewTickets(object){
            this.$emit('viewTickets', object);
        }

    }
}
</script>

<style>
.result-tickets-items{
    margin-bottom: 1.5rem;
    box-shadow: 0 2px 3px rgba(10,10,10,.1),0 0 0 1px #cc004d!important;
    background-color: #fff;
    border-radius: 5px;
    color: #4a4a4a;
    display: block;
    padding: 1.25rem;
}

.carrier{
    font-size: 0.75rem;
    font-weight: 300;
}

.bus__bottom{
    margin-bottom: -0.75rem !important;
    align-items: baseline;
}

.bus__column{
    padding: 0.75rem !important;
    }
p {
    margin: 0 !important;
    padding: 0 !important;
}
</style>