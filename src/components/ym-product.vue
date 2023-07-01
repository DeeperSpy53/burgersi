<template>
    <div class="product__modal">
        <div class="product">
            <div class="product__cross" @click="closeProduct">
                <div class="product__cross-1"></div> 
                <div class="product__cross-2"></div> 
            </div>
            <h2>{{ product.name }}</h2>

            <div class="product__wrapper">
                <div class="product__img">
                    <img :src="checkImg" alt="">
                </div>
                <div class="product__desc">
                    <p>{{ product.desc }}</p>

                    <h3>Состав:</h3>
                    <ul>
                        <li v-for="item in product.compound" :key="item">{{ item }}</li>
                    </ul>
                    <span>{{ product.weight }}г, ккал {{ product.kcal }}</span>
                </div>
            </div>

            <div class="product__counter">
                <button class="product__btnadd" @click="productAdd">Добавить</button>

                <div class="product-counter__btn">
                    <button @click="if(counter != 1) counter--;">-</button>
                    <p>{{ counter }}</p>
                    <button @click="counter++">+</button>
                </div>

                <span>{{ product.price }}₽</span>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'ym-product',
        props:{
            product: Object
        },
        methods:{
            productAdd(){
                if(this.counter > 0){
                    for(let i = 0; i < this.counter; i++){
                        this.$emit('plusCard', this.product);
                    }
                }
                this.closeProduct();
                this.counter = 1;

                console.log("12");
            },

            closeProduct(){
                const elem = document.querySelector('.product__modal');
                elem.style.display = "none";
            }
        },
        computed:{
            checkImg(){
                if(!this.product.img)
                    return;

                return require("../assets/eat/" + this.product.img);
            }
        },
        data(){
            return{
                counter: 1
            }
        }
    }
</script>