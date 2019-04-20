<template>
    <li class="list-group-item template">
        <div class="col-2 img-fruit">
            <img :src="require('../assets/'+this.fruit.img)" width="45px" height="45px"/>
        </div>
        <div class="col-5 frui-description">
            <span>{{ descriptionFormatted }} {{ fruit.kg }}</span>
            <span>{{ subtotalFormatted }}</span>
        </div>
        <div class="col-4 fruit-qtde text-right">
            <button class="button" @click.prevent="removeAmount()">
                <i class="fas fa-minus"></i>
            </button>
            {{ amount }}
            <button class="button" @click.prevent="addAmount()">
                <i class="fas fa-plus"></i>
            </button>
        </div>
        <div class="col-1 remove">
            <button class="ml-2 button" @click.prevent="removeFruit()">
                <i class="far fa-trash-alt"></i>
            </button>
        </div>
    </li>
</template>
<script>
export default {
    props:{
        fruit:{
            type: Object,
            required: true
        }
    },
    data(){
        return {
            amount: 1,
            subtotal: this.fruit.value
        }
    },
    computed: {
        descriptionFormatted() {
            return this.fruit.description.substr(0,1).toUpperCase()+this.fruit.description.substr(1)
        },
        subtotalFormatted() {
            return this.subtotal.toLocaleString('pt-br', {style: 'currency', currency: 'BRL'})
        }
    },
    methods: {
        addAmount() {
            if(this.amount < 99) {
                this.amount++
                this.subtotal += this.fruit.value
                this.$emit('addTotal', this.fruit.value)
            }
        },
        removeAmount() {
            if(this.amount > 1 ) {
                this.amount-- 
                this.subtotal -= this.fruit.value
                this.$emit('removeTotal', this.fruit.value)
            }
        },
        removeFruit() {
            this.$emit('removeFruit', [this.fruit.id, this.subtotal])
        }
    }
}
</script>
<style>
    .template {
        display: flex;
    }
    .img-fruit {
        padding-left: 0px!important;
        padding-right: 0px!important;
    }
    .frui-description {
        padding: 7px 0px 7px 0px;  
    }
    .fruit-qtde {
        padding: 7px 0px 7px 0px; 
    }
    .remove {
        padding: 7px 0px 7px 0px; 
    }
    .button {
        border:none!important;
        background-color: white!important;
        padding: 4px 8px 4px 8px;
        border-radius: 100%
    }
    .button:hover {
        background-color: #dcdde1 !important; 
    }
    .button:focus{
    outline:none;
    }
</style>
