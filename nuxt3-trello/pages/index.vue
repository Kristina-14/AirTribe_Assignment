<script setup>
import { ref } from 'vue'
import { workspaceList } from '../store/global.js'

const newWorkspaceName = ref('')
////const workspaceList = ref<Workspace[]>([])
const createWorkspace = () => {
    const randomId = Math.floor(Math.random()*100)

    workspaceList.value.push({
        id: randomId,
        name: newWorkspaceName.value
    })
    newWorkspaceName.value = ''
}
</script>

<template><div style="margin-left: 1rem;">
    <h2 >Home Page</h2>

    <h4>Workspaces</h4>
    <br/><div style="display: flex;">
    <input style="width: auto;" placeholder="Workspace Name" class="form-control me-2" type = "text" v-model="newWorkspaceName"
    @keyup.enter="createWorkspace"/> 
    &nbsp;&nbsp;
    <button class="btn btn-success" @click="createWorkspace">Create a Workspace</button>
    </div><br/>
    <ul class="workspace-list">
        <li v-for="workspace in workspaceList" :key="workspace.id"
        class="workspace-card">
        <nuxt-link :to="`/workspace/${workspace.id}`" style="text-decoration: none; color: white; font-weight: 400;">{{ workspace.id }}: {{ workspace.name }}</nuxt-link>
        </li>
    </ul>
    
    </div>
</template>

<style>
.workspace-card{
    background-color: rgba(1, 81, 32, 0.747);
    width: 95%;
    display: block;
    border: 2px solid green;
    border-radius: 5px;
    padding: 2rem;
    margin-bottom: 1rem;
}

.workspace-list{
    margin-left: 0;
    padding-left: 0;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-column: 10px;
}
</style>