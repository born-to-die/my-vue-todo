<template>
    <b-form @submit="onSubmit">
        <div class="form row p-3">
            <div class="col-12 col-sm-9 mb-2">
                <b-form-input
                    v-model="todo.name"
                    placeholder="Наименование задачи"
                    type="text"
                    class="w-100 my-2"
                    required
                />
                <b-form-textarea
                    v-model="todo.text"
                    placeholder="Описание задачи"
                    rows="3"
                    max-rows="6"
                    class="w-100"
                    ></b-form-textarea>
            </div>
            <div class="col-12 col-sm mb-2">
                <b-button type="submit" variant="primary" class="w-100 my-2"> Добавить </b-button>
            </div>
        </div>
    </b-form>
</template>
  
  <script>
  export default {
    name: 'TodoForm',
    props: {
    },
    data() {
      return {
        todo: {
            name: '',
            text: '',
        }
      }
    },
    methods: {
        onSubmit() {
            this.$emit('add', this.todo);
        }
    }
  }
  </script>

