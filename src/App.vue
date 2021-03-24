<template>
   <div class="container"> 
     <h1 class="first-list">
       My To Do List!
   </h1>

    <md-list>
      <md-list-item class="individual" v-for="(list, index) in todos" :key="list.id" @dblclick="editLabel(index)" >
        <input type="checkbox" @click="checked(index)" >
        <div :class="{editing: isSet != list.edit, complete: isComplete == list.completed}">
          {{ list.label}}
        </div>    
        <input :class="{editing: isSet == list.edit }" v-model="list.label" @keydown.enter="change(index)" >
        <button class="button" value="button" @click="removeTodo(list)">X</button>
      </md-list-item>

    <md-field >
      <md-input class="input" v-model="currentTodo" @keydown.enter="addTodo()" placeholder="Add a thing to do" ></md-input>
    </md-field>
    </md-list> 
  </div>
</template>

<script>
export default {
  data() {
    return {
      isComplete: true,
      isSet: false,
      todos: [],
      currentTodo: '',
    };
  },
  methods: {
    addTodo() {
      this.todos.push({id: this.todos.length, edit: false, completed: false, label: this.currentTodo,});
      this.currentTodo = '';
    },
    editLabel(index) {
      this.todos[index].edit = true;
      console.log("boop")
    },
    removeTodo(list) {
      console.log(this.todos); 
      var index = this.todos.indexOf(list); 
      console.log(index);
      this.todos.splice(index, 1);
    },
    change(index) {
      this.todos[index].edit = false;
    },
    checked(index) {
      console.log("check")
      this.todos[index].completed = !this.todos[index].completed
    }
  }
  };
</script>

<style>

.container {
  margin: auto;
  width: 42%;
  text-align: center;
  padding: 10px;
  background: white;
  border: 3px solid green;
}

.input {
color: blue;
text-align: center;
border: 3px solid black;
}

.title{
  color: blue;
margin: auto;
text-align: center;
}



.first-list {
  color: blue;
  margin: auto;
  padding: 5px;

}

.button {
  background: black;
  color: rgb(205, 205, 243);
}

.list-item {
margin: auto;
border: 3px dotted black;
color: blue;
}

.individual {
  display: flex;
  margin: auto;
  border: 3px solid black;
  margin: 3px;
  padding: 3px;
  
}

.complete {
  text-decoration: line-through;
}

.editing {
  display: none;
}

</style>