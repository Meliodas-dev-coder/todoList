<template>
    <div class="form-wrapper">
        <h3>Add New Task Here</h3>
        <b-form @submit.stop.prevent="addTask">
            <b-form-group id="input-group-1" label="Task Title:" label-for="input-1">
                <b-form-input placeholder="New task title" v-model="form.newTitle" id="input-1" type="text">
                </b-form-input>
            </b-form-group>
            <b-form-group id="input-group-2" label="Task Date:" label-for="input-2">
                <b-form-input id="input-2" placeholder="Task Description" v-model="form.newDay" type="text">
                </b-form-input>
            </b-form-group>
            <div class="button-group">
                <b-button class="mr-2" @click="$bvModal.hide('bv-modal-example')">Cancel</b-button>
                <b-button type="submit" variant="success">Submit</b-button>
            </div>
        </b-form>
    </div>
</template>

<script>
export default {
    name: 'AddTask',
    data() {
        return {
            form: {
                newTitle: "",
                newDay: ""
            }
        }
    },
    methods: {
        addTask() {
            const newTask = {
                id: Math.floor(Math.random() * 1000),
                text: this.form.newTitle,
                day: this.form.newDay,
                done: false
            }
            this.$emit('add-task', newTask)
            this.form.newTitle = ''
            this.form.newDay = ''
        }
    }
}
</script>

<style scoped>
h3 {
    padding: 30px;
}

div {
    padding: 20px;
    margin: 10px;
    color: white;
}



.button-group {
    text-align: right;
}
</style>