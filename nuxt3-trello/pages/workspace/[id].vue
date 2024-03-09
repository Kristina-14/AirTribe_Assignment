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

<template><div style="margin-left: 1rem;">
<h2>{{ workspaceName }} WorkSpace (#{{ $route.params.id }})</h2>
<section>
    <h2>{{ board.name }}</h2>
    <button class="btn btn-success" @click="createColumn">Create Columns </button>
    <br />    <br />
    <div class="column-grid">
    <section class="board-column" v-for="column in board.columns"> 
       
        <input class="form-control me-2" placeholder="task" 
        type="text" v-model="column.newItemName" style="box-sizing: border-box; margin: 2%; width: 95%"
        @keyup.enter="createCard(column)"
        />
       
        <button class="btn btn-success" @click="createCard(column)" style="margin: 2%; width: 95%;">
            Create Card</button>
        <ul type="circle">
            <li v-for="item in column.items" :key="item.id" style="margin-left: -1.5rem;">
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
border: 1px solid green;
border-radius: 5px;
list-style: none;
padding: 5px;
margin-top: 5px;
margin-bottom: 7px;
margin-right: 5px;
background-color: #f0f0f0;
}

.column-grid {
    display: flex;
    grid-template-columns: repeat(v-bind(board.columns.length),
     1fr);
}
.board-column {
    background-color: rgb(148, 190, 142);
    border: 1px solid green;
    border-radius: 2px;
    height: 80vh;
    margin-right: 1rem;
    padding: 5px;
}
.board-column input{
    width: 100%;
    white-space: normal; 
  word-wrap: break-word; 
}
</style>