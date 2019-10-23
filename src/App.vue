<template>
  <div id="app" class="container">
    <div class="todo-box">
      <div class="todo-header">
        <h2>To Do List</h2>
      </div>
      <div class="todo-form">
        <input
          type="text"
          class="form-control"
          @keypress="typing = true"
          placeholder="What do you want todo?"
          v-model="name"
          @keyup.enter="addTodo"
        />
        <small class="text-hint" v-show="typing">{{ name }}</small>
      </div>
      <div class="empty-task" v-if="todos.length < 1">
        <h3>Task Empty</h3>
        <small>You don't have task to do</small>
      </div>
      <div class="todo-list">
        <div class="todo-items" v-for="(data, key) in todos" :key="key">
          <div class="checkbox">
            <input
              type="checkbox"
              :id="`check-` + key"
              v-model="data.done"
              :checked="markAsCompleted()"
            />
          </div>
          <label
            :for="`check-` + key"
            class="todo-name"
            :class="{ 'is-done': data.done }"
          >
            {{ data.name }}
          </label>
          <a href="#" class="remove" @click="removeTodo(key)">delete</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      name: '',
      todos: []
    };
  },
  created() {
    this.todos = JSON.parse(localStorage.getItem('lists')) || [];
  },
  methods: {
    addTodo(event) {
      const text = event.target.value;
      this.todos.push({ name: text, done: false });
      localStorage.setItem('lists', JSON.stringify(this.todos));
      this.name = '';
    },
    removeTodo(key) {
      this.todos.splice(key, 1);
      localStorage.setItem('lists', JSON.stringify(this.todos));
    },
    markAsCompleted() {
      localStorage.setItem('lists', JSON.stringify(this.todos));
    }
  }
};
</script>

<style lang="scss">
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
body {
  font-family: 'Source Sans Pro', sans-serif;
  background: #f7f8fb !important;
  color: #333;
}
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  min-height: 100vh;
}
.todo-box {
  width: 35%;
  text-align: center;
}
.todo-form {
  width: 100%;
  display: block;
  height: 70px;
  input[type='text'] {
    padding: 5px 10px;
    display: block;
    margin: 0 auto;
    width: 100%;
    border: none;
    border-radius: 5px;
    height: 40px;
    box-shadow: 0 3px 7px -1px rgba(#000, 0.15);
  }
  .text-hint {
    color: #dc143c;
  }
}
.empty-task {
  display: block;
  text-align: center;
}
.todo-list {
  text-align: left;
  margin-top: 10px;
  background: #fff;
  width: 100%;
  border-radius: 5px;
  overflow: hidden;
  box-shadow: 0 2px 3px rgba(#000, 0.15);
  .todo-items {
    display: flex;
    align-items: center;
    border-bottom: 1px solid #f7f8fb;
    &:last-child {
      border-bottom: none;
    }
    .checkbox {
      background: #ccc;
      padding: 10px;
      input[type='checkbox'] {
        cursor: pointer;
        vertical-align: sub;
      }
    }
    .todo-name {
      padding: 0 10px;
      cursor: pointer;
      width: 100%;
    }
    .is-done {
      text-decoration: line-through;
      color: #aaa;
    }
    .remove {
      padding: 10px;
      background: #ccc;
      color: inherit;
      text-decoration: none;
      &:hover {
        color: #dc143c;
      }
    }
  }
}
</style>
