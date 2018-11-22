<template>
    <div class="container">
        <div>
            <input
                type="checkbox"
                v-bind:id="id"
                v-model="isFinished"
            />

            <label
                v-bind:for="id"
                v-bind:class="{ crossedOutText: isFinished }"
            >
                {{ text }}
            </label>
        </div>

        <button v-on:click="$emit('delete-item', id)">
            x
        </button>
    </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    text: String,
    id: Number,
    finished: Boolean
  },
  data: function() {
    return {
      isFinished: this.finished
    };
  }
};
</script>

<style scoped lang="scss">
.container {
  display: flex;
  justify-content: space-between;
  background-color: #302cd036;
  padding: 5px;
  margin-bottom: 5px;
  width: 200px;
}
button {
  border: none;
  outline: none;
  background-color: transparent;
  cursor: pointer;
  width: 20px;
}
button:active {
  font-weight: 700;
}
.crossedOutText {
  text-decoration-line: line-through;
}
</style>
