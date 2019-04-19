<template>
    <nav class="navbar navbar-light bg-light mb-2">
        <a class="navbar-brand" href="#">
            <img src="../assets/store.png" width="50px" height="50px" alt="">
            Shopping Fruits
        </a>
        {{ dataTime }}
    </nav>
</template>
<script>
import { setTimeout } from 'timers';
export default {
    data() {
        return {
            dataT: ''
        }
    },
    computed: {
        dataTime() {
            let vm = this;
            let date = ''
            let hours
            let minutes
            let seconds 
            setInterval(function () {
                date = new Date()
                hours = date.getHours() 
                minutes = date.getMinutes()
                seconds = date.getSeconds()
                if(hours < 10) {
                    hours = '0'+hours
                }
                if(minutes < 10) {
                    minutes = '0'+minutes
                }
                if(seconds < 10) {
                    seconds = '0'+seconds
                }
                vm.dataT = `${hours}:${minutes}:${seconds}`
            }, 1000);
            return this.dataT
        }
    }
}
</script>

<style>
    .navbar {
        background-color: #48dbfb!important; 
    }
    .navbar-brand {
        font-size: 34px!important;
        font-weight: bold;
        color :#0a3d62!important;
    }
</style>