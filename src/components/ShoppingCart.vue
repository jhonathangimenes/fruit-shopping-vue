<template>
    <li class="list-group-item template">
        <img :src="require('../assets/'+this.fruit.img)" width="50px" height="50px"/>
        <span>{{ descriptionFormatted }} {{ fruit.kg }}</span>
        <div>
            <button @click.prevent="addAmount()"><i class="fas fa-plus"></i></button>
            {{ amount }}
            <button@click.prevent="removeAmount()"><i class="fas fa-minus"></i></button>
        </div>
        <span>Valor: {{ subtotalFormatted }}</span>
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
    }
}
</script>
<style>
    .template {
        display: flex;
    }
</style>
