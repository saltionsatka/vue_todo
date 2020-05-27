<template>
    <div>
       <div v-for="todo in todoList" :key="todo.id">{{ todo.title }}</div>
    </div>
</template>

<script>
    export default {
        name: "Todos",
        props: ["todoList"]
    }
</script>

<style scoped>

</style>
