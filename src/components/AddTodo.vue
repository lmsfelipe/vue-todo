 <template>
  <div>
    <form @submit="addTodo">
      <input v-model="title" type="text" name="title">
      <input type="submit" value="submit">
    </form>
  </div>
</template>

<script>
export default {
  name: 'AddTodo',
  data() {
    return {
      title: ''
    }
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        title: this.title,
        completed: false
      }
      this.$emit('add-todo', newTodo)
      this.title = ''
    }
  }
}
</script>

