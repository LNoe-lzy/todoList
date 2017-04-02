<template>
  <section class="wrapper">
    <header class="add">
      <input placeholder="what needs to be done"
             @keyup.enter="addTodo"
             v-model="newTodo" />
    </header>
    <section>
      <div v-for="(list, index) in filterTodos" class="list-item">
        <input type="checkbox" class="item" v-model="list.completed" />
        <label :class="{completed: list.completed}">{{list.todo}}</label>
        <span class="close" @click="removeTodo(index)"></span>
      </div>
    </section>
    <footer v-show="todoList.length">
      <button :class="{actived: visiblity === 'all'}" @click="handleVisiblity('all')">all</button>
      <button :class="{actived: visiblity === 'actived'}" @click="handleVisiblity('actived')">actived</button>
      <button :class="{actived: visiblity === 'completed'}" @click="handleVisiblity('completed')">completed</button>
    </footer>
  </section>
</template>

<script>

let filter = {
  'all': function (todos) {
    return todos
  },
  'completed': function (todos) {
    return todos.filter(function (todo) {
      return todo.completed
    })
  },
  'actived': function (todos) {
    return todos.filter(function (todo) {
      return !todo.completed
    })
  }
}

export default {
  data () {
    return {
      newTodo: '',
      todoList: [],
      visiblity: 'all'
    }
  },
  methods: {
    addTodo () {
      this.todoList.push({
        todo: this.newTodo,
        completed: false
      })
      this.newTodo = ''
    },
    handleVisiblity (type) {
      this.visiblity = type
    },
    removeTodo (index) {
      this.todoList.splice(index, 1)
    }
  },
  computed: {
    filterTodos () {
      return filter[this.visiblity](this.todoList)
    }
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
ul {
  list-style: none;
}

.wrapper
  display: flex
  flex-direction: column
  .add
    width: 100%
    input
      width: 100%
      box-sizing: border-box
      padding: 10px 0 10px 45px
      font-size: 24px
      border: solid 1px #ededed
      font-weight: 100
  section
    display: flex
    flex-direction: column
    .list-item
      width: 100%
      box-sizing: border-box
      padding: 10px 10px
      font-size: 24px
      border-bottom: solid 1px #ededed
      border-left: solid 1px #ededed
      border-right: solid 1px #ededed
      display: flex
      align-items: center
      position: relative
      .item
        -webkit-appearance: none
        position: relative
        width: 24px
        height: 24px
        outline: none
        &::after
          content: ''
          width: 24px
          height: 24px
          display: inline-block
          background: url('../assets/checkbox_no.png')
          background-size: cover
        &:checked::after
          content: ''
          width: 24px
          height: 24px
          display: inline-block
          background: url('../assets/checkbox_on.png')
          background-size: cover
      label
        margin-left: 10px
        font-weight: 100
      .close
        display: block
        width: 24px
        height: 24px
        background: url('../assets/close.png')
        background-size: cover
        cursor: pointer
        position: absolute
        right: 20px
      .completed
        color: #ededed
        text-decoration: line-through
  footer
    padding: 12px 0
    box-sizing: border-box
    border-left: solid 1px #ededed
    border-right: solid 1px #ededed
    border-bottom: solid 1px #ededed
    display: flex
    justify-content: center
    button
      padding: 5px
      background: none
      border: none
      outline: none
      cursor: pointer
      border: 1px solid #ededed
      border-radius: 5px
      margin-right: 15px
    .actived
      border: 1px solid #F4606C
</style>
