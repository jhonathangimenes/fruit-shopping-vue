<template>
    <li class="list-group-item template">
        <img :src="require('../assets/'+this.fruit.img)" width="50px" height="50px"/>
        <span class="item">{{ descriptionFormatted }} 1Kg</span>
        <span class="item">{{ valueFormatted }}</span>
        <div class="peso ml-auto">
            <a href=""><i class="fas fa-plus-circle"></i></a>
            <div class="button-kg item">
                <span class="value">{{ kg }}</span>
            </div>
            <a href=""><i class="fas fa-minus-circle"></i></a>
        </div>
    </li>
</template>

<script>
export default {
    data() {
        return {
            kg: 5.544,
            valor: 0.0
        }
    },
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
    .template {
        display: flex;
        font-size: 25px;
        font-family: 'Permanent Marker', cursive;
    }
    .item {
        margin: 5px;
    }
    .fas {
        padding-top: 10px;
    }
    .peso {
        display: flex;
        padding-top: 15px;
    }
    span {
        padding-top: 10px;
    }
</style>
