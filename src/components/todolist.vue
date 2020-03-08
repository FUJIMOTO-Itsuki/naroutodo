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
    <div>Done<button @click="deleteDone">まとめて削除</button></div>
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
        { name: "ToDoリストを作る", done: false },
        { name: "もふもふする", done: true }
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
    },
    deleteDone() {
      for (let i = 0; i < this.items.length; i++) {
        if (this.items[i].done) {
          this.items.splice(i, 1);
          i--;
        }
      }
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
