<template>
    <main>
        <Delivery @sendData="sendData($event)"/>
        <Product :product="product" @plusCard="AddInCart($event)"/>
        <div class="eat-cats">
            <EatCat :name="cats[0]" icon="burgers.svg" :choose="cat" :id="0" @click="cat=0"/>
            <EatCat :name="cats[1]" icon="snacks.svg" :choose="cat" :id="1" @click="cat=1"/>
            <EatCat :name="cats[2]" icon="hotdog.svg" :choose="cat" :id="2" @click="cat=2"/>
            <EatCat :name="cats[3]" icon="combo.svg" :choose="cat" :id="3" @click="cat=3"/>
            <EatCat :name="cats[4]" icon="shaurma.svg" :choose="cat" :id="4" @click="cat=4"/>
            <EatCat :name="cats[5]" icon="pizza.svg" :choose="cat" :id="5" @click="cat=5"/>
            <EatCat :name="cats[6]" icon="vok.svg" :choose="cat" :id="6" @click="cat=6"/>
            <EatCat :name="cats[7]" icon="deserts.svg" :choose="cat" :id="7" @click="cat=7"/>
            <EatCat :name="cats[8]" icon="sous.svg" :choose="cat" :id="8" @click="cat=8"/>
        </div>

        <div class="wrapper">
            <Cart :count="count" :list="card" :totalprice="totalprice" @plusCard="AddInCart($event)" @minusCard="minusCard($event)"/>

            <Cat :name="cats[cat]" :cat="cat" :eat="eat[cat]" @addcart="AddProduct($event)"/>
        </div>
    </main>
</template>

<script>
    import EatCat from './ym-eat-cat.vue'
    import Cart from './ym-cart.vue'
    import Cat from './ym-cat.vue'
    import Delivery from './ym-delivery.vue'
    import Product from './ym-product.vue'

    export default {
        name: 'ym-content',
        components:{
            EatCat,
            Cart,
            Cat,
            Delivery,
            Product
        },
        methods:{
            sendData(e){
                // send cart, totalprice and client data on server
                console.log(e);
            },
            AddProduct(e){
                this.product = e;
                const elem = document.querySelector('.product__modal');
                elem.style.display = "flex";
            },
            AddInCart(event){
                let isHave = false;
                this.count++;
                this.totalprice += event.price;

                if(this.card.length > 0){
                    for(let i in this.card){
                        if(this.card[i].name == event.name){
                            if(isNaN(this.card[i].count)){
                                this.card[i].count = 1;
                            }
                            else{
                                this.card[i].count += 1;
                            }

                            isHave = true;
                        }
                    }
                }
                if(!isHave){
                    this.card.push(event);
                    this.card[this.card.length-1].count = 1;
                }
            },
            minusCard(e){
                let key = this.card.findIndex(function(cart){
                    return cart.name == e;
                });

                this.totalprice -= this.card[key].price;
                this.count -= 1;

                if(this.card[key].count <= 1){
                    this.card.splice(key, 1);
                }else{
                    this.card[key].count -= 1;
                }
            }
        },
        data(){
            return{
                count: 0,
                cat: 0,
                totalprice: 0,
                product: [],

                cats: ['Бургеры', 'Закуски', 'Хот-доги', 'Комбо', 'Шаурма', 'Пицца', 'Вок', 'Десерты', 'Соусы'],

                eat:[
                    [
                        {
                            name: 'Мясная бомба',
                            price: 689,
                            weight: 520,
                            img: 'meetbomb.jpg',
                            desc: 'Супер мясное наслаждение! Большая рубленая котлета из свежего говяжего мяса покорит вас своей сочностью, а хрустящие листья салата добавят свежести.',
                            compound: ['Пшеничная булочка', 'Котлета из говядины', 'Красный лук', 'Листья салата', 'Соус горчичный'],
                            kcal: 430
                        },
                        {
                            name: 'Супер сырный',
                            price: 550,
                            weight: 512,
                            img: 'supercheese.jpg'
                        },
                        {
                            name: 'Сытный',
                            price: 639,
                            weight: 580,
                            img: 'meetbomb.jpg'
                        },
                        {
                            name: 'Сытный',
                            price: 639,
                            weight: 580,
                            img: 'meetbomb.jpg'
                        },
                        {
                            name: 'Сытный',
                            price: 639,
                            weight: 580,
                            img: 'meetbomb.jpg'
                        },
                        {
                            name: 'Сытный',
                            price: 639,
                            weight: 580,
                            img: 'meetbomb.jpg'
                        }
                    ],
                    [
                        {
                            name: 'Начос',
                            price: 250,
                            weight: 220,
                            img: 'meetbomb.jpg'
                        },
                    ]
                ],

                card: []
            }
        }
    }
</script>