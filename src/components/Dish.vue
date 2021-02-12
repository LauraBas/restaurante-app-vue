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
      <button class="btn btn-success" @click="updateDish(dish.id)">Save</button>
    </span>
    <td
      v-on:click="activateInEditMode('description')"
      v-show="!isEditingDescription"
    >
      {{ dish.description }}
    </td>
    <span v-show="isEditingDescription">
      <input v-model="dish.description" type="text" class="form-control" />
      <button class="btn btn-warning" @click="deActivateInEditMode()">
        Cancel
      </button>
      <button class="btn btn-success" @click="updateDish(dish.id)">Save</button>
    </span>
    <td v-on:click="activateInEditMode('price')" v-show="!isEditingPrice">
      {{ dish.price }}
    </td>
    <span v-show="isEditingPrice">
      <input v-model="dish.price" type="number" class="form-control" />
      <button class="btn btn-warning" @click="deActivateInEditMode()">
        Cancel
      </button>
      <button class="btn btn-success" @click="updateDish(dish.id)">Save</button>
    </span>
  <td>
    <button class="mini ui red button" @click="onDelete">Delete</button>
  </td>
  </tr>
</template>

<script>
export default {
  name: "Dish",
  isEditingTitle: 0,
  isEditingDescription: 0,
  isEditingPrice: 0,
  dish: {
    title: "",
    description: "",
    price: 0,
  },
  props: {
    dish: {
      type: Object,
    },
  },
  methods: {

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
    onDelete() {
      this.$emit("onDelete", this.dish.id);
    },
    onEdit() {
      this.$emit("onEdit", this.dish);
    },
  },
};
</script>

<style scoped></style>
