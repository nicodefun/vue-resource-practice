<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="closeDialog">
    <template #default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <p>Pls check all inputs, and enter at least a few characters into each input field.</p>
    </template>
    <template v-slot:actions>
      <base-button @click="closeDialog">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitForm">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" id="title" name="title" v-model="inputTitle" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          name="description"
          id="description"
          rows="3"
          v-model="textArea"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">link</label>
        <input name="link" id="link" type="url" v-model="url" />
      </div>
      <div>
        <base-button type="submit">Add Resources</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
export default {
  data() {
    return {
      inputTitle: '',
      textArea: '',
      url: '',
      inputIsInvalid: false
    };
  },
  inject: ['addResource'],
  methods: {
    submitForm() {
      if (
        this.inputTitle.trim() === '' ||
        this.textArea.trim() === '' ||
        this.url.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }
      //provide from TheResource
      this.addResource(this.inputTitle, this.textArea, this.url);
    },
    closeDialog(){
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
  border-color: darkcyan;
  background-color: rgb(231, 237, 237);
}

.form-control {
  margin: 1rem 0;
}
</style>
