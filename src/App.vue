<template>
  <div class="container-fluid col-centered todo-app">
    <center>
      <h1>
        <strong><i>ToDo List - FDI</i></strong>
      </h1>
    </center>
    <input class="form-control" v-model="newTodo" v-on:keyup.enter="addTodo(todo)">
    <h2>
      <i> ToDo </i>
    </h2>
    <ul class="list-group" v-show="todos.length">
      <li class="list-group-item list-group-item-info" v-for="todo in remaining">
        <span>{{ todo.task }}</span>
        <button class="btn btn-default" v-on:click="removeTask(todo)">
          <span class="glyphicon glyphicon-remove"></span>
        </button>
        <button class="btn btn-default" @click="completed(todo)">
          <span class="glyphicon glyphicon-ok"></span>
        </button>
      </li>
    </ul>
      <h2>
        <i> Complete </i>
      </h2>
      <ul class="list-group">
        <li class="list-group-item list-group-item-success" v-for="todo in complete">
          {{ todo.task }}
        </li>
      </ul>
    </div>
    <div class="json-output">
      <br/>
      <br/>
      <!-- <h4>JSON output:</h4>
        {{ $data | json }} -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: [{
        task: 'Test for ToDo unfinshed section',
        completed: false
      }, {
        task: 'Test for ToDo complete section',
        completed: true
      }]
    }
  },

  computed: {
    complete(todo) {
      return this.todos.filter(this.isCompleted);
    },

    remaining(todo) {
      return this.todos.filter(this.inProgress);
    }
  },

  methods: {
    isCompleted(todo) {
      return todo.completed;
    },

    inProgress(todo) {
      return ! this.isCompleted(todo);
    },

    addTodo(todo) {
      let text = this.newTodo.trim();
      this.todos.push({
        task: text,
        completed: false
      });
      this.newTodo = '';
    },

    removeTask(todo) {
      this.todos.$remove(todo);
    },

    completed(todo) {
      todo.completed = ! todo.completed;
    }
  }
}
</script>
