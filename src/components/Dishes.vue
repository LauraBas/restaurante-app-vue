<template>
  <div class="container">
    <button class="add" @click="toggleForm" v-show="!createMode">Add</button>
    <Form v-show="createMode" 
    :form="form" 
    @storeDish="storeDish"
    @toggleForm="toggleForm" />
    <div>
      <table>
        <thead>
          <tr>
            <th>Id</th>
            <th>Title</th>
            <th>Description</th>
            <th>Price</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <Dish
            v-for="dish in dishes.data"
            :key="dish.id"
            :dish="dish"
            @onDelete="onDelete"
            @onUpdate="onUpdate"
          />
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import ApiClient from "../services/ApiClient.js";
import Dish from "./Dish";
import Form from "./Form.vue";

export default {
  name: "Dishes",
  components: {
    Dish,
    Form
  },
  data() {
    return {
      dishes: {
        type: Array
      },
      createMode: false,
      form: {
        title: "",
        description: "",
        price: ""
      }
    };
  },

  created() {
    this.getDishes();
  },
  methods: {
    async getDishes() {
      const res = await ApiClient.getDishApi();
      this.dishes = res.data;
    },
    async onDelete(id) {
      await ApiClient.deleteDishApi(id);
      this.getDishes();
    },
    async storeDish(dish) {
      await ApiClient.storeDishApi(dish);
      this.toggleForm();
      this.getDishes();
    },
    async onUpdate(id) {
      await ApiClient.updateDishApi(id);
    },
    toggleForm(){
      this.createMode = !this.createMode;
    }
  }
};
</script>

<style>
*{
  outline: none;
}
table {
  margin: 1rem;
  border-collapse: collapse;  
}
table td {
  padding: 0.5rem;
  border: 1px solid orange;
}
table th {
  padding: 0.5rem;
  border: 1px solid ForestGreen;
}
.add{
  background-color: yellow;
  border-radius: 10px;
  border-width: 0.5px;
  padding: 0.5em;
  width: 5em;
  margin: 0.5em;
}
</style>
