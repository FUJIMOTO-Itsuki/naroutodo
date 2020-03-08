<template>
  <div>
    <div>TodoList</div>
    <div>ToDo</div>
    <div v-for="item in items" :key="item.name">
      <div class="item">
        <div class="name" v-if="!item.done">名前: {{ item.name }}</div>
      </div>
    </div>
    <div>
      <label>
        名前
        <input type="text" v-model="newItem.name" />
      </label>

      <button @click="addItem" v-bind:disabled="isNameEmpty">add</button>
    </div>
    <div>Done</div>
    <div v-for="item in items" :key="item.name">
      <div class="item">
        <div class="name" v-if="item.done">名前: {{ item.name }}</div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "TodoList",
  data() {
    return {
      items: [
        { name: "りんご", done: false },
        { name: "たまご", done: true }
      ],
      newItem: { name: "", done: false }
    };
  },
  methods: {
    addItem() {
      this.items.push(this.newItem);
      this.newItem = { name: "", done: false };
    }
  },
  computed: {
    isNameEmpty() {
      return this.newItem.name == "";
    }
  }
};
</script>

<style></style>
