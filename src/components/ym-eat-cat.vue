<template>
    <div v-if="choose==id" class="eat choose-cat">
        <img :src="checkImg" alt="">
        <h4>{{name}}</h4>
    </div>
    <div v-else class="eat">
        <img :src="checkImg" alt="">
        <h4>{{name}}</h4>
    </div>
</template>

<script>
    export default {
        name: 'ym-eat',
        props:{
            name: String,
            icon: String,
            choose: Boolean,
            id: Number
        },
        computed:{
            checkImg(){
                if(!this.icon)
                    return;

                return require("../assets/icons/cats/" + this.icon);
            }
        }
    }
</script>