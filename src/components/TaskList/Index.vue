<template>
    <div class="form-wrapper padding">
        <Header :tasks="tasks" />
        <Tasks @edit-task="editTask" @toggle-task="toggleTask" @delete-task="deleteTask" :tasks="tasks" />
    </div>
</template>

<script>
import Header from './Header.vue';
import Tasks from './Tasks.vue';

export default {
    name: "TaskList",
    components: {
        Header,
        Tasks
    },
    props: {
        tasks: Array
    },
    methods: {
        deleteTask(id) {
            this.$emit('delete-task', id)
        },
        toggleTask(id) {
            this.$emit('toggle-task', id)
        },
        editTask(id) {
            this.$emit('edit-task', id)
        },
    },
    emits: ['delete-task', 'toggle-task', 'edit-task'],
}
</script>

<style scoped>
.padding {
    margin: 10px;
    padding: 30px;
    color: white;
}
</style>