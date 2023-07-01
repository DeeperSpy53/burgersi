<template>
    <div class="cart-item">
        <img :src="checkImg" alt="">

        <div class="cart-item__info">
            <h5>{{ product.name }}</h5>
            <p>{{ product.weight }}г</p>
            <span>{{ product.price }}₽</span>
        </div>

        <div class="cart-item__counter">
            <button @click="$emit('minusCard', product.name)">-</button>
            <p>{{ product.count }}</p>
            <button @click="$emit('plusCard', product)">+</button>
        </div>

    </div>
</template>

<script>
    export default {
        name: 'ym-cart-item',
        props: {
            product: Object
            /*name: String,
            price: Number,
            weight: Number,
            img: String,
            count: Number*/
        },
        computed:{
            checkImg(){
                if(!this.product.img)
                    return;

                return require("../assets/eat/" + this.product.img);
            }
        }
    }
</script>