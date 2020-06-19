<!-- /src/components/TodoList.vue -->
<template>
    <section>
        <transition-group name="list" tag="ul">
            <!-- v-for 디렉티브로 구현 (목록 렌더링)-->
            <li v-for="(todoItem,index) in propsdata" :key="todoItem" class="shadow">
                 <i class="checkBtn fas fa-check" aria-hidden="true"></i> 
                {{todoItem}}
                <span class="removeBtn" type="button" @click="removeTodo(todoItem,index)">
                    <i class="far fa-trash-alt" aria-hidden="true"></i> 
                </span>
                </li>
        </transition-group>
    </section>
</template>

<script>
export default {
    props:['propsdata'],
    // data(){
    //     return{
    //         todoItems:[]
    //     }
    // },
    // created 라이프 사이클 훅에서 localStorage의 데이터를 뷰로 옮긴다
    // created(){
    //     if(localStorage.length>0){
    //         for(var i=0;i<localStorage.length;i++){
    //             //처음 앱이 실행되서 라이프사이클의 created 단계에 다다르면 
    //             //webpack-dev-server에 관련된 문자열만 빼고 localStorage의 값을 Items에 넣어줍니다.
    //             if(localStorage.key(i)!=='loglevel:webpack-dev-server')
    //             this.todoItems.push(localStorage.key(i));
    //         }
    //     }
    // },
    //리스트 삭제 메소드
    methods:{
        removeTodo(todoItem,index){
            //localStorage.removeItem(todoItem)
            // splice : 배열의 특정 인덱스에서 부여한 숫자만큼의 인덱스를 삭제(js api)
            //this.todoItems.splice(index,1);
             this.$emit('removeTodo',todoItem,index)
        }
    }
}
</script>

<style scoped>
    ul{
        list-style-type: none;
        padding-left: 0px;
        margin-top: 0;
        text-align: left;
    }
    .list-enter-active, list-leave-active{
        transition: all 1s;
    }
    .list-enter, .list-leave-to{
        opacity: 0;
        transform: translateY(30px);
    }

    li{
        display: flex;
        min-height: 50px;
        height: 50px;
        line-height: 50px;
        margin: 0.5rem 0;
        padding: 0 0.9rem;
        background: #fff;
        border-radius: 5px;
    }

    .checkBtn{
        line-height: 45px;
        color: #62acde;
        margin-right: 5px;
    }
    .removeBtn{
        margin-left: auto;
        color: #de4343;
    }
</style>
