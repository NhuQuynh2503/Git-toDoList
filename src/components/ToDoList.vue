<template>
    <div class="toDoList_wrapper">
        <div class="toDoList_main">
            <input class="add-text" type="text" v-model="text" >
            <button class="btn-add" @click="addData">Add</button>
            <div class="box" v-for="(item,index) in list" :key="item.id">
                <p>{{ item.content }}</p>
                <button @click="fixData(item)" class="btn-sua">Sửa</button>
                <button @click="deleteData(index.id)" class="btn-xoa"><Icon icon="material-symbols:delete-outline"></Icon></button>
            </div>
        </div>
    </div>
    


    <div class="popup-container" v-if="isShowFix">
        <div class="popup">
            <div class="text"><input type="text" v-model="editedContent"></div>
            <button @click="saveEditedContent"  class="btn-save">Save</button>
            <button @click="fixData"  class="btn-cancel">Cancel</button>
        </div>
    </div>
</template>
<script setup>
import {ref} from "vue"

const editedContent = ref("")
const isShowFix = ref(false)
// Data duoc chua trong list
const list = ref([
    {
        id:1,
        content:"I will wake up at 8 in the moring"
    },
    {
        id:2,
        content:"I will give time for 2 hours CSS"
    },
    {
        id:3,
        content:"Then i will have breakfast"
    },

])
const text = ref("")
function addData() {
    // list.value.push({ content: text.value })
    // text.value=""
    const newID = list.value.length > 0 ? list.value[list.value.length - 1].id + 1 : 1;
    list.value.push({id:newID, content:text.value})
    text.value="";

}
function deleteData(index){
    list.value.splice(index,1);
}
const editedItemId = ref(null);
const isShowCancel  = ref(true);
function fixData(item){
    isShowFix.value = true;
    editedContent.value = item.content;
    editedItemId.value = item.id;
    isShowCancel.value = false;    
    
}
// function cancel(){
//     isShowFix.value = false;
// }
function saveEditedContent() {
    const itemIndex = list.value.findIndex(item => item.id === editedItemId.value) // Tìm index của phần tử trong mảng list
    if (itemIndex !== -1) {
        list.value[itemIndex].content = editedContent.value // Cập nhật nội dung của phần tử
    }
    isShowFix.value = false // Ẩn popup sau khi lưu
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
.toDoList_main .add-text{
    width: 350px;
    height: 50px;
    margin: 3rem 2rem;
    border-radius: 5px;
    border:1px solid  #bebdbd ;
}
.toDoList_main .btn-add {
    width: 17%;
    height: 55px;
    background: #2c6bec;
    border: none;
    color: #fff;
    border-radius: 10px;
}
.box{
    width: 480px;
    height: auto;
    margin: 1rem 2rem;
    background: #c5e1e5;
    display: flex;
    position: relative;
    justify-content: space-between; /* Căn các phần tử theo chiều ngang và giữa hai bên */
}
.box p{
    /* margin-left: 5px;
    margin-right: 20px;
    overflow: auto; 
    max-height: 50px; */
    height: 20px;
    margin-left: 5px;
    margin-right: 200px;
    word-break: break-all;
    
}
.box .btn-sua{
    position: absolute;
    right: 50px;
    width: 40px;
    height: 40px;
    margin: 5px;
    border-radius: 10px;
    border: none;
    background: rgb(192, 74, 31);
}
.box .btn-xoa{
    position: absolute;
    right: 0;
    border-radius: 10px;
    border: none;
    width: 40px;
    height: 40px;
    margin: 5px;
    background: #2c6bec;
}
/* popup */
.popup-container{
    display: flex;
    position: fixed;
    right: 0;
    top: 0;
    left: 0;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    background: #c2c1c1;
}
.popup{
    border: 1px solid #bebdbd ;
    width: 450px;
    height: 300px;
    background: #fff;
    border-radius: 10px;
}
.text{
    margin: 43px;
}
.text input{
    width: 350px;
    height: 80px;
}
.popup .btn-save{
    width: 70px;
    height: 40px;
    color: #fff;
    background:seagreen;
    margin-left: 70px;
    border: none;
    border-radius: 10px;
}
.popup .btn-cancel{
    width: 70px;
    height: 40px;
    color: #fff;
    background: red;
    margin-left: 160px;
    border: none;
    border-radius: 10px;
}
</style>