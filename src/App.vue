<script>
import { reactive, toRefs } from 'vue'
import IconDelete from "./components/IconDelete.vue";
import IconEdit from "./components/IconEdit.vue";
import IconCircle from "./components/IconCircle.vue";
export default {
  name: 'App',
  components: {
    IconCircle,
    IconDelete,
    IconEdit
},
  setup() {
    const state = reactive ({
      newTaskInput: '',
      taskList: []
    })

    const addTask = () => {
      state.taskList.push(state.newTaskInput)
      state.newTaskInput = ''
    }

    return {
     ...toRefs(state),
     addTask
    }
  }
}
</script>


<template>
  <main class="main-wrapper">
    <h1 class="page-title"> Minimal Task</h1>
    <p class="subtitle">A minimal to-do app powered by Vue.js 3</p>
    <div class="new-task-wrapper">
      <input type="text"
             placeholder="Type a new to-do item"
             class="new-task-input"
             v-model="newTaskInput"
             @keyup.enter="addTask"
      />
    <button class="new-task-button">+ Add</button>
    </div>
    <nav>
      <ul class="tab-wrapper">
        <li class="tab-item is-active">
          <button class="tab-button"> All (3)</button>
        </li>
        <li>
          <button class="tab-button">Current (2)</button>
        </li>
        <li>
          <button class="tab-button">Completed (1)</button>
        </li>
      </ul>
    </nav>
    <ul class="task-list">
      <li v-for="taskItem in taskList" :key="taskItem" class="task-list-item">
        <input type="checkbox"
               class="task-list-checkbox">
        <p class="task-list-text">{{ taskItem }}</p>
        <div class="task-list-cta">
          <p><IconEdit class="task-list-cta-icon"/><span class="sr-only"
          >Edit</span>
          </p>
          <p><IconDelete class="task-list-cta-icon"/><span class="sr-only"
          >Delete</span>
          </p>
        </div>
      </li>
    </ul>
  </main>
</template>


<style>
html {
  background-color: #fbfbfb;
}

.task-list-checkbox {
  display: block;
}

.task-list {
  padding: 0;
}

.task-list-cta-icon .icon-object {
  fill: #2d2d2d;
}

.task-list-cta-icon:hover .icon-object {
  fill: #0728bf;
}

.task-list-item {
  border: 1px solid #f6f6f6;
  box-shadow: 2px 2px 8px 0px #c0c0c0;
  border-radius: 8px;
  display: flex;
  align-items: center;
  padding: 0 16px;
  margin-bottom: 16px;
}

.task-list-item:focus,
.task-list-item:hover {
  border: 1px solid #0631f8;
}

.task-list-cta {
  display: flex;
  column-gap: 16px;
}

.task-list-text {
  margin-left: 12px;
  font-weight: bold;
  flex: 1;
}

.tab-wrapper {
  display: flex;
  grid-column-gap: 30px;
  list-style: none;
  margin: 45px 0;
  padding: 0;
}


.tab-item {
  padding-bottom: 6px;
}

.tab-item:hover .tab-button{
  color: #0728bf;
}

.tab-item.is-active {
  border-bottom: 3px solid #0631f8;
}

.tab-item.is-active .tab-button {
  color: #2d2d2d;
}

.tab-button {
  border: 0;
  background-color: transparent;
  color: #6b6b6b;
  letter-spacing: 1px;
  font-weight: bold;
  font-family: "Source Code Pro";
  padding: 0;
}

.tab-button:hover {
  cursor: pointer;
}

.new-task-wrapper {
  display: flex;
}

.new-task-input {
  padding: 16px;
  font-weight: 600;
  color: #959595;
  flex: 1;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
  border: 1px solid #f6f6f6;
  box-shadow: 2px 2px 8px 0 #c0c0c0;
  letter-spacing: 1px;
}

.new-task-button {
  background-color: #0631f8;
  color: #fff;
  padding: 18px 24px;
  font-weight: 900;
  border: 0;
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;

}
.main-wrapper {
  max-width: 600px;
  margin: 0 auto;
}

.page-title {
  font-family: 'Alef', sans-serif;
  font-size: 44px;
  letter-spacing: 1.84px;
  color: #2d2d2d;
  margin-top: 104px;
  margin-bottom: 15px;
}

.subtitle {
  font-size: 1rem;
  font-weight: bold;
  color: #6b6b6b;
  margin-top: 0;
  letter-spacing: 0.67px;
}
</style>