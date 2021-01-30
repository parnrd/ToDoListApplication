<template>
  <div class="nav-bar">
    <modal-new-task @add:task="addNewTask"></modal-new-task>
    <p>Folders</p>
    <ul>
      <li>
        <a>
          <img
          class="img-btn"
          src="./../assets/list_w.png"
          alt="All Task"
        />
          All Task <span class="box-all-task">{{ this.tasks.length }}</span></a
        >
      </li>
      <li>
        <a>
          <img
          class="img-btn"
          src="./../assets/star_w.png"
          alt="Important"
        />
          Important
          <span class="box-important-task">{{ this.tasks.length }}</span></a
        >
      </li>
      <li>
        <a>
          <img
          class="img-btn"
          src="./../assets/send_w.png"
          alt="Complete"
        />
          Complete
          <span class="box-complete-task">{{ this.tasks.length }}</span></a
        >
      </li>
      <li>
        <a>
          <img
          class="img-btn"
          src="./../assets/delete_w.png"
          alt="Trash"
        /> Trash </a>
      </li>
      <br />
    </ul>
  </div>
</template>

<script>
import ModalNewTask from './ModalNewTask.vue'
export default {
  name: 'nav-bar-menu',
  components: {
    ModalNewTask
  },
  props: {
    tasks: Array
  },
  methods: {
    addNewTask (task) {
      const lastId =
        this.tasks.length > 0 ? this.tasks[this.tasks.length - 1].id : 0
      const id = lastId + 1
      const taskNew = { ...task, id }
      this.tasks = [...this.tasks, taskNew]
      console.log(this.tasks)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.nav-bar {
  position: relative;
  display: inline-block;
  width: 10%;
  height: 650px;
  align-items: center;
  float: left;
  border: solid 1px #848484;
  background-color: #424242;
}
p {
  font-weight: normal;
  padding: 5px;
  color: #fff;
}
ul {
  list-style-type: none;
  padding: 5px;
}
li {
  display: block;
  margin-bottom: 0.3rem;
}
li a span {
  padding: 2px;
  border-radius: 2px;
  float: right;
  right: 0;
}
a {
  color: #fff;
}
.box-all-task {
  background: #0404b4;
  color: #fff;
}
.box-important-task {
  background-color: #ffff00;
  color: #000;
}
.box-complete-task {
  background-color: #ff0000;
  color: #fff;
}
[class*="img-btn"]{
width: 20px;
    position: relative;
    display: inline-block;
    left: 1px;
    top: 5px;
}
</style>
