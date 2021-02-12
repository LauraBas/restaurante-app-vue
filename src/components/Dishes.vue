<template>
  <div class="container">
    <Form :form="form" @storeDish="storeDish" />
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
      this.getDishes();
    },
    async onUpdate(id) {
      await ApiClient.updateDishApi(id);
    }
  }
};
</script>

<style>
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
</style>
