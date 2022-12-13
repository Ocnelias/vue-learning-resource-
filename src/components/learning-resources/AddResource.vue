<template>
  <base-dialog v-if="inputIsInvalid" title="invalid input" @close="confirmError">
    <template #default>
      invalid value
    </template>
    <template #actions>
      <base-button @click="confirmError"> ok </base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <input type="text" name="title" ref="titleInput" />
      </div>
      <div class="form-control">
        <textarea name="description" ref="descriptionInput"> </textarea>
      </div>
      <div class="form-control">
        <input type="link" name="link" ref="linkInput" />
      </div>
      <div class="form-control">
        <base-button type="submit"> submitData </base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  inject: ['addResource'],
  data() {
    return {
      inputIsInvalid: false,
    };
  },
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descriptionInput.value;
      const enteredLink = this.$refs.linkInput.value;
      if (enteredTitle.trim() === '') {
        this.inputIsInvalid = !this.inputIsInvalid;
        return;
      } else {
        this.addResource(enteredTitle, enteredDescription, enteredLink);
        this.inputIsInvalid = false;
      }
    },
    confirmError(){
      this.inputIsInvalid = false;
    }
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
