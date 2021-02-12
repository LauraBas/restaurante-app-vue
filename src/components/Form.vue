<template>
  <div class="modal" :class="{ show: modal }">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h4 class="modal-title">Create</h4>
        </div>
        <div class="modal-body">
          <form @submit.prevent="storeDish()">
            <div class="modal-body">
              <div class="my-4">
                <label for="nombre">Title</label>
                <input
                  v-model="dish.title"
                  type="text"
                  class="form-control"
                  id="title"
                />
              </div>
              <div class="my-4">
                <label for="description">description</label>
                <input
                  v-model="dish.description"
                  type="text"
                  class="form-control"
                  id="description"
                />
              </div>
              <div class="my-4">
                <label for="price">price</label>
                <input
                  v-model="dish.price"
                  type="number"
                  min="0"
                  class="form-control"
                  id="price"
                />
              </div>
            </div>
            <div class="modal-footer">
              <button
                class="btn btn-warning"
                data-dismiss="modal"
                @click="closeModal()"
              >
                cancel
              </button>
              <button
                class="btn btn-success"
                data-dismiss="modal"
                type="submit"
              >
                save
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Form",
  props: {
    msg: String,
  },
};
</script>
