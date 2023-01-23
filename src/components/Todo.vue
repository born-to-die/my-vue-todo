<template>

    <div class="todo">

        <div :class="todo.completed ? 'head row text-muted' : 'head row'">

            <div class="col-12 col-sm">
                <span class="h4"> {{ todo.name }} </span> 
                <span class="mx-2 small text-muted" > {{ todo.date }} </span>
                <div :class="todo.completed ? 'text text-muted' : 'text'">
                    {{ todo.text }}
                </div>
            </div>

            <div class="col-12 col-sm-3">

                <b-button
                    v-if="!todo.completed"
                    @click="changeCompleted(true)"
                    type="submit"
                    variant="success"
                    class="w-100 mb-1"> Готово </b-button>

                <b-button
                    v-if="todo.completed"
                    @click="changeCompleted(false)"
                    type="submit"
                    variant="outline-secondary"
                    class="w-100 mb-1"> Вернуть </b-button>

                <b-button
                    @click="deleteTodo()"
                    type="submit"
                    :variant="todo.completed ? 'outline-secondary' : 'outline-danger'"
                    class="w-100 "> Удалить </b-button>

            </div>

        </div>

    </div>

</template>
  
  <script>
  export default {
    name: 'MyTodo',
    props: {
        todo: {
            required: true,
            type: Object,
        },
    },
    data() {
      return {
        completed: this.todo.completed,
      }
    },
    methods: {
        changeCompleted(value) {
            this.$emit('changeCompleted', {id: this.todo.id, value: value});
        },
        deleteTodo() {
            this.$emit('deleteTodo', {id: this.todo.id});
        }
    },
    watch: {
        'todo.completed'() {
            this.completed = this.todo.completed
        }
    }
  }
  </script>

<style scoped>
.head {
    margin: 0.5rem;
}
.text {
    margin: 1rem;
}
.todo {
    margin: 1rem;
    border-bottom: 1px solid #ccc;
}
</style>
