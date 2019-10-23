<template>
  <div class="todo-list">
    <div class="todo-items" v-for="(data, key) in todos" :key="key">
      <div class="checkbox">
        <input type="checkbox" :id="`check-` + data.id" v-model="data.done" />
      </div>
      <label :for="`check-` + data.id" class="todo-name" :class="{ 'is-done': data.done }">
          {{ data.name }}
      </label>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [
        {id: 1, name: "Go to School?", done: true},
        {id: 2, name: "Dinner with yui at 8 p.m", done: false},
      ],
      // checked: this.todos.done
    }
  }
}
</script>

<style lang="scss">
input[type="checkbox"] {
    cursor: pointer;
}

.todo-list {
  text-align: left;
  margin-top: 10px;
  background: #fff;
  width: 100%;
  border-radius: 5px;
  overflow: hidden;
  box-shadow: 0 2px 3px rgba(#000, 0.15);
}

.todo-items {
  display: flex;
  align-items: center;
  border-bottom: 1px solid #f7f8fb;
  &:last-child {
    border-bottom: none;
  }
  .checkbox {
      display: flex;
      background: #CCC;
      padding: 10px;
  }
  .todo-name {
      padding: 0 10px;
      cursor: pointer;
      width: 100%;
  }
  .is-done {
    text-decoration: underline;
    text-decoration-line: line-through;
    color: #444;
  }
}
</style>
