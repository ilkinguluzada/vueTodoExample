<template>
  <div>
    <div id="error" style="display:none" class="alert alert-danger">
      Todo is empty!
    </div>

    <div class="form-group text-left">
      <input type="text" class="form-control" name="todo-input" placeholder="Add task" v-model="newTodo" @keyup.enter="addTodo">

      <ul class="list-group">
        <li v-if="!todo.editing" class="list-group-item todo-item" v-for="todo in todos" :key="todo.id">
          <span @dblclick="editTodoShow(todo.id - 1)">{{todo.title}}</span>
          <span class="badge"  @click="deleteTodo(todo.id - 1)">X</span>
        </li>

        <li v-else="todo.editing" class="list-group-item todo-item-edit">
          <input class="editInput" type="text" name="" v-model="todo.title" @keyup.enter="doneEdit(todo)" @blur="doneEdit(todo)" v-focus>
        </li>
      </ul>

    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  data () {
    return {
      newTodo: '',
      idNewTodo: 3,
      todos:[
        {
          "id":1,
          "title":"Finish Learning Vue",
          "completed": false,
          "editing":false,
        },
        {
          "id":2,
          "title":"Finish Learning Phyton",
          "completed": false,
          "editing":false,
        },
        {
          "id":3,
          "title":"Wrap up all",
          "completed": false,
          "editing":false,
        }
      ]
    }
    },
    directives: {
      focus: {
        inserted: function (el) {
          el.focus()
        }
      }
    },

    methods: {
      addTodo(){
        if (this.newTodo.trim() != 0) {
          this.todos.push({
            id: this.idNewTodo,
            title: this.newTodo,
            completed: false,
          });
          this.newTodo = '';
          this.idNewTodo++;

          var err = document.getElementById("error");
          err.style.display="none";
        }else{
          var err = document.getElementById("error");
          err.style.display="block";
        }
      },

      deleteTodo(id){
        this.todos.splice(id, 1)
      },

      editTodoShow(id){
        this.todos[id].editing = true;
      },
      doneEdit(todo){
        this.todos[todo.id-1].editing = false;
      }


  }
}
</script>


<style>
  .editInput{
    outline: none;
    margin: -10px;
    padding: 10px;
  }
</style>
