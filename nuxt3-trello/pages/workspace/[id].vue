<script>
import { workspaceList } from '../../store/global.js'

export default{
    setup(){
        return{
            workspaceList
        }
    },
    data: () =>({
        workspaceName: ''
    }),
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
<p>{{ $route.params.id }} </p>
</div>
</template>

<style>
</style>