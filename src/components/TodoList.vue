<template>
  <div>
    <h3><p class="tasks">Ukonczone zadania:
    {{todos.filter(todo => {return todo.done === true}).length}}</p></h3>
    <h4><p class="tasks">Nieukonczone zadania:
    {{todos.filter(todo => {return todo.done === false}).length}}</p></h4>
    <todo v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo"
    v-for="todo in todos" :todo.sync="todo" v-bind:todo="todo"></todo>
  </div>
</template>

<script type = "text/javascript" >
import sweetalert from 'sweetalert';
import Todo from './Todo';

export default {
  props: ['todos'],
  components: {
    Todo,
  },
  methods: {
    deleteTodo(todo) {
      sweetalert({
        title: 'Are you sure?',
        text: 'This To-Do will be permanently deleted!',
        type: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#DD6B55',
        confirmButtonText: 'Yes, delete it!',
        closeOnConfirm: false,
      },
      () => {
        const todoIndex = this.todos.indexOf(todo);
        this.todos.splice(todoIndex, 1);
        sweetalert('Deleted!', 'Your To-Do has been deleted.', 'success');
      });
    },

    completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
      sweetalert('Sukces!', 'Zadanko ukonczone!', 'success');
    },
  },
};
</script>

<style scoped>
p.tasks {
  text-align: center;
}

h3{
  color:#12d11c;
}

h4{
  color:#cc2645;
}
</style>
