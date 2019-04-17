<template>
    <div class="container">
        <div class="row">
            <div class="col-6">
                <h4>Fruits</h4>
                <ul class="list-group">
                    <FruitItem v-for="fruit in fruits"
                    :key="fruit.id"
                    :fruit="fruit"
                    @addFruitCart="addCart($event)"/>
                </ul>
            </div>
            <div class="col-6">
                <h4>Carrinho</h4>
                <ul class="list-group">
                    <ShoppingCart v-for="fruit in cart"
                    :key="fruit.id"
                    :fruit="fruit"
                    @addTotal="total += $event"
                    @removeTotal="total -= $event"/>
                </ul>
                Total: {{ totalFormatted }}
            </div>
        </div>
    </div>
</template>
<script>
    import FruitItem from './FruitItem.vue'
    import ShoppingCart from './ShoppingCart.vue'
    export default {
        components: {
            FruitItem,
            ShoppingCart
        },
        data() {
            return {
                fruits:[
                    {id: 1, description: 'apple', value: 2.25, img: 'fruits/apple.png'},
                    {id: 2, description: 'banana', value: 1.10, img: 'fruits/banana.png'},
                    {id: 3, description: 'grape', value: 7.40, img: 'fruits/grape.png'},
                    {id: 4, description: 'orange', value: 3.75, img: 'fruits/orange.png'},
                    {id: 5, description: 'pineapple', value: 5.80, img: 'fruits/pineapple.png'},
                    {id: 6, description: 'strawberry', value: 10.35, img: 'fruits/strawberry.png'}
                ],
                cart: [],
                total: 0.0

            }
        },
        computed: {
            totalFormatted() {
                return this.total.toLocaleString('pt-br', {style: 'currency', currency: 'BRL'})
            }
        },
        methods: {
            addCart(event) {
                if(this.cart.indexOf(event) < 0) {
                    this.cart.push(event)
                    this.total += event.value
                }else {
                    alert('Objeto já adicionado ao Carrinho')
                }
            }
        }
    }
</script>