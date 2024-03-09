<script>
import { workspaceList } from '../../store/global.js'

export default{
    setup(){
        return{
            workspaceList
        }
    },
    data: () =>({
        newColumnName: '',
        workspaceName: '',
        board: {
            columns: [
                {
                columnName: 'Winter',
                newItemName: '',
                items: [
                {
        id: 123,
        name: 'Rocket Punch'
    }
                ]
                },
                {
                columnName: 'Summer',
                newItemName: '',
                items: []
                }, 
                {
                columnName: 'Autumn',
                newItemName: '',
                items: []
                }
            ]
        }, 
    }),
    methods:
    {
        createColumn(){
            if (this.newColumnName){
                this.board.columns.push({
                columnName: this.newColumnName,
                newItemName: '',
                items: []
            })
            this.newColumnName=''
            }
        },
createCard(column){
    if(column.newItemName){
        column.items.push({
        id: 123,
        name: column.newItemName
    })

    column.newItemName = '';
    }
    },
    migrateItem({ cardId, targetColumn, originalColumn}){
        // console.log(payload)
        
        //Step1: Move item to new list
        this.board.columns.find(column => column.columnName === targetColumn).items.push(
            this.board.columns.find(column => column.columnName === originalColumn).items.
            find(item => item.id === cardId)
        )
        //Step2: Delete item from old list
        const parentColumn = this.board.columns.find(
            column => column.columnName === originalColumn
        )
        parentColumn.items = parentColumn.items.filter(item => item.id !== cardId)
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
    <div>
    <input class="form-control me-2"
    v-model="newColumnName"
    type="text" placeholder="New Column Title"
    style="
    display: inline-block;
    width: auto;
    padding: 5px;"
        @keyup.enter= "createColumn"
    />

    <button style="vertical-align: top;" class="btn btn-success" @click="createColumn">Create Columns </button>
</div>
    <br />   
    <div class="column-grid">
    <section class="board-column" v-for="column in board.columns"> 
       <h4 style="margin-bottom: -10px; padding: 5px;">{{ column.columnName }}</h4>
       <hr/>
        <input class="form-control me-2" placeholder="task" 
        type="text" v-model="column.newItemName" style="box-sizing: border-box; margin: 2%; width: 95%"
        @keyup.enter="createCard(column)"
        />
       
        <button class="btn btn-success" @click="createCard(column)" style="margin: 2%; width: 95%;">
            Create Card</button>
        <ul type="circle">
            <li v-for="item in column.items" 
            :key="item.id" 
            style="margin-left: -1.5rem;">
          <BaseCard :data="item"
          :parentColumn="column.columnName"
          :migrateList="board.columns"
          @migrate-item="migrateItem"/>
        </li>
        </ul>
    </section>

</div>


</section>
</div>
</template>

<style scoped>
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