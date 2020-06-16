<template>
  <div id="app">
    
      <Header />
      <div class="main"></div>
      <AddBook v-on:add-book="addBook"/>
      <Books v-bind:books="books" v-on:del-book="deleteBook" />
  </div>
</template>

<script>
import Books from './components/books.vue'
import Header from './components/layout/header.vue'
import AddBook from './components/AddBook.vue'

export default {
  name: 'App',
  components: {
    Header,
    AddBook,
    Books
  },
  data() {
    return {
      books: [
        {
          id: 0,
          title: 'The Hobbit',
          author: 'J.R.R. Tolkien',
          pages: 295,
          read: true
        },
        {
          id: 1,
          title: 'Harry Potter and the Philosopher\'s Stone',
          author: 'J.K. Rowling',
          pages: 246,
          read: false
        }
      ],
      dataFields:['books']
    }
  },
  mounted() {
    this.dataFields.forEach(field => this.checkStorage(field))
  },
  methods: {
    checkStorage(key) {
      if(localStorage.getItem(key)) {
        try {
          this[key] = JSON.parse(localStorage.getItem(key))
        } catch(e) {
          localStorage.removeItem(key)
        }
      }
    },
    deleteBook(id) {
      this.books= this.books.filter(book => book.id !== id)
      this.saveBooks()
    },
    addBook(newBook) {
      this.books= [...this.books, newBook]
      this.saveBooks()
    },
    saveBooks() {
      this.dataFields.forEach(field =>
      localStorage.setItem(field, JSON.stringify(this[field])))
    }
  }
}
</script>

<style>
  * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    #app {
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    body {
      background-color: #1a1a1a;
      margin: 5%;
    }

  .main {
      display: flex;
      justify-content: center;
    }
</style>
