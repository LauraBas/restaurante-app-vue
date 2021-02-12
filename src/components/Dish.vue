<template>
  <tr>
    <th scope="row">{{ dish.id }}</th>
    <td v-on:click="activateInEditMode('title')" v-show="!isEditingTitle">{{ dish.title }}</td>
    <span v-show="isEditingTitle">
      <input v-model="dish.title" type="text" class="form-control" />
      <button class="save" @click="onUpdate">Save</button>
      <button class="cancel" @click="deActivateInEditMode()">Cancel</button>
    </span>
    <td
      v-on:click="activateInEditMode('description')"
      v-show="!isEditingDescription"
    >{{ dish.description }}</td>
    <span v-show="isEditingDescription">
      <input v-model="dish.description" type="text" class="form-control" />
      <button class="save" @click="onUpdate">Save</button>
      <button class="cancel" @click="deActivateInEditMode()">Cancel</button>
    </span>

    <td v-on:click="activateInEditMode('price')" v-show="!isEditingPrice">{{ dish.price }}</td>
    <span v-show="isEditingPrice">
      <input v-model="dish.price" type="number" class="form-control" />
      <button class="save" @click="onUpdate">Save</button>
      <button class="cancel" @click="deActivateInEditMode()">Cancel</button>
    </span>
    <td>
      <button class="delete" @click="onDelete">Delete</button>
    </td>
  </tr>
</template>

<script>
export default {
  name: "Dish",
  props: {
    dish: {
      type: Object
    }
  },
  data() {
    return {
      isEditingTitle: 0,
      isEditingDescription: 0,
      isEditingPrice: 0
    };
  },
  methods: {
    onDelete() {
      this.$emit("onDelete", this.dish.id);
    },
    onUpdate() {
      this.deActivateInEditMode();
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
    }
  }
};
</script>

<style scoped>
.cancel{
  background-color: crimson;
  color:white;
  border-radius: 10px;
  border-width: 0.5px;
}
.save{
  background-color: green;
  color:white;
  border-radius: 10px;
  border-width: 0.5px;
}
.delete{
  background-color: blue;
  color:white;
  border-radius: 10px;
  border-width: 0.5px;
}
.form-control{
  border:none;
}
</style>
