<template>
    <div class="container">
        <div class="row">
            <div class="col-md-7 mb-2">
                <ul class="list-group">
                    <li class="list-group-item title">
                        <h3>
                            Escolha as frutas 
                            <img src="../assets/fruits.png" width="40px" height="40px" alt="cart">
                        </h3>
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
                        <div class="row">
                            <div class="col-8">
                                <h3>
                                    Carrinho
                                    <img src="../assets/cart.png" width="40px" height="40px" alt="cart">
                                </h3>
                            </div>
                            <div class="col-4 text-right remove-div">
                                <button class="remove-all" @click.prevent="removeAll()">
                                    <img src="../assets/garbage.png" width="40px" height="40px" alt="cart">
                                </button>
                            </div>
                        </div>
                    </li>
                    <template v-if="cart == 0">
                        <li class="list-group-item text-center">
                            <h3>Carrinho vazio <img src="../assets/sad.png" width="40px" height="40px" alt="remove all"></h3>
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
                    {id: 1, description: 'maça', value: 2.25, img: 'fruits/apple.png'},
                    {id: 2, description: 'banana', value: 1.10, img: 'fruits/banana.png'},
                    {id: 3, description: 'uva', value: 7.40, img: 'fruits/grape.png'},
                    {id: 4, description: 'laranja', value: 3.75, img: 'fruits/orange.png'},
                    {id: 6, description: 'morango', value: 10.35, img: 'fruits/strawberry.png'}
                ],
                cart: [],
                total: 0.0,
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
                this.backgroundMoney = 'background-color: #78e08f'
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
                    alert('Essa fruta já foi adicionada ao carrinho')
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

            },
            removeAll() {
                this.cart = []
                this.total = 0
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
    .remove-all {
        border:none!important;
        background-color: #48dbfb!important;
    }
    .remove-all:hover {
        transform: scale(1.1);
    }
    .remove-all:focus{
    outline:none;
    }
    .remove-div {
        padding-right: 3px 
    }
</style>
