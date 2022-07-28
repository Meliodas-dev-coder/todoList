<template>
  <div class="bodyWrapper">
    <div class="contain">
      <div class="row">
        <div class="col-lg-4 col-md-12 col-sm-12">
          <AddTask @add-task="addTask" />
        </div>
        <div class="col-lg-8 col-md-12 col-sm-12">
          <TaskList @edit-task="editTask" @toggle-task="toggleTask" @delete-task="deleteTask" :tasks="tasks" />
        </div>

        <b-modal id="bv-modal-example" hide-footer>
          <template #modal-title>
            Edit Task
          </template>
          <div class="d-block text-left">
            <b-form @submit.stop.prevent="onUpdate(data.id)">
              <b-form-group id="input-group-1" label="Task Title:" label-for="input-1">
                <b-form-input :placeholder="data.text" v-model="form.newTitle" id="input-1" type="text">
                </b-form-input>
              </b-form-group>
              <b-form-group id="input-group-2" label="Task Date:" label-for="input-2">
                <b-form-input id="input-2" :placeholder="data.day" v-model="form.newDay" type="text">
                </b-form-input>
              </b-form-group>
              <div class="button-group">
                <b-button @click="$bvModal.hide('bv-modal-example')" class="mr-2">Cancel</b-button>
                <b-button type="submit" variant="success">Submit</b-button>
              </div>
            </b-form>
          </div>
        </b-modal>
      </div>
    </div>
  </div>
</template>

<script>
import AddTask from './components/AddTask/Index.vue'
import TaskList from './components/TaskList/Index.vue'

export default {
  name: 'App',
  components: {
    AddTask,
    TaskList
  },
  methods: {
    addTask(newTask) {
      this.tasks = [...this.tasks, newTask]
    },
    deleteTask(id) {
      this.boxTwo = ''
      this.$bvModal.msgBoxConfirm('Please confirm that you want to delete this item.', {
        title: 'Please Confirm',
        size: 'md',
        buttonSize: 'md',
        okVariant: 'primary',
        okTitle: 'Confirm',
        cancelTitle: 'Cancel',
        footerClass: 'p-2',
        hideHeaderClose: false,
        centered: true
      })
        .then(value => {
          this.boxTwo = value;
          if (value == true) {
            this.tasks = this.tasks.filter((task) => task.id !== id)
          }
        })
        .catch(err => {
          console.log(err)
        })

    },
    toggleTask(id) {
      this.tasks = this.tasks.map((task) => task.id === id ? { ...task, done: !task.done } : task)
    },
    editTask(id) {
      this.tasks = this.tasks.filter((task) => task.id === id ? this.data = { ...task } : task)
      this.$bvModal.show('bv-modal-example')
    },
    onUpdate(id) {
      this.tasks = this.tasks.map((task) => task.id === id ? { ...task, text: this.form.newTitle || task.text, day: this.form.newDay || task.day } : task)
      this.form.newTitle=''
      this.form.newDay=''
      this.$bvModal.hide('bv-modal-example')
    }
  },
  data() {
    return {
      tasks: [],
      data: '',
      form: {
        newTitle: "",
        newDay: ""
      }
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Task Test Number 01',
        day: 'Wendesday 27th July 2022 at 14:00',
        done: true,
      },
      {
        id: 2,
        text: 'Task Test Number 02',
        day: 'Wendesday 27th July 2022 at 14:00',
        done: false,
      },
      {
        id: 3,
        text: 'Task Test Number 03',
        day: 'Wendesday 27th July 2022 at 14:00',
        done: true,
      },
      {
        id: 4,
        text: 'Task Test Number 04',
        day: 'Wendesday 27th July 2022 at 14:00',
        done: false,
      },
    ]
  },

}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.button-group{
  margin: 10px;
  text-align: right;;
}
.contain{
  width: 100%;
  padding: 30px;
}
.form-wrapper {
  background: rgba(24, 24, 16, .2);
  border-radius: 2em;
  backdrop-filter: blur(25px);
  border: 2px solid rgba(255, 255, 255, 0.05);
  background-clip: padding-box;
  box-shadow: 10px 10px 10px rgba(46, 54, 68, 0.03);
}
body{
  background: linear-gradient(to right, rgba(126, 64, 246, 1), rgba(80, 139, 252, 1));
}
.bodyWrapper {
  
  height: 100%;
}

.mr-2 {
  margin-right: 5px;
}
</style>
