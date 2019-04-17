<template>
    <div class="container">
        <div class="row">
            <div class="col-6">
                <h4>Fruits</h4>
                <ul class="list-group">
                    <FruitItem v-for="fruit in fruits"
                    :key="fruit.id"
                    :fruit="fruit"/>
                </ul>
            </div>
            <div class="col-6">
                <h4>Carrinho</h4>
            </div>
        </div>

    </div>
</template>
<script>
    import FruitItem from './FruitItem.vue'
    export default {
        components: {
            FruitItem
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
                ]
            }
        }
    }
</script>
