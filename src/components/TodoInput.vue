<!-- /src/components/TodoInput.vue -->
<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <i class="addBtn fas fa-plus" aria-hidden="true"></i>
        </span>
        <!-- <button v-on:click="addTodo">추가</button> -->
    </div>
</template>

<script>
export default {
    data(){
        return{ 
            newTodoItem:''
        }
    },methods:{
        addTodo(){
            //input에 입력 값이 있을 때만 저장
            if(this.newTodoItem!==""){
                // input에 입력된 텍스트의 앞뒤 공백 문자열 제거
                var value = this.newTodoItem && this.newTodoItem.trim();
                //localStorage.setItem(value,value);
                // TodoInput 컴포넌트에서 App 컴포넌트로 이벤트 전달
                this.$emit('addTodo',value)
                this.clearInput();
            }
           
        },
        clearInput(){
            this.newTodoItem="";
        }
    }
}
</script>

<style>
input:focus{
    outline: none;
}

.inputBox{
    background-color: #fff;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}

.inputBox input{
    border-style: none;
    font-size: 0.9rem;
}
.addContainer{
    float: right;
    background: linear-gradient(to right, #6478fb,#8763fb);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.addBtn{
    color: #fff;
    vertical-align: middle;
}
</style>
