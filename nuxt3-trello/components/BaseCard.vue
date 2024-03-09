<script setup>
import { computed, ref } from 'vue'

const props = defineProps({
    data:Object,
    migrateList: Array, 
    parentColumn: String
})

const emits = defineEmits({
    'migrate-item':  null
})

const migrateListTarget = ref('')

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
</script>

<template>
           <section>
            <h1>{{ data.name }}</h1>

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