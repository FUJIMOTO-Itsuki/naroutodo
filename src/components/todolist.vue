<template>
  <div>
    <div><h2>TodoList</h2></div>
    <div>
      <h3>
        ToDo
        <label>
          <input type="text" v-model="newItem.name" />
        </label>

        <button @click="addItem" v-bind:disabled="isNameEmpty">追加！</button>
      </h3>
    </div>
    <div v-for="item in todoItems" :key="item.name">
      <div class="item" v-if="!item.done">
        <div class="name">
          名前: {{ item.name }}
          <button @click="switchDone(item.id)">完了した！</button>
          <button @click="deleteItem(item.id)">削除</button>
        </div>
      </div>
    </div>
    <div>
      <h3>Done <button @click="deleteDone">まとめて削除</button></h3>
    </div>
    <div v-for="item in doneItems" :key="item.name">
      <div class="item" v-if="item.done">
        <div class="name">
          名前: {{ item.name }}
          <button @click="switchDone(item.id)">実は未完…</button>
          <button @click="deleteItem(item.id)">削除</button>
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
        { name: "ToDoリストを作る", done: true, id: 0 },
        { name: "もふもふする", done: false, id: 1 }
      ],
      nextId: 2,
      newItem: { name: "", done: false, id: 2 }
    };
  },
  methods: {
    addItem() {
      this.items.push(this.newItem);
      this.nextId++;
      this.newItem = { name: "", done: false, id: this.nextId };
    },
    findItemIndex(id) {
      for (let i = 0; i < this.items.length; i++) {
        if (this.items[i].id == id) {
          return i;
        }
      }
    },
    switchDone(id) {
      let index = this.findItemIndex(id);
      this.items[index].done = !this.items[index].done;
    },
    deleteItem(id) {
      let index = this.findItemIndex(id);
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
    },
    todoItems() {
      let todos = [];
      for (let i = 0; i < this.items.length; i++) {
        if (!this.items[i].done) {
          todos.push(this.items[i]);
        }
      }
      return todos;
    },
    doneItems() {
      let dones = [];
      for (let i = 0; i < this.items.length; i++) {
        if (this.items[i].done) {
          dones.push(this.items[i]);
        }
      }
      return dones;
    }
  }
};
</script>

<style></style>
