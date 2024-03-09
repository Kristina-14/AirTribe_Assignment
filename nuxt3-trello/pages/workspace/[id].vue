<script>
import { workspaceList } from '../../store/global.js'

export default{
    setup(){
        return{
            workspaceList
        }
    },
    data: () =>({
        workspaceName: '',
        board: {
            columns: []
        }, 
    }),
    methods:
    {
        createColumn(){
            this.board.columns.push({
                newItemName: '',
                items: []
            })
        },
createCard(column){
    if(column.newItemName){
        column.items.push({
        id: 123,
        name: column.newItemName
    })

    column.newItemName = '';
    }
    }
    },
    mounted(){
        this.workspaceName = this.workspaceList.find(
            workspace => workspace.id === Number(this.$route.params.id)
            ).name
            console.log(this.workspaceName)
    }
}
</script>

<template><div>
<h1>{{ workspaceName }} WorkSpace (#{{ $route.params.id }})</h1>
<section>
    <h2>{{ board.name }}</h2>
    <button @click="createColumn">Create Columns </button>
    <br />    <br />
    <div class="column-grid">
    <section class="board-column" v-for="column in board.columns"> 
       
        <input type="text" v-model="column.newItemName" style="box-sizing: border-box; margin: 2%; width: 95%"
        @keyup.enter="createCard(column)"
        />
       
        <button @click="createCard(column)" style="margin: 2%; width: 95%; background-color: lightgrey; border-radius: 2px;">Create Card</button>
        <ul type="circle">
            <li v-for="item in column.items" :key="item.id">
            {{ item.name }}</li>
        </ul>
    </section>

</div>


</section>
</div>
</template>

<style>
li {
  white-space: normal; 
  word-wrap: break-word; 
}

.column-grid {
    display: flex;
    grid-template-columns: repeat(v-bind(board.columns.length),
     1fr);
}
.board-column {
    background-color: powderblue;
    border: 1px solid blue;
    border-radius: 2px;
    height: 80vh;
    margin-right: 1rem;
    padding-right: 5px;
}
.board-column input{
    width: 100%;
}
</style>