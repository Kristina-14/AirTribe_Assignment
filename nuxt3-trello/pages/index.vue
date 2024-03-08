<script lang="ts" setup>
import { ref } from 'vue'

interface Workspace{
    id: Number
    name: string
}

const newWorkspaceName = ref('')
const workspaceList = ref<Workspace[]>([])
const createWorkspace = () => {
    const randomId = Math.floor(Math.random()*100)

    workspaceList.value.push({
        id: randomId,
        name: newWorkspaceName.value
    })
    newWorkspaceName.value = ''
}
</script>

<template>
    <h1>Home Page</h1>
    <h2>Reacently Viewed</h2>
    <h2>Workspaces</h2>
    <input type = "text" v-model="newWorkspaceName"
    @keyup.enter="createWorkspace"/>
    <button @click="createWorkspace">Create a Workspace</button>
    <ul class="workspace-list">
        <li v-for="workspace in workspaceList" :key="workspace.id"
        class="workspace-card">
        
        {{ workspace.id }}: {{ workspace.name }}
        </li>
    </ul>
</template>

<style>
.workspace-card{
    background-color: rgb(203, 252, 180);
    display: block;
    border: 2px solid green;
    border-radius: 5px;
    padding: 2rem;
    margin-bottom: 1rem;
}

.workspace-list{
    margin-left: 0;
    padding-left: 0;
}
</style>