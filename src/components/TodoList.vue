<template>
    <div class="wrapper">
        <h1>
            {{ msg }}
        </h1>

        <div class="title">
            Please, enter list of todos
        </div>

        <div class="todosContainer">
            <TodoItem
                v-for="(item, index) in items"
                v-bind:key="item.id"
                v-bind="item"
                v-bind:index="index"
                v-on:delete-item="deleteItem($event)"
            />
        </div>

        <div class="inputContainer">
            <input
                v-model.trim="newItem"
                @keyup.enter="addItem"
                placeholder="Enter item"
            />

            <button
                v-on:click="addItem"
                class="addButton"
            >
                +
            </button>
        </div>
    </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  name: "TodoList",
  components: {
    TodoItem
  },
  props: {
    msg: String
  },
  data: function() {
    return {
      items: [
        { id: 0, text: "Wake up", finished: false },
        { id: 1, text: "Make breakfast", finished: false },
        { id: 2, text: "Go to work", finished: false }
      ],
      newItem: ""
    };
  },
  methods: {
    addItem: function() {
      if (!this.newItem) return;
      this.items.push({
        id: this.items.length ? this.items[this.items.length - 1].id + 1 : 0,
        text: this.newItem,
        finished: false
      });
      this.newItem = "";
    },
    deleteItem: function(id) {
      this.items = this.items.filter(item => item.id !== id);
    }
  }
};
</script>

<style scoped lang="scss">
h1 {
  padding: 20px 0;
  margin: 0;
  width: 100%;
  background-color: #c1e3f49c;
}
ol {
  display: inline-block;
}
li {
  text-align: left;
}
input {
  width: 160px;
  padding: 3px;
  border-radius: 3px;
  border: 1px solid #00000061;
}
.wrapper {
  border: 1px solid #0000001c;
  border-radius: 5px;
  width: 500px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: white;
}
.title {
  font-size: 18px;
  font-weight: 600;
  margin: 15px 0;
}
.todosContainer {
  margin-bottom: 15px;
}
.addButton {
  margin-left: 10px;
  outline: none;
  border: none;
  background-color: #205386;
  color: white;
  font-size: 24px;
  width: 30px;
  height: 30px;
  border-radius: 50px;
  cursor: pointer;
}
.addButton:hover {
  background-color: #193f65;
}
.addButton:active {
  background-color: white;
  border: 1px solid #205386;
  color: #205386;
  font-weight: 700;
}
.inputContainer {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}
</style>
