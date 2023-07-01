<template>
    <div class="delivery__modal">
        <div class="delivery">
            <div class="del__cross" @click="closeDelivery">
                <div class="del__cross-1"></div> 
                <div class="del__cross-2"></div> 
            </div>
            <div class="del__orange-box">
                <img src="../assets/icons/donut.svg" alt="">
            </div>

            <div class="del__white-box">
                <form @submit.prevent="sendDelivery">
                    <h2>Доставка</h2>
                    <input v-model="name" class="w294px" type="text" placeholder="Ваше имя" id="name" required>
                    <input v-model="phone" class="w294px" type="tel" placeholder="Телефон" id="phone" required>

                    <fieldset @change="deliveryTypeChange">
                        <div class="white-box__radio">
                            <input type="radio" value="Самовывоз" id="sam" v-model="delivery">
                            <label for="sam">Самовывоз</label>
                        </div>
                        <div class="white-box__radio">
                            <input type="radio" value="Доставка" id="del" v-model="delivery" checked>
                            <label for="del">Доставка</label>
                        </div>
                    </fieldset>

                    <input v-model="adress" class="w294px" type="text" placeholder="Улица, дом, квартира" id="adress" required>

                    <div class="white-box__wrapper">
                        <input v-model="floor" type="text" placeholder="Этаж" id="floor">
                        <input v-model="domofon" type="text" placeholder="Домофон" id="domofon">
                    </div>

                    <button>Оформить</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'ym-delivery',
        data(){
            return{
                name: '',
                adress: '',
                floor: '',
                phone: '',
                domofon: '',
                delivery: ''
            }
        },
        methods: {
            deliveryTypeChange(){
                const elem = document.querySelector('.white-box__wrapper');
                const adress = document.getElementById('adress');

                if(elem.style.display == 'none'){
                    elem.style.display = "flex";
                    adress.style.display = "flex";
                }else{
                    elem.style.display = "none";
                    adress.style.display = "none";

                    this.adress = '';
                    this.domofon = '';
                    this.floor = '';
                }
            },
            closeDelivery(){
                const delivery = document.querySelector('.delivery__modal');
                delivery.style.display = "none";
            },

            sendDelivery(){
                // data send on server
                this.closeDelivery();
                this.$emit('sendData', { name: this.name, phone: this.phone, delivery: this.delivery, address: this.address, domofon: this.domofon, floor: this.floor})
            }
        }
    }
</script>