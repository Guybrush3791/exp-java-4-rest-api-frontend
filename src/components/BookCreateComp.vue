<template>
  <div>
    <h1>Book create</h1>
    <form @submit.prevent="createBook">
      <label for="name">Nome</label><br>
      <input type="text" name="name" v-model="book.name">
      <br>
      <label for="description">Description</label><br>
      <input type="text" name="description" v-model="book.description">
      <br>
      <label for="price">Price</label><br>
      <input type="number" name="price" v-model="book.price">
      <br>
      <input type="submit" value="CREATE">
    </form>
  </div>
</template>

<script>
import axios from 'axios';

const BASE_API_URL = "http://localhost:8080/api/v1";

  export default{
    data() {

      return {

        book: {
          name: "",
          description: "",
          price: ""
        }
      };
    },
    methods: {

      createBook() {

        console.log("pre create", JSON.stringify(this.book));

        axios.post(BASE_API_URL + "/books", this.book)
        .then(res => {

          this.$router.push('/');
        })
        .catch(err => console.log(err));
      }
    },
    mounted() {

      console.log("book create mounted");
    }
  }
</script>