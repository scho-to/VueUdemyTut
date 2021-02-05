<template>
  <teleport to="body">
    <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="closeModal">
      <template #default>
        <p>
          At least one input is not valid.
        </p>
        <p>
          please make sure, that every input is filled.
        </p>
      </template>
      <template #actions>
        <base-button @click="closeModal">Okay</base-button>
      </template>
    </base-dialog>
  </teleport>
  <base-card>
    <form action="" @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" id="title" name="title" ref="titleInput">
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea name="" id="description" cols="30" rows="10" ref="descInput"></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input type="url" id="link" name="link" ref="linkInput">
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
  export default {
    inject: ["addResource"],
    data(){
      return {
        inputIsInvalid: false
      }
    },
    methods: {
      submitData(){
        const title = this.$refs.titleInput.value;
        const desc = this.$refs.descInput.value;
        const link = this.$refs.linkInput.value;
        
        if(title.trim() === '' ||
           desc.trim() === '' ||
           link.trim() === '') {
          this.inputIsInvalid = true;
          return;
        }
        
        this.addResource(title, desc, link);
      },
      closeModal(){
        this.inputIsInvalid = false;
      }
    }
  }
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