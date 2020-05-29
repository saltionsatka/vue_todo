<template>
    <div>
       <div v-for="todo in todos" :key="todo.id">
           <todos :todo="todo" @del-todo="$emit('del-todo', todo.id)"></todos>
       </div>
    </div>
</template>

<script>
    import todos from "./TodoItem.vue";
    export default {
        name: "Todos",
        components: {
            todos
        },
        props: ["todos"]
    }
</script>

<style scoped>

</style>
