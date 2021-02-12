<template>
  <tr>
    <th scope="row">{{ dish.id }}</th>
    <td v-on:click="activateInEditMode('title')" v-show="!isEditingTitle">
      {{ dish.title }}
    </td>
    <span v-show="isEditingTitle">
      <input v-model="dish.title" type="text" class="form-control" />
      <button class="btn btn-warning" @click="deActivateInEditMode()">
        Cancel
      </button>
      <button class="btn btn-success" @click="onUpdate">Save</button>
    </span>
    <td>{{ dish.description }}</td>
    <td>{{ dish.price }}</td>
    <td>
      <button class="mini ui red button" @click="onDelete">Delete</button>
    </td>
  </tr>
</template>

<script>
export default {
  name: "Dish",
  props: {
    dish: {
      type: Object,
    },
  },
  data() {
    return {
      isEditingTitle: 0,
      isEditingDescription: 0,
      isEditingPrice: 0,
    };
  },
  methods: {
    onDelete() {
      this.$emit("onDelete", this.dish.id);
    },
    onUpdate() {
      this.deActivateInEditMode()
      this.$emit("onUpdate", this.dish.id);
    },

    activateInEditMode(name) {
      if (name == "title") {
        this.isEditingTitle = true;
      }
      if (name == "description") {
        this.isEditingDescription = true;
      }
      if (name == "price") {
        this.isEditingPrice = true;
      }
    },
    deActivateInEditMode() {
      this.isEditingTitle = false;
      this.isEditingDescription = false;
      this.isEditingPrice = false;
    },
  },
};
</script>

<style scoped>
</style>
