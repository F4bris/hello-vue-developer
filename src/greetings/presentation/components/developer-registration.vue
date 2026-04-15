<script setup>

  import {ref} from "vue"

  const firstName = ref ('');
  const lastName = ref ('');
  const errorMessage = ref ('');

  const emit = defineEmits (['developer-registered', 'registration-deferred']);

  function submitRegistrationRequest(){
    let submittedFirstName = firstName.value.toString().trim();
    let submittedLastName = lasttName.value.toString().trim();

    if(submittedFirstName || submittedLastName) {
      console.log('Registering developer');
      emit('developer-registered', {
        firstName: submittedFirstName,
        lastName: submittedLastName
      });

      //TODO: clear fields
      errorMessage.value='';
    }else{
      console.log('Cannot register: Both fields are required');
      errorMessage.value= 'Please provide at least first name or last name. Warning: Both fields are required';

    }
  }

  function deferRegistration{
    console.log('Deferring registration');
    emit('registration-deferred', {firstName: '', lastName:''});
    clearFields();
    errorMessage.value='';
  }

  function clearFields() {
    firstName.value = '';
    lastName.value = '';
    errorMessage.value='';
  }

</script>

<template>
  <div>
    <h2>New Developer</h2>
  </div>
  <div>
    <form v-on:submit.prevent="submitRegistrationRequest">
      <div class="field">
        <label for="first-name">First Name</label>
        <input type="text" id="first-name" v-model="firstName">
      </div>

      <div class="field">
        <label for="last-name">Last Name</label>
        <input type="text" id="last-name" v-model="lastName">

      </div>

      <div class="actions">
        <button type="submit">Register</button>
        <button type="button" v-on:click="deferRegistration()">Later</button>
        <button type="button" v-on:click="clearFields()">Clear</button>
      </div>
    </form>

    <p v-if="errorMessage" class="error" role="alert">{{errorMessage}}}</p>
  </div>
</template>

<style scoped>

</style>