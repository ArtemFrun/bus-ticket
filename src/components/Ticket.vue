<template>
    <div class="">
        <div class="ticket result-tickets-items">
                <div class="ticket-info row row-cols-1 row-cols-md-1" v-for="tiket in tickets">
                    <div class="bus__column col">
                        <div class="d-inline-block">
                            <div class="passenger-title">Пасажир 1</div>
                        </div>
                    </div>
                    <div class="ticket__row row row-cols-md-3 row-cols-3">
                        <div class="bus__column col">
                            <div class="input__block d-inline-block">
                                <label for="Username" class="mb-2">Імя</label>
                                <div class="input-group mb-3">
                                    <span class="input-group-text icon-input" id="basic-addon1">@</span>
                                    <input type="text" class="form-control input__text" placeholder="Імя" aria-label="Username" aria-describedby="basic-addon1">
                                </div>
                            </div>
                        </div>
                        <div class="bus__column col">
                            <div class="cd-inline-blockol">
                                <label for="Surname" class="mb-2">Прізвище</label>
                                <div class="input-group mb-3">
                                    <span class="input-group-text icon-input" id="basic-addon1">@</span>
                                    <input type="text" class="form-control input__text" placeholder="Прізвище" aria-label="Surname" aria-describedby="basic-addon1">
                                </div>
                            </div>
                        </div>
                        <div class="bus__column col">
                            <div class="cd-inline-blockol">
                                &nbsp;
                            </div>
                        </div>
                    </div>
                    <div class="bus__column col">
                        <div class="ticket__line" data-content="Квиток">
                        </div>
                    </div>
                    <div class="bus__column col">
                        <div class="d-none">
                            <span></span>
                        </div>
                    </div>
                    <div class="ticket__row row row-cols-md-2 row-cols-2">
                        <div class="bus__column col-sm-6 col-md-6">
                            <div class="ticket__row row row-cols-md-2 row-cols-2">
                                <div class="bus__column col">
                                    <div class="dropdown">
                                        <button class="btn btn__place" type="button" data-bs-toggle="dropdown" aria-expanded="false" v-bind:class="seatS !== '' ? cheangeSeat : ''">
                                            {{this.buttonText}}
                                        </button>
                                        <div class="dropdown-menu dropdowm__place">
                                            <div class="bus__places">
                                                <div class="first">
                                                    <svg version="1.1" viewBox="0 0 40 40" class="svg-icon" style="width: 40px; height: 40px;"><path fill="#ccc" stroke="none" d="m38 20c0-9.94-8.06-18-18-18s-18 8.06-18 18 8.06 18 18 18 18-8.06 18-18zm-4.5 0c0 5.86-3.77 10.81-9 12.67v-25.34c5.23 1.86 9 6.81 9 12.67zm-15.75 0c0-1.24 1.01-2.25 2.25-2.25s2.25 1.01 2.25 2.25-1.01 2.25-2.25 2.25-2.25-1.01-2.25-2.25zm2.25-13.5c0 6.15-5.92 11.13-13.27 11.23 1.09-6.36 6.6-11.23 13.27-11.23zm-13.27 15.77c7.35 0.1 13.27 5.08 13.27 11.23-6.67 0-12.18-4.87-13.27-11.23z" class="zu-wheel"></path></svg>
                                                </div>
                                                <div class="places__info" >
                                                    <div class="places__view" v-for="places in tiket.busTempl.matrix[0]">
                                                        <div class="col" v-for="place in places">
                                                            <div class="place__set" v-if="(typeof(place.n) !== 'undefined')" v-bind:class="[place.free == '1' ? freeClass : disableClass, (place.n == seatS) ? activeClass : '']" >
                                                                <div class="" v-if="place.free == '1'" @click="selectSeat(place.n)">
                                                                    <span ><svg data-v-cbdf82c4="" version="1.1" viewBox="0 0 40 40" class="svg-icon" style="width: 40px; height: 40px;"><path fill="#ccc" stroke="none" d="m9.41 2.44c-3.69 1.03-3.11 3.48-4.66 6.4-0.59 1.12-1.48 2.01-1.87 3.24-0.5 1.59-0.47 3.75-0.54 5.4-0.14 3.12-0.36 7.44 0.6 10.44 0.4 1.27 1.2 2.08 1.81 3.24 1.13 2.14 1.36 5.39 3.96 6.25 0.83 0.27 1.95 0.23 2.82 0.23h10.23c1.33 0 3.45 0.17 3.94-1.48 0.39-1.28-0.67-2.42-1.82-2.78h-8.82c-2.72-0.07-3.48-0.39-4.02-3.3-0.44-1.63 0.32-2.1 0-4.68-0.14-2.33-0.66-3.55-0.56-6.12l0.68-5.4-0.32-3.24c0.05-1.1 0.78-3.27 1.83-3.74 0.57-0.26 1.74-0.22 2.39-0.22h7.06c1.46-0.01 3.09-0.06 3.58-1.8 0.74-2.62-3.14-2.52-4.64-2.44h-11.65zm18.71 2.8c-1.25 3.72-3.52 3.24-6.71 3.24h-8.03v5.4s-0.42 6.48-0.42 6.48 0.57 6.48 0.57 6.48l-0.24 4.68h9.53c2.74 0 4.31 0.31 5.3 3.24 1.29 0 6 0.23 6.86-0.36 1.04-0.72 1.53-3.11 1.74-4.32 0.69-3.87 0.93-7.6 0.93-11.52-0.01-2.1-0.67-7.69-1.15-9.72-0.22-0.99-0.66-2.65-1.52-3.24-0.64-0.45-1.86-0.36-2.63-0.36h-4.23z" class="zu-seat"></path></svg></span>
                                                                    <span class="place__number">{{place.n}}</span>
                                                                </div>
                                                                <div class=""  v-else>
                                                                    <span><svg data-v-cbdf82c4="" version="1.1" viewBox="0 0 40 40" class="svg-icon" style="width: 40px; height: 40px;"><path fill="#c33" stroke="none" d="m9.41 2.44c-3.69 1.03-3.11 3.48-4.66 6.4-0.59 1.12-1.48 2.01-1.87 3.24-0.5 1.59-0.47 3.75-0.54 5.4-0.14 3.12-0.36 7.44 0.6 10.44 0.4 1.27 1.2 2.08 1.81 3.24 1.13 2.14 1.36 5.39 3.96 6.25 0.83 0.27 1.95 0.23 2.82 0.23h10.23c1.33 0 3.45 0.17 3.94-1.48 0.39-1.28-0.67-2.42-1.82-2.78h-8.82c-2.72-0.07-3.48-0.39-4.02-3.3-0.44-1.63 0.32-2.1 0-4.68-0.14-2.33-0.66-3.55-0.56-6.12l0.68-5.4-0.32-3.24c0.05-1.1 0.78-3.27 1.83-3.74 0.57-0.26 1.74-0.22 2.39-0.22h7.06c1.46-0.01 3.09-0.06 3.58-1.8 0.74-2.62-3.14-2.52-4.64-2.44h-11.65zm18.71 2.8c-1.25 3.72-3.52 3.24-6.71 3.24h-8.03v5.4s-0.42 6.48-0.42 6.48 0.57 6.48 0.57 6.48l-0.24 4.68h9.53c2.74 0 4.31 0.31 5.3 3.24 1.29 0 6 0.23 6.86-0.36 1.04-0.72 1.53-3.11 1.74-4.32 0.69-3.87 0.93-7.6 0.93-11.52-0.01-2.1-0.67-7.69-1.15-9.72-0.22-0.99-0.66-2.65-1.52-3.24-0.64-0.45-1.86-0.36-2.63-0.36h-4.23z" class="zu-seat"></path></svg></span>
                                                                    <span class="place__number">{{place.n}}</span>
                                                                </div>
                                                                
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                <div class="bus__column col">
                                    <div class="d-inline-block">
                                        <p class="bus__way">
                                            <span>{{" " + tiket.cityDepName + " - " + tiket.cityArrName + " "}}</span>
                                        </p>
                                        <p class="bus__carrier">
                                            <span>ДЕНИСІВКА ТДВ надає можливість вибрати місце в автобусі</span>
                                        </p>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="bus__column col-sm-1 col-md-1 d-flex__al-center">
                            <div class="d-inline-block price">
                                <p>
                                    <span>{{" " + tiket.pricePass + " " + tiket.priceCName + " "}}</span>
                                </p>
                            </div>
                        </div>
                        <div class="d-inline-block">
                            <p>
                                <span></span>
                            </p>
                        </div>
                    </div>
                    <div class="bus__column col">
                        <div class="d-block">
                            <label for="note">Примітка</label>
                            <div class="input-group mb-3">
                                <input type="text" class="form-control input__text" placeholder="Примітка" aria-label="note" aria-describedby="basic-addon1">
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="contact-info container">
                <div class="contact-info__wrapper">
                    <div class="contact__info">
                        <div class="">Контактна інформація</div>
                        <div class="row row-cols-md-2 row-cols-2">
                            <div class="col-sm-4 col-md-4">
                                <label for="E-mail">E-mail</label>
                                <div class="input-group">
                                    <input type="email" class="form-control input__text" placeholder="E-mail" aria-label="E-mail" aria-describedby="basic-addon1">
                                </div>
                            </div>
                            <div class="col-sm-4 col-md-4">
                                <label for="phone">Телефон</label>
                                <div class="input-group">
                                    <input type="text" class="form-control input__text" placeholder="Телефон" aria-label="phone   " aria-describedby="basic-addon1">
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="checkbox-block">
                        <div class="input-group">
                            <div class="input-group-text ">
                                <input class="form-check-input mt-0" type="checkbox" name="term" id="term">
                            </div>
                            <label for="term">Я приймаю умови повернення, публічної 
                                <a href=""> оферти </a>
                                і даю згоду на обробку персональних даних.
                            </label>
                        </div>
                    </div>
                </div>
            </div>
    </div>
