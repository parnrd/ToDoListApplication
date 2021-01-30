<template>
  <div id="show-tasks">
    <ul class="search-box">
      <li>
        <img src="./../assets/search_w.png" alt="Search" />
      </li>
      <li>
        <input type="text" v-model="searchMsg" />
      </li>
    </ul>
    <table>
      <tbody>
        <tr v-for="task in tasks" :key="task.id">
          <td>
            <input
              type="checkbox"
              id="checked"
              name="checked"
              value="checked"
            />
          </td>
          <td>
            <ul class="task-desc">
              <li v-if="editingState == task.id">
                <input type="text" v-model="task.name" />
              </li>
              <li v-else>{{ task.name }}</li>
              <li v-if="editingState == task.id">
                <textarea v-model="task.desc"></textarea>
              </li>
              <li v-else>{{ task.desc }}</li>
              <li>{{ task.dateAdded | formatDate }}</li>
            </ul>
          </td>
          <td v-if="editingState == task.id">
            <button @click="editTask(task)">Save</button>
            <button @click="cancelEditMode(task)">Cancel</button>
          </td>
          <td v-else>
            <a class="btn-edit" @click="editMode(task)"
              ><img src="./../assets/edit_w.png" /><span>Edit</span></a
            >
            <a class="btn-delte"
              ><img src="./../assets/delete_w.png" /><span>Delete</span></a
            >
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  name: 'show-tasks',
  data () {
    return {
      mockTasks: [
      ],
      editingState: null
    }
  },
  props: {
    tasks: Array
  },
  methods: {
    editMode (task) {
      this.cachedTask = Object.assign({}, task)
      this.editingState = task.id
    },
    cancelEditMode (task) {
      Object.assign(task, this.cachedTask)
      this.editingState = null
    },
    editTask (task) {
      if (task.name === '' || task.desc === '') return
      this.$emit('edit:task', task.id, task)
      this.editingState = null
    }
  }
}
</script>
<style scoped>
#show-tasks {
  border: solid 1px #848484;
  background-color: #424242;
  color: #fff;
  height: 650px;
  float: left;
  width: calc(90% - 4px);
}
.search-box {
  width: 60%;
  margin-left: 20px;
  border: solid 1px #848484;
  border-radius: 8px;
  padding: 0px;
  height: 40px;
}
.search-box li:first-child {
  width: 60px;
  float: left;
}
.search-box img {
  width: 30px;
}
.search-box input {
  font-size: 18px;
  border: solid 1px #848484;
  background-color: #424242;
  color: #fff;
}
ul {
  list-style: none;
  width: calc();
}

.task-desc li:first-child {
  color: #fff;
  font-weight: 600;
}
.task-desc li {
  color: #848484;
  font-weight: 500;
}
</style>
