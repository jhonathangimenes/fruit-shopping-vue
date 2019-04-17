<template>
    <li class="list-group-item" @click="addCart()">
        <img :src="require('../assets/'+this.fruit.img)" width="50px" height="50px"/>
        <span class="item">{{ descriptionFormatted }} 1Kg</span>
        <span class="item">{{ valueFormatted }}</span>
    </li>
</template>

<script>
export default {
    props: {
        fruit: {
            type: Object,
            required: true
        }
    },
    computed: {
        valueFormatted() {
            return this.fruit.value.toLocaleString("pt-BR",
                { style: 'currency', currency: 'BRL' }
            )
        },
        descriptionFormatted() {
            return this.fruit.description.substr(0,1).toUpperCase()+this.fruit.description.substr(1)
        }
    },
    methods: {
        addCart() {
            this.$emit('addFruitCart', this.fruit)
        }
    }
}
</script>

<style>
    .button-kg {
        border-style: solid;
        border-width: 1px;
        border-color: #ced6e0;
        width: 60px;
        height: 30px;
        font-size: 15px;
        text-align: center;
    }
    .item {
        margin: 5px;
    }
    span {
        font-family: 'Permanent Marker', cursive;
        font-size: 20px;
    }
</style>
