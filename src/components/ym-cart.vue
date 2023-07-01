<template>
    <div class="cart">
        <div class="cart__info">
            <h2>Корзина</h2>
            <span>{{ count }}</span>
        </div>

        <p class="cart__counter" v-if="count == 0">Тут пока пусто :(</p>
        <div class="cart__items" v-else>
            <div class="cart__list">
                <CartItem v-for="item in list" :key="item.name" :product="item" @plusCard="$emit('plusCard', $event)" @minusCard="$emit('minusCard', $event)"/>
            </div>

            <div class="cart__footer">
                <div class="cart__total-price"> 
                    <span>Итого</span>
                    <p>{{totalprice}}₽</p>
                </div>

                <button @click="openDelivery">Оформить заказ</button>

                <div class="cart__free-delivery">
                    <img v-if="totalprice >= 599" src="../assets/icons/delivery.svg" alt="">
                    <p v-if="totalprice >= 599">Бесплатная доставка</p>

                    <a class="cart__hide">Свернуть</a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import CartItem from './ym-cart-item.vue'
    export default {
        name: 'ym-cart',
        components:{
            CartItem
        },
        props:{
            count: Number,
            list: Object,
            totalprice: Number
        },
        methods:{
            openDelivery(){
                const delivery = document.querySelector('.delivery__modal');
                delivery.style.display = "flex";
            },
        }
    }
</script>