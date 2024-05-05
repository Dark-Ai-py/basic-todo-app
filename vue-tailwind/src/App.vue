<script setup>
import { ref } from 'vue'

let cards = ref([
  {title: 'Date', description: 'yapping'},
]);
  let modalValue = ref("");
  let maxCharExceeded = ref(false);
  function isMaxCharExceeded() {
    if (modalValue.value.length >= 100) {
      maxCharExceeded = true;
    } else {
      maxCharExceeded = false;
    }
  }

function addCard(desc, event) {
  if (maxCharExceeded == true) {
    if (event) {
      event.preventDefault();
    }
  } else if (maxCharExceeded == false) {
  let dateClass = new Date();
  let year = new String(dateClass.getFullYear())
  let date =`${dateClass.getMonth() + 1}/${dateClass.getDate()}/${year.substring(2)}`;
  cards.value.push({title: date, description: desc});
  modalValue.value = "";
  } 
}

function removeCard(index) {
  console.log(index)
  cards.value.splice(index, 1);
}

</script>

<template>
  <div data-theme="cyberpunk" class="wrapper h-full">
    <nav class="navbar bg-base-100">
      <div class="flex-1">
        <a class="btn text-xl">ToDo list</a>
      </div>
      <div class="flex-none">
        <button class="btn btn-square btn-ghost" onclick="add_card.showModal()">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" class="inline-block w-5 h-5 stroke-current"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 12h.01M12 12h.01M19 12h.01M6 12a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0z"></path></svg>
        </button>
      </div>
    </nav>

    <dialog id="add_card" class="modal">
      <div class="modal-box overflow-hidden">
        <h3 class="font-bold text-lg mb-5">Hello! What would you like to add?</h3>
        <textarea class="textarea textarea-secondary w-full h-24 overflow-none no-underline" maxlength="100" @input="modalValue = $event.target.value; isMaxCharExceeded()"  :value="modalValue"></textarea>
        <p class="py-4 relative bottom-4 pb-0 text-red-500 font-bold" v-show="maxCharExceeded">**This note exceeds the maximum length**</p>
        <div class="modal-action">
          <form method="dialog" class="w-full h-max gap-80 flex">
            <button class="btn btn-error font-semibold" @click="modalValue = ''">Close</button>
            <button class="btn btn-primary font-semibold" @click="addCard(modalValue, $event)">Submit</button>
          </form>
        </div>
      </div>
    </dialog>

    <div class="grid grid-cols-4 grid-rows-2 gap-0.5">
    <div class="card w-ful bg-base-100 shadow-xl max-h-58 border-black border-solid border-2" v-for="(card, index) in cards" :key="index">
      <div class="card-body">
        <h2 class="card-title">{{ card.title }}</h2>
        <p class="line-clamp-5 max-h-28">{{ card.description }}</p>
        <div class="card-actions justify-end">
          <button class="btn btn-primary" @click="removeCard(index)">X</button>
        </div>
      </div>
    </div>
  </div>

  </div>
</template>

<style scoped>
.wrapper {
  width: 100vw;
  height: 100vh;
  
}
textarea {
  resize: none;
}

</style>
