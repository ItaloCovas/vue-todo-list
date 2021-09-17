<template>
  <li>
    <span class="list-item">
      <input
        type="checkbox"
        :id="index"
        class="item-checkbox"
        v-model="item.checked"
      />
      <label :for="index" :class="getItemClass(item.checked)">
        {{ item.label }}
      </label>
    </span>
    <span v-html="deleteIcon" @click="deleteItem(index)"> </span>
  </li>
</template>

<script>
import feather from "feather-icons";

export default {
  name: "ListItem",
  props: {
    //Tudo que o componente precisa receber do comp. pai
    item: Object,
    index: Number,
  },
  computed: {
    deleteIcon() {
      return feather.icons.trash.toSvg({ width: 18 });
    },
  },
  methods: {
    getItemClass(itemChecked) {
      return itemChecked ? "item-checked" : "";
    },

    deleteItem(index) {
      this.$emit("delete-item", index);
    },
  },
};
</script>

<style scoped>
li,
.list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

li {
  width: 100%;
}

.item-checkbox {
  margin-right: 10px;
}

.item-checked {
  text-decoration: line-through;
}
</style>