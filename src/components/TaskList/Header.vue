<template>
    <div class="row">
        <div class="col-6">
            <h3>Task List</h3>
        </div>
        <div class="col-6">
           <strong>Number of undone Task : </strong>{{ tasks.filter(task => task.done == false).length }}
        </div>
    </div>
</template>

<script>
export default {
    name: "HeaderBloc",
    props: {
        tasks: Array
    },
}
</script>

<style scoped>
</style>