<!-- /src/App.vue -->

<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>

</template>

<script>
// import 불러올 파일의 내용이 담길 객체 from '불러올 파일 위치'
import TodoHeader from './components/TodoHeader'; 
import TodoInput from './components/TodoInput';
import TodoList from './components/TodoList';
import TodoFooter from './components/TodoFooter';

export default{
  data(){
    return{
      //데이터 속성 todoItems 선언
      todoItems:[]
    }
  },
  methods:{
    
    clearAll(){
       localStorage.clear();
       this.todoItems = [];
    },
    addTodo(todoItem){
      //localStorage에 data를 추가하는 로직
      localStorage.setItem(todoItem,todoItem);
      this.todoItems.push(todoItem);
    },
    removeTodo(todoItem,index){
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index,1);
    }
  },
  created(){
      if(localStorage.length>0){
          for(var i=0;i<localStorage.length;i++){
              //처음 앱이 실행되서 라이프사이클의 created 단계에 다다르면 
              //webpack-dev-server에 관련된 문자열만 빼고 localStorage의 값을 Items에 넣어줍니다.
              if(localStorage.key(i)!=='loglevel:webpack-dev-server')
              this.todoItems.push(localStorage.key(i));
          }
      }
  },
  components:{
    // 컴포넌트 이름 : 컴포넌트 내용
    'TodoHeader':TodoHeader,
    'TodoInput':TodoInput,
    'TodoList':TodoList,
    'TodoFooter':TodoFooter
    
  }
}

</script>

<style>
body{
  text-align: center;
  background-color: #f6f6f8;
}
input{
    border-style:groove;
}
button{
  border-style: groove;
  width: 200px;
}
.shadow{
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.3);
}
</style>
