<template>
  <tr>
    <th scope="row">{{ dish.id }}</th>
    <td v-on:click="toggleEditMode('title')" v-show="!isEditingTitle">{{ dish.title }}</td>
    <span v-show="isEditingTitle">
      <div class="input-btn">
        <input v-model="dish.title" type="text" class="form-control" />
        <button class="btn btn-success" @click="onUpdate('title')">Save</button>
        <button class="btn btn-warning" @click="toggleEditMode('title')">cancel</button>
      </div>
    </span>
    <td v-on:click="toggleEditMode('description')" v-show="!isEditingDescription">{{ dish.description }}</td>
      <span v-show="isEditingDescription">
        <div class="input-btn">
          <input v-model="dish.description" type="text" class="form-control" />
          <button class="btn btn-success" @click="onUpdate('description')">Save</button>
          <button class="btn btn-warning" @click="toggleEditMode('description')">cancel</button>
        </div>  
      </span>    
    <td v-on:click="toggleEditMode('price')" v-show="!isEditingPrice">{{ dish.price }}</td>
    <span v-show="isEditingPrice">
      <div class="input-btn">
        <input v-model="dish.price" type="number" class="form-control" />
        <button class="btn btn-success" @click="onUpdate('price')">Save</button>
        <button class="btn btn-warning" @click="toggleEditMode('price')">cancel</button>
      </div>
    </span>
    <td>
      <button class="btn btn-danger" @click="onDelete">Delete</button>
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
    onUpdate(name) {
      this.toggleEditMode(name)
      this.$emit("onUpdate", this.dish.id);
    },

    toggleEditMode(name) {
      if (name == "title") {
        this.isEditingTitle = !this.isEditingTitle;
      }
      if (name == "description") {
        this.isEditingDescription = !this.isEditingDescription;
      }
      if (name == "price") {
        this.isEditingPrice = !this.isEditingPrice;
      }
    },
  }
};
</script>

<style scoped>
*{
  outline: none;
}
.input-btn{
  display:flex
}
.form-control{
  border:none;
}
.btn{
  margin:2px;
}
</style>
