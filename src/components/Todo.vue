<template>
  <div class="hello">
    <h1>To-do Application</h1>
    <input v-model="text" type="text">
    <button @click="addTodo">Add</button>
    
    <ul>
      <li v-for="(item, index) in todos" :key="item.id">
        <p :class="{ 'todo-completed': item.completed }">
          <input :value="item.completed" @change="updateCompleted(index)" type="checkbox">
          <span>{{ item.text }}</span>
          <button @click="delTodo(index)">x</button>
        </p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      todos: [],
      text: ''
    }
  },
  created () {
    const demo_user_token = '545144f656d88e8a29b272883442aa48397aa19ad22734ae5516e3f4	';
    /* App ID used to create a user token. */
    const demo_appid = 'web';

    const api = new Mesibo();

    api.setListener(new MesiboListener());
    api.setAppName(demo_app_id);
    api.setCredentials(demo_user_token);
    api.setDatabase("mesibo");

    api.start();
  },
  methods: {
    updateCompleted (index) {
      this.todos.splice(index, 1, {
        id: this.todos[index].id,
        text: this.todos[index].text,
        completed: !this.todos[index].completed
      })
    },
    addTodo () {
      this.todos.push({
        id: Date.now(),
        text: this.text,
        completed: false
      })
      this.text = ''
    },
    delTodo (index) {
      this.todos.splice(index, 1)
    }
  }
}
</script>
<style scoped>
.todo-completed {
  text-decoration: line-through;
  color: #757575;
}
</style>
