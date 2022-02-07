<template>
    <div>
        <v-card
            class="pa-3 mb-3"
            :class="{'done' : list.status === 'done'}"
            v-for="(list, index) in todoList"
            :key="index"
        >
            <p>{{list.memo}}</p>
            <p>{{list.status}}</p>
            <v-btn
                v-if="list.status === 'created'"
                fab flat small
                @click="$emit('statusControl', index, 'done')"
            >완료</v-btn>
            <v-btn
                v-else
                fab small
                @click="$emit('statusControl', index, 'created')"

            >부활</v-btn>
            <v-btn
                @click="$emit('listDelete', index)"
                fab small
            >제거</v-btn>
<!--            수정 버튼은 완료 상태에서는 접근이 불가야해야한다.-->
            <v-btn
                @click="listEdit(list.memo, index)"
                v-if="list.status === 'created'"
                fab small
            >수정</v-btn>
        </v-card>
    </div>
</template>
<script>
import {eventBus} from '../main'

export default {
    props :['todoList'],
    //todoList에 있는 요소들을 하나씩 불러 list에 넣고
    methods:{
        listEdit(memo, index){
            eventBus.$emit('listEdit', memo, index);
        }
    }
}
</script>

<style scoped>
/*scoped 를 쓰면 이리 파일 내에서만 작동한다.*/

.done{
    background-color: rgba(0,0,0,0.1);
}
.done p{
    text-decoration: line-through;
    color:rgba(0,0,0,0.5);
}

</style>