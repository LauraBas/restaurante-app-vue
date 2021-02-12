<template>
  <div class="my-form">
    <form class="ui form">
      <div class="fields">
        <div class="four wide field">
          <label>Title</label>
          <input
            type="text"
            name="title"
            placeholder="Title"
            @change="handleChange"
            :value="form.title"
          />
        </div>

        <div class="four wide field">
          <label>Description</label>
          <input
            type="text"
            name="description"
            placeholder="Descritption"
            @change="handleChange"
            :value="form.description"
          />
        </div>

        <div class="six wide field">
          <label>Price</label>
          <input
            type="number"
            min=0
            name="price"
            placeholder="€ price"
            @change="handleChange"
            :value="form.price"
          />
        </div>

        <div class="two wide field">
          <button class="ui orange button submit-button"  @click="storeDish">
            Create
          </button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "Form",
  props: {
    form: {
      type: Object
    }
  },
  methods: {
    handleChange(event) {
      const { name, value } = event.target;
      let form = this.form;
      form[name] = value;
      this.form = form;
    },
    storeDish(event) {     
      event.preventDefault();
      if (this.formValidation()) {
        this.$emit("storeDish", this.form);
        this.clearFormFields();
      }
    },
    formValidation() {
      if (document.getElementsByName("title")[0].value === "") {
        alert("Field  Required");
        return false;
      }
  
      if (document.getElementsByName("description")[0].value === "") {
        alert("Field  Required");
        return false;
      }

      if (document.getElementsByName("price")[0].value === "") {
         alert("Field  Required");
        return false;
      }
      return true;
    },
    clearFormFields() {
     
      this.form.title = "";
      this.form.description = "";
      this.form.price = "";
      document.querySelector(".form").reset();
    }
  },
};
</script>

<style scoped></style>
  
