<template>
    <div class="cat">
        <h2>{{ name }}</h2>

        <div class="cat__wrapper">
            <EatItem v-for="item in eat" :key="item.name" :product="item" @addcart="$emit('addcart', $event)"/>
        </div>
    </div>
</template>

<script>
    // <EatItem name="Мясная бомба" :price="689" :weight="520" img="meetbomb.jpg"/>
    import EatItem from './ym-eat-item.vue'
    export default {
        name: 'ym-cat',
        props:{
            name: String,
            cat: Number,
            eat: Object
        },
        components:{
            EatItem
        }
    }
</script>