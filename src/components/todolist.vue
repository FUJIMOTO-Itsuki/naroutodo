<template>
  <div>
    <div>TodoList</div>
    <div>
      ToDo<label>
        タスク名
        <input type="text" v-model="newItem.name" />
      </label>

      <button @click="addItem" v-bind:disabled="isNameEmpty">追加！</button>
    </div>
    <div v-for="(item, index) in items" :key="item.name">
      <div class="item" v-if="!item.done">
        <div class="name">
          名前: {{ item.name }}
          <button @click="switchDone(index)">完了した！</button>
          <button @click="deleteItem(index)">削除</button>
        </div>
      </div>
    </div>
    <div>Done</div>
    <div v-for="(item, index) in items" :key="item.name">
      <div class="item" v-if="item.done">
        <div class="name">
          名前: {{ item.name }}
          <button @click="switchDone(index)">実は未完…</button>
          <button @click="deleteItem(index)">削除</button>
        </div>
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
    },
    switchDone(index) {
      this.items[index].done = !this.items[index].done;
    },
    deleteItem(index) {
      this.items.splice(index, 1);
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
