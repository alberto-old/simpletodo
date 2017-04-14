<template>
  <div id="main">
    <nav class="pa3 pa4-ns">
      <a class="link dim black b f1 f-headline-ns tc db mb3 mb4-ns" href="#" title="Home">Simple Todo</a>
      <div class="tc pb3">
        <a class="link dim gray f6 f5-ns dib mr3" href="/" title="Home"><strong>Home</strong></a>
        <a class="link dim gray f6 f5-ns dib mr3" href="/active" title="Active">Active</a>
        <a class="link dim gray f6 f5-ns dib mr3" href="/completed" title="Completed">Completed</a>
      </div>
    </nav>
    <form class="pa3 pa5-ns" @submit.prevent="add(task)" >
      <input v-model="task" type="text">
      <input type="submit" value="Add">
    </form>
    <article class="pa3 pa5-ns">
      <h1 class="f4 bold center mw6">Todos</h1>
      <ul class="list pl0 ml0 center mw6 ba b--light-silver br2">
        <li v-for="todo of todos" class="flex items-center ph3 pv3 bb b--light-silver">
          <span v-bind:class="{strike: todo.complete}" class="flex-auto">{{todo.id}} {{todo.task}}</span>
          <button @click="toggle(todo)"><img src="https://icon.now.sh/check"/></button>
          <button @click="remove(todo)"><img src="https://icon.now.sh/trash"/></button>
        </li>
      </ul>
    </article>
  </div>
</template>

<script>
  import { mapState, mapActions } from 'vuex'
  import axios from 'axios'

  export default {
    data () {
      return {
        task: 'add new task'
      }
    },
    async created () {
      const res = await axios.get('https://todos-cuvsmolowg.now.sh/todos')
      this.$store.commit('init', res.data)
    },
    computed: {
      ...mapState({
        todos: state => state.todos
      })
    },
    methods: {
      ...mapActions([
        'add',
        'remove',
        'toggle'
      ])
    }
  }
</script>
