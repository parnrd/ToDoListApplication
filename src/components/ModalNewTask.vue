<template>
  <div class="modal-new-task">
    <button class="button-add" @click.prevent="show">Add New Task</button>
    <modal name="new-task-modal" @opened="opended" :width="500" :height="300">
      <div class="headder">
        <h1>Add Task</h1>
        <img
          class="close-modal"
          @click.prevent="hide"
          src="./../assets/close_w.png"
          alt="close"
        />
      </div>
      <form @submit.prevent="handleAddSubmit">
        <input
          ref="first"
          type="text"
          placeholder="Task"
          :class="{ 'has-error': submitting && invalideTaskName }"
          @focus="clearStatus"
          @keypress="clearStatus"
          v-model="task.name"
        /><br />
        <textarea
          v-model="task.desc"
          :class="{ 'has-error': submitting && invalideTaskDesc }"
          @focus="clearStatus"
          type="text"
          placeholder="Add Description here...."
        /><br />
        <button class="discard-btn" @click.prevent="discardChange">
          Discard
        </button>
        <button type="submit" class="add-btn">Add Task</button>
        <p v-if="summiting && error" class="error-message">
          Please fill out all required fields
        </p>
        <p v-if="success" class="success-message">Task successfully added</p>
      </form>
    </modal>
  </div>
</template>
<script>
export default {
  name: 'modal-new-task',
  data () {
    return {
      summiting: false,
      success: false,
      error: false,
      task: {
        name: '',
        desc: '',
        status: '',
        dateAdded: new Date()
      }
    }
  },
  methods: {
    opended () {
      this.$refs.first.focus()
    },
    show () {
      this.$modal.show('new-task-modal')
    },
    hide () {
      this.$modal.hide('new-task-modal')
    },
    handleAddSubmit () {
      this.summiting = true
      this.clearStatus()
      if (this.invalideTaskName || this.invalideTaskDesc) {
        this.error = true
        return
      }
      this.task.status = 'added'
      this.$emit('add:task', this.task)
      this.$refs.first.focus()
      this.task = {
        name: '',
        desc: '',
        status: '',
        dateAdded: new Date()
      }
      this.summiting = false
      this.error = false
      this.success = true
    },
    clearStatus () {
      this.success = false
      this.error = false
    },
    discardChange () {
      this.task = {
        name: '',
        desc: '',
        status: '',
        dateAdded: new Date()
      }
      this.clearStatus()
    }
  },
  computed: {
    invalideTaskName () {
      return this.task.name === ''
    },
    invalideTaskDesc () {
      return this.task.desc === ''
    }
  }
}
</script>
<style scoped>
.modal-new-task {
  border-radius: 20px;
}

.headder {
  width: 100%;
  background: #0404b4;
  color: #fff;
  position: relative;
  height: 40px;
}
.headder h1 {
  margin: 0;
  font-size: 1.5em;
  width: 50%;
  float: left;
  padding: 5px;
}
.headder .close-modal {
  cursor: pointer;
  position: absolute;
  top: 10px;
  right: 10px;
  width: 20px;
  opacity: 1;
  float: right;
}
.modal-new-task form {
  background: #424242;
  align-items: center;
  height: 100%;
}
input {
  width: calc(100% - 20px);
  margin: 5px;
  border-radius: 5px;
  font-size: 18px;
  border: solid 1px #848484;
  background-color: #424242;
  color: #fff;
}
textarea {
  width: calc(100% - 20px);
  height: 150px;
  margin: 5px;
  border-radius: 5px;
  font-size: 18px;
  border: solid 1px #848484;
  background-color: #424242;
  color: #fff;
}
.button-add {
  appearance: none;
  outline: none;
  border: none;
  background: none;
  cursor: pointer;
  display: inline-block;
  padding: 15px;
  background-color: #0404b4;
  border-radius: 5px;
  color: #fff;
  font-size: 12px;
  font-weight: 500;
  transform: translateX(50%);
  left: -50%;
  margin-top: 10px;
}
[class*="-btn"] {
  font-size: 22px;
  width: calc(30% - 10px);
  cursor: pointer;
  border-radius: 8px;
  border: solid 1px darkgrey;
  margin-top: 10px;
  float: right;
  margin-left: 5px;
}
.discard-btn {
  border: solid 1px #ff0000;
  background-color: #ff0000;
  color: #fff;
}
.add-btn {
  border: solid 1px #0040ff;
  background-color: #0040ff;
  color: #fff;
}
.error-message {
  color: #ff0000;
  font: bold;
}
.success-message {
  color: #fff;
  font: bold;
}
</style>