</template>

<script>

export default{
    props: {
        tickets:{
            type:Object,
            required: true
        }
    },
    data(){
        return{
            freeClass: 'seat__free',
            disableClass: 'seat__disable',
            activeClass: 'active',
            cheangeSeat:'seat__cheange',
            seatS: '',
            buttonText: 'Вибір місця'
        }
    },
    methods:{
        selectSeat(value){
            this.seatS = value;
            this.buttonText = 'Змінити місце ('+value+')';
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

.ticket-info
{
    margin-left: -0.75rem;
    margin-right: -0.75rem;
    margin-top: -0.75rem;
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
    padding: 0 0.75rem !important;
    flex-basis: 0;
    flex-grow: 1;
    flex-shrink: 1;
    }
p {
    margin: 0 !important;
    padding: 0 !important;
}

.icon-input{
    background-color: #fff !important;
    border-right: 0px !important;
}

.input__block
{
    width: 100%;
    max-width: 100%;
}

.ticket__row
{
    margin-top: 0 !important;
}

.input__text
{
    font-size: 1.25rem !important;
}


.ticket__line
{
    display: block;
    position: relative;
    border-top: 0.1rem solid #cc004d;
    height: 0.1rem;
    margin: 2rem 0;
    text-align: center;
}

.ticket__line:after
{
    background: #fff;
    color: #cc004d!important;
    content: attr(data-content);
    display: inline-block;
    font-size: 1rem;
    padding: 0.3rem 0.8rem;
    transform: translateY(-1.1rem);
    text-align: center;
}

.btn__place
{
    font-size: 1.25rem !important;
    border: 1px solid #000 !important;
    padding: 5px 0px !important;
    width: 100% !important;
}

.seat__cheange
{
    background-color: #cc004d !important;
    color: #fff !important;
    border: 0px !important;
}

.bus__places
{
    display: inline-flex;
    margin-top: 10px;
    border-radius: 8px;
    border: 1px solid #ccc;
    padding: 20px;
    flex-direction: row-reverse;
}

.places__info
{
    display: flex;
    flex-direction: column-reverse;
}

.places__view
{
    display: flex;
    flex-direction: row-reverse;
}

.place__set
{
    width: 40px;
    max-width: 40px;
    height: 40px;
    max-height: 40px;
    margin: 2px;
    color: #ccc;
    fill: #ccc;
    overflow: hidden;
    position: relative;
    cursor: pointer;
    border: none;
}

.place__number
{
    color: #fff;
    font-size: 10px;
    font-weight: 700;
    position: absolute;
    left: 62%;
    top: 50%;
    transform: translate(-50%,-50%);
}

.seat__disable
{
    cursor: not-allowed !important;
}

.seat__free.active
{
    cursor: not-allowed !important;
}

.seat__free.active path
{
    fill: #65bb69;
}

.bus__way{
    color: #7a7a7a!important;
}

.bus__carrier{
    font-size: 0.75rem !important;
}

.price{
    color: #cc004d !important
}

.d-flex__al-center{
    display: flex;
    align-items: center;
}

</style>