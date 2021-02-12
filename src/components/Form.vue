<template>
  <div>
    <form class="my-form">
      <div class="fields">
        <label>Title</label>
        <input
          type="text"
          name="title"
          placeholder="Title"
          @change="handleChange"
          :value="form.title"
        />

        <label>Description</label>
        <input
          type="text"
          name="description"
          placeholder="Descritption"
          @change="handleChange"
          :value="form.description"
        />

        <label>Price</label>
        <input
          type="number"
          min="0"
          name="price"
          placeholder="€ price"
          @change="handleChange"
          :value="form.price"
        />
        <div>
          <button class="save" @click="storeDish">Create</button>
          <button class="cancel" @click="toggleForm">Cancel</button>
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
    toggleForm() {
      this.$emit("toggleForm")
    }
  }
};
</script>
<style scoped>
*{
  outline: none;
}
.fields {
  display: flex;
  flex-direction: column;
  width: 12rem;
}
.save {
  background-color: green;
  color: white;
  border-radius: 10px;
  border-width: 0.5px;
  padding: 0.5em;
  width: 5em;
  margin: 0.5em;
}
.cancel {
  background-color:orangered;
  color: white;
  border-radius: 10px;
  border-width: 0.5px;
  padding: 0.5em;
  width: 5em;
  margin: 0.5em;
}
label {
  text-align: start;
  padding: 0.1em;
}
</style>
  
