<template>
  <div class="container" v-on:keydown.enter="add">
    <h1>ToDo App</h1>
    <div class="content">
      <input v-model="task" id="task-name-input" type="text" placeholder="Введіть своє завдання">

      <TaskList @delete="deleteTask" @editData="change" v-model:tasks="filteredTasks"></TaskList>

      <div class="info">
        <p id="counter"></p>
        <div>
          <button id="all" @click="selectedSort = 'all'" :class="classButton('all')">Всі</button>
          <button id="active" @click="selectedSort = 'active'" :class="classButton('active')">Активні</button>
          <button id="completed" @click="selectedSort = 'completed'" :class="classButton('completed')">Виконані</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TaskList from '@/components/TaskList.vue';

export default {
  components: { TaskList },
  data() {
    return {
      tasks: [],
      task: '',
      selectedSort: 'all',
    };
  },
  methods: {
    add() {
      this.tasks.filter((task) => { console.log(`${task.taskName == this.task}`); return task.taskName == this.tasks });
      if (this.tasks.filter((task) => task.taskName == this.tasks).length === 0) {
        this.tasks.push({ id: Date.now(), taskName: this.task, isCompleted: false });
        this.task = '';
        this.save();
      } else {
        alert('This task is exist');
      };
    },
    change(id) {
      this.tasks.forEach((el) => {
        if (el.id === id) {
          el.isCompleted = !el.isCompleted;
        }
      })
      this.save();
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((el) => el.id !== id);
      this.save();
    },
    save() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    classButton(text) {
      return {
        'active-button': text === this.selectedSort,
        'disactive-button': text !== this.selectedSort
      }
    }
  },
  computed: {
    filteredTasks() {
      if (this.selectedSort === 'all') {
        return this.tasks;
      }
      return this.tasks.filter((task) => task.isCompleted === (this.selectedSort === 'completed'));
    },
  },
  mounted() {
    this.tasks = JSON.parse(localStorage.getItem("tasks")) || [];
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@100;200;300;400;500;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  font-family: 'Montserrat';
  box-sizing: border-box;
  outline: none;
}

body {
  background: rgb(240, 240, 240);
  background: linear-gradient(180deg, rgba(240, 240, 240, 1) 0%, rgba(220, 220, 220, 1) 100%) no-repeat;
  height: 100%;
  min-height: 100vh;
}

.container {
  max-width: 1000px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

h1 {
  text-align: center;
  font-size: 10rem;
  font-weight: 100;
  color: rgb(170, 170, 170);
  margin-bottom: 1.5rem;
}

.content {
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  box-shadow: 0px 0px 15px -5px rgba(0, 0, 0, 0.75);
  border: 3px solid rgb(170, 170, 170);
  border-top: none;
  border-bottom: none;
  margin-bottom: 2rem;
}

#task-name-input {
  border: none;
  border-bottom: 3px solid rgb(170, 170, 170);
  padding: 1.5rem;
  width: 1000px;
  color: rgb(180, 180, 180);
  font-size: 2rem;
}

#task-name-input::placeholder {
  color: rgb(180, 180, 180);
}

#start-message {
  border: none;
  background: white;
  border-bottom: 3px solid rgb(170, 170, 170);
  padding: 1.5rem;
  width: 1000px;
  color: rgb(180, 180, 180);
  font-size: 2rem;
  text-align: center;
}

#task-list {
  display: flex;
  flex-direction: column;
}

.task {
  position: relative;
  border: none;
  border-bottom: 3px solid rgb(170, 170, 170);
  background-color: #fff;
  padding: 1.5rem;
  width: 1000px;
  color: black;
  font-size: 2rem;
  overflow: hidden;
  display: flex;
  flex-direction: row;
  align-items: center;
}

.task input {
  width: 2rem;
  height: 2rem;
  margin-right: 1rem;
}

.task input {
  width: 2rem;
  height: 2rem;
  border-radius: 50%;
  background: white;
}

.delete-task {
  position: absolute;
  right: 0.5rem;
  background: none;
  border: none;
  outline: none;
  font-size: 4rem;
  color: rgb(180, 180, 180);
}

.completed {
  text-decoration: line-through;
  color: rgb(180, 180, 180);
}

.info {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem;
  position: relative;
  width: 100%;
  background: white;
}

.info div {
  margin: 0 auto;
}

.info button {
  font-size: 1.5rem;
  padding: 1rem;
  border-radius: 5px;
  border: 3px solid rgb(170, 170, 170);
  color: rgb(170, 170, 170);
  /* background: white; */
  cursor: pointer;
}

#counter {
  position: absolute;
  left: 1rem;
  font-size: 1.5rem;
  color: rgb(170, 170, 170);
}

.active-button {
  background: rgb(230, 230, 230);
}

.disactive-button {
  background: white;
}
</style>
