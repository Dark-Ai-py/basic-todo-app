<script setup>
import { ref } from 'vue'

let cards = ref([
  {title: 'Date', description: 'yapping'}
]);

console.log(cards);

  let modalValue = ref(0);

function addCard(desc) {
  let dateClass = new Date();
  let year = new String(dateClass.getFullYear())
  let date =`${dateClass.getMonth() + 1}/${dateClass.getDate()}/${year.substring(2)}`;
  cards.value.push({title: date, description: desc});
}

</script>

<template>
  <div data-theme="dim" class="wrapper">
    <nav class="navbar bg-base-100">
      <div class="flex-1">
        <a class="btn text-xl">daisyUI</a>
      </div>
      <div class="flex-none">
        <button class="btn btn-square btn-ghost" onclick="add_card.showModal()">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" class="inline-block w-5 h-5 stroke-current"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 12h.01M12 12h.01M19 12h.01M6 12a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0z"></path></svg>
        </button>
      </div>
    </nav>

    <dialog id="add_card" class="modal">
      <div class="modal-box min-h-60">
        <h3 class="font-bold text-lg mb-5">Hello! What would you like to add?</h3>
        <textarea class="textarea textarea-secondary w-full max-h-20 min-h-20 overflow-auto mb-3" @input="modalValue = $event.target.value"></textarea>
        <br>
        <div class="modal-action">
          <form method="dialog">
            <button class="btn btn-error absolute left-3 bottom-4">Close</button>
            <button class="btn btn-primary absolute right-3 bottom-4" @click="addCard(modalValue)">Submit</button>
          </form>
        </div>
      </div>
    </dialog>

    <div class="card w-96 bg-base-100 shadow-xl max-h-58" v-for="card in cards" :key="card">
      <div class="card-body">
        <h2 class="card-title">{{ card.title }}</h2>
        <p class="line-clamp-5 max-h-28">{{ card.description }}</p>
        <div class="card-actions justify-end">
          <button class="btn btn-primary">X</button>
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
</style>
