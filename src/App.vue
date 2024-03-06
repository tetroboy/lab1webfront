<template>
    <div id="app" class="container mt-5">
      <h2>App Workspace</h2>
      <div class="mb-3">
        <h3>Learn New Words</h3>
        <ul class="list-group">
          <li class="list-group-item" v-for="(word, index) in words" :key="index">{{ word }}</li>
        </ul>
      </div>
      <div class="mb-3">
        <input type="text" v-model="newWord" class="form-control" placeholder="Enter new word">
        <button class="btn btn-primary" @click="addWord(newWord)">Add New Word</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        words: [],
        newWord: ''
      };
    },
    created() {
      this.loadUserWords();
    },
    methods: {
      // Метод для завантаження даних з локального сховища
      loadUserWords() {
        const userWords = JSON.parse(localStorage.getItem('userWords')) || [];
        this.words = userWords;
      },
      // Метод для додавання нового слова
      addWord(wordToAdd) {
        const userWords = JSON.parse(localStorage.getItem('userWords')) || [];
        userWords.push(wordToAdd);
        localStorage.setItem('userWords', JSON.stringify(userWords));
        console.log('Слово додано:', wordToAdd);
  
        // Оновити список слів
        this.loadUserWords();
      }
    }
  };
  </script>
  
  <style>
  #app {
    font-family: Arial, sans-serif;
    text-align: center;
  }
  </style>