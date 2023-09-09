<template class="container"> 
  <input 
    type="text" 
    placeholder="Add person to invite..."
    v-model="nameInput"
    @keypress.enter="addInvitee"
  >
  <TransitionGroup name="invitees">
    <li 
      v-for="name in names" 
      :key="name"
      @click="removeInvitee(name)"
    >
    {{ name }}
  </li>
  </TransitionGroup>  

</template>

<script setup>
  import {ref} from "vue"

  const names = ref(["Abdur Rahman Talha", "Afnan Ferodusi"])
  const nameInput = ref("")

  const addInvitee = () => {
    names.value.unshift(nameInput.value);
    nameInput.value = ""
  }

  const removeInvitee = (name) => {
    names.value = names.value.filter(n => n !== name)
  }
</script>



<style scoped>
 
  .container {
    position: relative;
  }

  h1 {
    position: absolute;
  }

  button {
    margin-top: 50px;
  } 

  .container {
    max-width: 300px;
    margin: 0 auto
  }

  .container input {
    width: 100%;
    border-radius: 5px;
    border: 1px solid rgba(128,128,128, 0.13);
    padding: 10px;
    margin-bottom: 20px;
    box-shadow: 1px 1px 10px rgba(0,0,0,0.12);
  }

  ul {
    display: inline;
    list-style: none;
    margin: 0px;
    padding: 0px;
  }

  li {
    list-style: none;
    width: 300px;
    border-radius: 5px;
    padding: 5px 10px;
    margin-top: 10px;
    box-shadow: 1px 1px 10px rgba(0,0,0,0.12);
    text-align: center;
    cursor: pointer;
  }

  /* TRANSITION GROUP */

  .invitees-enter-from {
    opacity: 0;
    transform: scale(0.5);   
  }

  .invitees-enter-to {
    opacity: 1;
    transform: scale(1);    
  }

  .invitees-enter-active {
    transition: all 4s ease;
  }

  .invitees-leave-from {
    opacity: 1;
    transform: scale(1);
  }

  .invitees-leave-to {
    opacity: 0;
    transform: scale(0);
  }

  .invitees-leave-active {
    transition: all 0.5s ease;
    position: absolute;
  }

  .invitees-move {
    transition: all 0.5s ease;
  }
</style>
