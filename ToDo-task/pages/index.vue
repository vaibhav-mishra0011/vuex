<template>
  <v-layout row justify-center>
    <v-btn class="mx-auto" height="50px" @click.native.stop="dialog = true">
      Add To Do
    </v-btn>
    <v-dialog v-model="addTodoDialog" max-width="290">
      <v-card>
        <v-card-title>Add a To Do Task</v-card-title>
        <v-text-field v-model="todoTitle" label="Type here"></v-text-field>
        <v-text-field
          class="label-set"
          height="50px"
          v-model="todoCompleted"
          type="checkbox"
          label="Mark as completed"
        ></v-text-field>

        <v-card-actions>
          <v-btn @click="addToDo" :disabled="!todoTitle">Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <div class="card">
      <div class="card-inner">
        <ul class="list">
          <ul class="mx-5px"  v-for="(todo,todoIndex) in todos" :key="todo.id">
            <to-do :toDo="todo" :toDoIndexValue="todoIndex" @delete="deleteTodo" @edit="handleEdit" />
          </ul>
        </ul>
      </div>
    </div>
  </v-layout>
</template>

<script>

export default {
  data() {
    return {
      addTodoDialog: false,
      todos: [
        { id: 1, name: "aa", todoCompleted: false },
        { id: 2, name: "bb", todoCompleted: false },
      ],
      todoTitle: null,
      toDotoEdit: false,
    };
  },
  methods: {
    addToDo() {
      if (this.toDotoEdit) {
        this.editTodo();
      } else {
        this.todos.push({
          id: this.todos.length + 1,
          name: this.todoTitle,
          todoCompleted: false
        });
        this.openPopUp();
        this.resetAddview();
      }
    },

    editTodo() {
      this.todos.forEach((todo, todoIndex) => {
        if (todo.id === this.toDotoEdit.id) {
          this.toDotoEdit.name = this.todoTitle;
          this.todos[todoIndex] = this.toDotoEdit;
        }
      });

      this.resetAddview();
    },
    resetAddview() {
      this.todoTitle = "";
      this.todoCompleted = false;
      this.addTodoDialog = false;
    },

    deleteTodo(todoId) {
      //this.todos = this.todos.filter((todo) => todo.id !== todoId);
      const todoDeleteIndex = this.todos.findIndex((todo) => todo.id === todoId);
      this.todos.splice(todoDeleteIndex, 1);
    },

    handleEdit(toDo) {
      this.todoTitle = toDo.name;
      this.addTodoDialog = true;
      this.toDotoEdit = toDo;
    },

    openPopUp(){
      alert("Your Task has been added")
    }
    
  },
  
};
</script>













