<template>
  <div class="container">
    <div>
      <h3 class="text-center">All Dishes</h3>
      <br />

      <b-table-simple hover small caption-top responsive>
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
              @onEdit="onEdit"
            />
        </tbody>
      </b-table-simple>
    </div>
  </div>
</template>

<script>
import ApiClient from "../services/ApiClient.js";
import Dish from "./Dish";
export default {
  name: "Dishes",
  components: {
    Dish
  },
  props: {
    dishes: {
      type: Array
    },
  },
  data() {
    return {
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
    async storeDish() {
      const dish = this.dish;
      await ApiClient.storeDishApi(dish);
      this.closeModal();
      this.getDishes();
    },
    async updateDish(id) {
      await ApiClient.updateDishApi(id);
      this.deActivateInEditMode();
    },
  },
};
 
</script>

<style>
.show {
  display: list-item;
  opacity: 1;
  background: rgba(75, 56, 143, 0.705);
}
.modal {
  padding: 10px;
}
.my-4 {
  padding: 5px;
}
</style>
