<script setup>

  import {ref} from "vue";
  import {Developer} from "./greetings/model/components/Developer";

  const firstName = ref('');
  const lastName = ref('');
  const developerCount = ref(0);
  const hasRegistered= ref(false);

  function updatedRegisteredDeveloperInfo(developer){
    firstName.value = developer.firstName;
    lastName.value = developer.lastName;
    hasRegistered.value = true;
    console.log('Developer registered: ', developer);
    //TODO: Update developer info
  }

  function resetRegisteredDeveloperInfo(){
    firstName.value = '';
    lastName.value = '';
    hasRegistered.value = false;
    console.log('Registration deferred');
  }

  function updateDeveloperCount(developer){
    const dev = new Developer(developer.firstName, developer.lastName);
    if(dev.fullName !== 'Unknown'){
      developerCount.value++;
    }
  }
</script>

<template>
  <h1>Hello Vue Developer Application</h1>
  <developer-registration @developer-registered ="updatedRegisteredDeveloperInfo"
  @registration-deferred="resetRegisteredDeveloperInfo"/>

</template>
