<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea
          v-model="newNote"
          name="note"
          id="note"
          cols="30"
          rows="15"
        ></textarea>
        <div class="modal-buttons">
          <button @click="addNote">Add Notes</button>
          <button @click="showModal = false" class="close-btn">Close</button>
        </div>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="card-container">
        <div
          v-for="note in notes"
          :key="note.id"
          class="card"
          :style="{ backgroundColor: note.background }"
        >
          <p class="note-text">
            {{ note.text }}
          </p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";

const showModal = ref(false);
const newNote = ref("");

const notes = ref([]);

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

const addNote = () => {
  notes.value.push({
    id: Math.floor(Math.random() * 1000),
    text: newNote.value,
    date: new Date(),
    background: getRandomColor(),
  });
  newNote.value = "";
  showModal.value = false;
};
</script>

<style scoped>
.container {
  max-width: 1000px;
  padding: 10px;
  width: 100vw;
  height: 100vh;
  margin: 0 auto;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
h1 {
  font-size: 60px;
}
header button {
  background: #313131;
  color: #fff;
  padding: 10px;
  font-size: 25px;
  width: 50px;
  height: 50px;
  border-radius: 100%;
  border: none;
  outline: none;
  cursor: pointer;
}
.card {
  width: 300px;
  height: 225px;
  padding: 15px;
  background: paleturquoise;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-top: 30px;
  margin-bottom: 10px;
  border-radius: 15px;
}

.card .note-text {
  font-family: "Dosis";
  font-size: 16px;
  font-weight: bold;
}

.card-container {
  display: flex;
  flex-wrap: wrap;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.78);
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  position: relative;
  width: 750px;
  background: #fff;
  padding: 30px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
}

.modal button {
  width: 140px;
  padding: 10px 15px;
  margin: 10px;
  background: purple;
  border-radius: 25px;
  border: none;
  color: #fff;
  font-size: 18px;

  cursor: pointer;
  font-family: "Dosis";
}
.modal .close-btn {
  background: crimson;
  color: #fff;
}
.modal-buttons {
  align-self: flex-end;
}

textarea {
  border: 1px solid purple;
  font-size: 17px;
  border-radius: 15px;
  padding: 20px;
}
</style>
