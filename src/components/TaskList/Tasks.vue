<template>
    <div>
        <table class="table text-white mb-0">
            <thead>
                <tr>
                    <th scope="col">Task Title</th>
                    <th scope="col">Task Description</th>
                    <th scope="col">Task State</th>
                    <th scope="col">Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr class="fw-normal" v-for="task in tasks" :key="task.id">
                    <td>
                        <span class="ms-2"><strong>{{ task.text }}</strong></span>
                    </td>
                    <td class="align-middle">{{ task.day }}</td>
                    <td class="align-middle">
                        <h5 class="mb-0"><span :class='task.done ? "badge bg-success ": "badge bg-danger"'>{{
                                task.done ? "Task completed" :
                                    "Task not completed"
                        }}</span></h5>
                    </td>
                    <td class="align-middle flexy">
                        <a href="#!" data-mdb-toggle="tooltip" @click="$emit('toggle-task', task.id)" title="Done">
                            <font-awesome-icon icon="fa-solid fa-check" class="check" />
                        </a>
                        <a href="#!" data-mdb-toggle="tooltip" @click="$emit('edit-task', task.id)" title="Edit">
                            <font-awesome-icon icon="fa-solid fa-pencil" class="pencil" />
                        </a>
                        <a href="#!" data-mdb-toggle="tooltip" @click="$emit('delete-task', task.id)" title="Remove">
                            <font-awesome-icon icon="fa-solid fa-trash" size="lg" class="trash" />
                        </a>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: "TasksComponent",
    props: {
        tasks: Array
    },
    emits: ['delete-task', 'toggle-task', 'edit-task'],
}
</script>

<style scoped>
.flexy{
    display: flex;
    justify-content: space-between;
    align-content: center;
}
td{
    border: none !important;
    padding: 1rem !important;
}
.pencil{
    color: white;
}
.check{
    color: yellowgreen;
}
.trash{
    color: red;
}
</style>