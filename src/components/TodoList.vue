<template>
  <div class="todo-list">
    <h3>Todo List</h3>
    <input type="text" class="input-new-item" v-on:keyup.enter="addNewItem" />

    <ul>
      <ListItem
        v-for="(item, index) in list"
        :key="index"
        :item="item"
        :index="index"
        @delete-item="deleteItem"
      />
    </ul>
  </div>
</template>

<script>
import ListItem from "./ListItem";

export default {
  name: "TodoList",
  components: {
    ListItem,
  },
  data() {
    return {
      list: [],
    };
  },
  created() {
    const localStorageItems = JSON.parse(localStorage.getItem("list")); // Verifica no created o que tem no localStorage
    this.list = localStorageItems ? localStorageItems : [];
  },
  methods: {
    addNewItem(event) {
      const newItem = event.target.value;
      this.list.unshift({
        label: newItem,
        checked: false,
      });

      event.target.value = "";
    },

    deleteItem(index) {
      this.list.splice(index, 1);
    },

    updateLocalStorage() {
      localStorage.setItem("list", JSON.stringify(this.list));
    },
  },
  watch: {
    list() {
      this.updateLocalStorage();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo-list {
  width: 500px;
  margin: 0 auto;
}

.input-new-item {
  width: 80%;
  height: 30px;
}

ul {
  list-style: none;
  padding: 0;
  width: 80%;
  margin: 20px auto;
  text-align: left;
}
</style>
