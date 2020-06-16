<template>
  <div class="form-container">
      <button :disabled="hasOpened" class="add-btn" @click="active = !active; hasOpened= !hasOpened" > Add a new Book! </button>
      <form v-if="active" @submit="addBook">
          <input type="text" v-model="title" name="title" placeholder="Enter book title..." required>
          <input type="text" v-model="author" name="author" placeholder="Enter book author..." required>
          <input type="text" v-model="pages" name="title" placeholder="Enter # of pages..." pattern="[0-9]+" required>
          <div class="check">
            <input type="checkbox" v-model="checked" name="checkbox">
            <label for="read"> I have read this book </label>
          </div>
          <div class="submission">
            <input type="submit" name="submit" value="Submit">
            <button @click="clear"> Cancel </button>
          </div>
      </form>
  </div>
</template>

<script>
import uniqid from 'uniqid'

export default {
    name: "AddBook",
    
    data() {
        return {
            title: '',
            author: '',
            pages: '',
            checked: false,
            active: false,
            hasOpened: false
        }
    },
    methods: {
        addBook(e) {
            e.preventDefault()
            const newBook= {
                id: uniqid(),
                title: this.title,
                author: this.author,
                pages: this.pages,
                read: this.checked
            }
            //send this up to the parent
            this.$emit('add-book', newBook);

            this.title= ''
            this.author= ''
            this.pages= ''
            this.checked= false
            this.active= false
            this.hasOpened= false
        },
        clear() {
            this.title= ''
            this.author= ''
            this.pages= ''
            this.checked= false
            this.active= false
            this.hasOpened= false
        }
    }
}
</script>

<style scoped>
    .form-container {
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .add-btn {
      margin: 25px;
    }

    form {
        display: flex;
        flex-direction: column;
        width: 500px;
    }

    .check {
        display: flex;
        align-self: center;
        color: white;
    }

    .submission {
        display: flex;
        justify-content: space-evenly;
        margin-top: 10px;
    }

    input[type="text"] {
        margin: 5px;
    }

    input[type="checkbox"] {
        margin-right: 15px;
    }
</style>