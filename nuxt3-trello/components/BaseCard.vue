<script setup>
import { computed, ref, watchEffect } from 'vue'

const props = defineProps({
    data:Object,
    migrateList: Array, 
    parentColumn: String,
    position: Object
})

const emits = defineEmits({
    'migrate-item':  null
})

const migrateListTarget = ref('')
let initailX = ref(0);

const filteredMigrateListTarget = computed(() => {
    return props.migrateList.filter(item => item.columnName !== props.parentColumn)
})

const migrateCard = () => {
    const targetColumn = migrateListTarget.value
    const originalColumn = props.parentColumn
    console.log({targetColumn, originalColumn})

    if(targetColumn !== originalColumn){
        emits('migrate-item', {
            cardId: props.data.id,
            targetColumn,
            originalColumn
        })
    }
}

onMounted(() => {
    initailX.value = props.position.x
})

watchEffect(() => {
if(props.position.x - initailX.value > 200){
        emits("migrate-item", {
            cardId: props.data.id,
            targetColumn: "Summer",
            originalColumn: props.parentColumn,
        })
           if (props.position.x - initailX.value > 300){
        emits("migrate-item", {
            cardId: props.data.id,
            targetColumn: "Autumn",
            originalColumn: props.parentColumn
        })
    }
    }

})

</script>

<template>
           <section>
            <h1>{{ data.name }}</h1>
            <p> Position: {{ position }}</p>
            <p> original: {{ initailX }}</p>
            <select 
            name="migrate-list" 
            id="migrate-list"
            style="padding: 5px; 
            width: 100%; margin-bottom: 10px;"
            v-model="migrateListTarget">
                <option 
                v-for="column in filteredMigrateListTarget" 
                :key="`migrate-${column.columnName}`"
                :value="column.columnName"
                >
                {{ column.columnName }}
                </option>
            </select>
            <button @click="migrateCard">Migrate</button>
        </section>

</template>

<style></style>