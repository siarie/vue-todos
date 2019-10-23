<template>
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
</template>

<script>
export default {
  data() {
    return {
      name: '',
      typing: false,
    }
  },
  methods: {
    addTodo(event) {
      const text = event.target.value
      this.todos.push({text, done: false, id: Date.now()})
      event.target.value = ''
    },
    refreshTodo() {
      this.$emit('refreshTodo')
    }
  }
};
</script>

<style lang="scss" scoped>
.todo-form {
  width: 100%;
  display: block;
  height: 70px;
}
input {
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
    color: #DC143C;
}
</style>
