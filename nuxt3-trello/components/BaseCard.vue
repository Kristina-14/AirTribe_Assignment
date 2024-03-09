<script setup>
defineProps({
    data:Object,
    migrateList: Array, 
    parentColumn: String
})
</script>

<template>
           <section>
            <h1>{{ data.name }}</h1>

            <select name="migrate-list" 
            id="migrate-list"
            style="padding: 5px; 
            width: 100%; margin-bottom: 10px;">
                <option 
                v-for="column in migrateList" 
                :key="`migrate-${column.columnName}`"
                :value="column.columnName"
                >
                {{ column.columnName }}
                </option>
            </select>
            <button>Migrate</button>
        </section>

</template>

<style></style>