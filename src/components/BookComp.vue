<template>
  <li v-if="!deleted">
    <span @click="open = !open">
      {{ book.name }} - {{ book.price }}E - 
    </span>
			<button @click="deleteBook(book.id)">X</button>
			<div v-if="open">
				{{ book.description }}
			</div>
  </li>
</template>

<script>
import axios from 'axios';

const BASE_API_URL = "http://localhost:8080/api/v1";

export default{
  data() {

    return {
      open: false,
      deleted: false
    }
  },
  methods: {

    deleteBook(id) {

      console.log("delete book " + id);

      axios.delete(BASE_API_URL + "/books/" + id)
          .then(res => this.deleted = true)
          .catch(err => console.log(err));
    }
  },
  props: {
    book: {}
  }
}
</script>