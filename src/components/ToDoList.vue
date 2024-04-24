<template>
    <div class="toDoList_wrapper">
        <div class="toDoList_main">
            <input type="text" v-model="text" >
            <button @click="addData">Add</button>
            <div class="box" v-for="(item,index) in list" :key="index">
                <p>{{ item.content }}</p>
                <button @click="deleteData(index)" class="btn"><Icon icon="material-symbols:delete-outline"></Icon></button>
            </div>
        </div>
    </div>

</template>
<script setup>
import {ref} from "vue"


const list = ref([
    {
        content:"I will wake up at 8 in the moring"
    },
    {
        content:"I will give time for 2 hours CSS"
    },
    {
        content:"Then i will have breakfast"
    },

])
const text = ref("")
function addData() {
    list.value.push({ content: text.value })
    text.value=""
}
function deleteData(index){
    list.value.splice(index,1)
}
</script>
<style scoped>
.toDoList_wrapper{
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #2261cb;
    width: 100%;
    height: 100%;
}
.toDoList_main{
    width: 550px;
    height: 550px;
    background: #fff;
    border: .5px solid rgba(0, 0, 0, .1);
    border-radius: 10px;
}
.toDoList_main input{
    width: 350px;
    height: 50px;
    margin: 3rem 2rem;
    border-radius: 5px;
    border:1px solid  #bebdbd ;
}
.toDoList_main button{
    width: 17%;
    height: 55px;
    background: #2c6bec;
    border: none;
    color: #fff;
    border-radius: 10px;
}
.box{
    width: 480px;
    height: 50px;
    margin: 1rem 2rem;
    background: #c5e1e5;
    display: flex;
    position: relative;
}
.box p{
    margin-left: 5px;
    margin-right: 200px;
}
.box .btn{
    position: absolute;
    right: 0;
    width: 40px;
    height: 40px;
    margin: 5px;
}

</style>