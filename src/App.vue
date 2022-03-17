<template>
  <div>
    <div id="form">
      <input placeholder="Procure um personagem" type="text" v-model="search" />
      <button @click="findChar">Pesquisar</button>
    </div>
    <ul class="listChar">
      <li
        class="layoutChar"
        v-for="personagem in personagens"
        :key="personagem.id"
      >
        <img class="imgChar" :src="personagem.image" />
        <p class="descriptionChar">{{ personagem.name }}</p>
      </li>
    </ul>
    <div class="layoutButtons">
      <button class="skipButton" @click="previousPage">Previous</button>
      <button class="skipButton" @click="nextPage">Next</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      personagens: [],
      search: "",
      currentPage: "1",
      baseURL: "https://rickandmortyapi.com/api/character/",
    };
  },
  mounted() {
    fetch(this.baseURL)
      .then((response) => response.json())
      .then((data) => {
        this.personagens = data.results;
      });
  },
  methods: {
    findChar() {
      fetch(this.baseURL + `?name=${this.search}`)
        .then((response) => response.json())
        .then((data) => {
          this.personagens = data.results;
        });
    },
    nextPage() {
      this.currentPage++;
      fetch(this.baseURL + `?page=${this.currentPage}`)
        .then((response) => response.json())
        .then((data) => {
          this.personagens = data.results;
        });
    },
    previousPage() {
      this.currentPage--;
      fetch(this.baseURL + `?page=${this.currentPage}`)
        .then((response) => response.json())
        .then((data) => {
          this.personagens = data.results;
        });
    },
  },
};
</script>

<style>
ul {
  list-style: none;
  padding: 0;
}

body {
  background-color: #161616;
}

#form {
  display: flex;
  justify-content: center;
}

#form input {
  width: 300px;
  margin: 10px;
  outline: none;
  border-radius: 10px;
  font-size: 1rem;
  padding: 0.5rem;
}

#form button {
  width: 100px;
  margin: 10px;
  outline: none;
  border-radius: 10px;
  border: none;
  background: rgb(64, 248, 64);
  color: black;
  font-size: 1rem;
}

.descriptionChar {
  font-size: 1.5rem;
  margin: 10px;
  color: rgb(64, 248, 64);
}

.imgChar {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  margin: 10px;
}

.layoutChar {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.listChar {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.layoutButtons {
  display: flex;
  justify-content: center;
}

.skipButton {
  width: 100px;
  margin: 10px;
  outline: none;
  border-radius: 10px;
  border: none;
  background: rgb(248, 64, 64);
  color: rgb(255, 255, 255);
  font-size: 1rem;
}
</style>
