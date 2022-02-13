<template>
<v-container>
        <h1>투두 리스트</h1>
        <p>전체 할일 : {{todoList.length}} / 완료된 일 :{{countList}} / 남은 할일 : {{todoList.length - countList}}</p>
    <v-layout row wrap>
        <v-flex xs6 pa-2>
            <List
                :todoList="todoList"
                @statusControl="stateControl"
                @listDelete="listDelete"
            />
<!-- props : todoList데이터를 :todoList라는 변수명으로 자식 컴포넌트에 전달해줘.-->
        </v-flex>
        <v-flex xs6 pa-2>
            <ListAdd
            @listAdd="listAdd"
            @listEdit="listEdit"
            />
        </v-flex>
    </v-layout>
</v-container>
</template>

<script>
    import List from './List'
    import ListAdd from'./ListAdd'

    export default{
        components : {
            List,
            ListAdd
        },
        data(){
            return{
                todoList:[],

            }
        },
        computed:{
            countList(){
                let counter = 0;
                this.todoList.forEach(list => {
                    if(list.status === "done"){
                        counter ++;
                    }
                })
                return counter;
            },
        },
        methods:{
            listAdd(memo){
                console.log('받았어!')
                this.todoList.push({memo : memo, status:"created"});
                //들고온 데이터를 객체 형태로넣어준다.
            },
            stateControl(index, status){
                this.todoList[index].status = status;
            },
            listDelete(index){
                this.todoList.splice(index,1);
            },
            listEdit(memo, index){
                this.todoList[index].memo = memo

            }
        }
    }
</script>