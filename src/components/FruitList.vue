<template>
    <div class="container">
        <div class="row">
            <div class="col-md-7">
                <ul class="list-group">
                    <li class="list-group-item title">
                        <h3>Choose the fruits <img src="../assets/fruits.png" width="40px" height="40px" alt="cart"></h3>
                    </li>
                    <FruitItem v-for="fruit in fruits"
                    :key="fruit.id"
                    :fruit="fruit"
                    @addFruitCart="addCart($event)"/>
                </ul>
            </div>
            <div class="col-md-5">
                <ul class="list-group">
                    <li class="list-group-item title">
                        <h3>Cart <img src="../assets/cart.png" width="40px" height="40px" alt="cart"></h3>
                    </li>
                    <template v-if="cart == 0">
                        <li class="list-group-item text-center">
                            <h3>Empty <img src="../assets/sad.png" width="40px" height="40px" alt="cart"></h3>
                        </li>
                    </template>
                    <template v-else>
                        <ShoppingCart v-for="fruit in cart"
                        :key="fruit.id"
                        :fruit="fruit"
                        @addTotal="total += $event"
                        @removeTotal="total -= $event"
                        @removeFruit="removeFruit($event)"/>
                    </template>
                </ul>
            </div>
            <div class="col-md-12 mt-3">
                <div class="text-right">
                    <span class="money" :style="backgroundMoney">Total: {{ totalFormatted }}</span>
                </div>
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
                    {id: 6, description: 'strawberry', value: 10.35, img: 'fruits/strawberry.png'}
                ],
                cart: [],
                total: 0.0,
                wallet: 58.00,
                backgroundMoney: ''
            }
        },
        computed: {
            totalFormatted() {
                return this.total.toLocaleString('pt-br', {style: 'currency', currency: 'BRL'})
            },
        },
        watch: {
            total(newValue) {
                if(newValue < this.wallet) {
                    this.backgroundMoney = 'background-color: #78e08f'
                } else {
                    this.backgroundMoney = 'background-color: #ee5253'
                }
                var vm = this;
                setTimeout(function(){
                    vm.backgroundMoney = ''
                }, 300);
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
            },
            removeFruit(event) {
                for(let i = 0; i < this.cart.length; i++) {
                    if(this.cart[i].id == event[0]) {
                        let index = this.cart.indexOf(this.cart[i])
                        this.cart.splice(index, 1)
                        this.total -= event[1]
                    }
                }

            }
        }
    }
</script>
<style>
    .money {
        padding: 10px;
        font-size: 30px;
        border-radius: 10px;
    }
    h3 {
        font-weight: bold
    }
    .title {
        background-color: #48dbfb!important; 
    }
</style>
