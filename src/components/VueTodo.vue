<template>
  <div class="content">
    <div class="todos">
      <div class="head">
        <h1> Список дел </h1>
      </div>

      <div>
        <TheTodoForm @add="addTodo"></TheTodoForm>
      </div>

      <div
        v-for="(todo, index) in todosRender"
        :key="index"
      >
        <MyTodo :todo="todo" @changeCompleted="changeCompleted" @deleteTodo="deleteTodo"></MyTodo>
      </div>
    </div>
  </div>
</template>

<script>

import MyTodo from "@/components/Todo.vue";
import TheTodoForm from "@/components/TheTodoForm.vue";

export default {
  name: 'VueTodo',
  components: {
    MyTodo,
    TheTodoForm,
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          name: "Купить хлеб",
          text: "",
          date: "2022-10-26",
          completed: false,
        },
        {
          id: 2,
          name: "Купить масло",
          text: "Хлеб с маслом лучше чем без",
          date: "2022-10-25",
          completed: false,
        },
        {
          id: 3,
          name: "Погладить кота",
          text: "Это дело в приоритете!",
          date: "2022-10-24",
          completed: true,
        },
        {
          id: 4,
          name: "Лечь спать пораньше",
          text: "Сон способствует переработке и хранению информации. Сон (особенно медленный) облегчает закрепление изученного материала, быстрый сон реализует подсознательные модели ожидаемых событий. Во сне мозг убирает ненужные нейронные связи. Сон обеспечивает ",
          date: "2022-10-23",
          completed: false,
        },
        {
          id: 5,
          name: "Изучить Vue",
          text: "",
          date: "2022-10-20",
          completed: true,
        },
        {
          id: 6,
          name: "Погулять",
          text: "",
          date: "2022-10-19",
          completed: false,
        },
      ]
    }
  },
  methods: {

    addTodo(todo) {
      let date = new Date();
      todo.date = date.toISOString().split('T')[0];
      todo.completed = false;
      this.todos.push(todo);
    },

    changeCompleted(d) {
      const index = this.todos.findIndex(function(e) {
        console.debug(e. id + ' ' + d.id);
        if (e.id == d.id) return e;
      });
      this.todos[index].completed = d.value;
    },

    deleteTodo(todo) {
      const index = this.todos.findIndex(function(e) {
        console.debug(e. id + ' ' + todo.id);
        if (e.id == todo.id) return e;
      });
      this.todos.splice(index, 1);
    }
  },
  computed: {

    todosRender() {

      let data = [];

      data = [
        ...this.todos.filter(e => e.completed == false).sort((a, b) => { return new Date(b.date) - new Date(a.date);}),
        ...this.todos.filter(e => e.completed == true).sort((a, b) => { return new Date(b.date) - new Date(a.date);}),
      ]
      
      return data;
    },
  },
}
</script>


<style scoped>
.content {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  width: 100%;
}
.head {
  text-align: center;
}
.todos {
  max-width:48rem;
  margin:auto;
  text-align: left;
}
</style>
