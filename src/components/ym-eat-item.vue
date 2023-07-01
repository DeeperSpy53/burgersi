<template>
    <div class="eat-item">
        <img :src="checkImg" alt="">
        <h3>{{ product.price }}₽</h3>
        <h4>{{ product.name }}</h4>
        <p>{{ product.weight }}г</p>
        <button @click="$emit('addcart', product)">Добавить</button>
    </div>
</template>

<script>
    export default {
        name: 'ym-eat-item',
        props: {
            product: Object
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