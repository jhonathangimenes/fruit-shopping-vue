<template>
    <li class="list-group-item template" @click="addCart()">
            <div class="col-8 img-fruit-description">
                <img :src="require('../assets/'+this.fruit.img)" width="45px" height="45px"/>
                <span class="item">{{ descriptionFormatted }} 1Kg</span>
            </div>
            <div class="col-4 text-right value">
                <span class="item">{{ valueFormatted }}</span>
            </div>
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
    .template {
        display: flex;
    }
    .img-fruit-description {
        padding-left: 0px;
    }
    .button-kg {
        border-style: solid;
        border-width: 1px;
        border-color: #ced6e0;
        width: 60px;
        height: 30px;
        font-size: 15px;
        text-align: center;
    }
    .value {
        padding-right: 0px
    }
    .item {
        margin: 5px;
    }
</style>
