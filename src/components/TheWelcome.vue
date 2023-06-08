<template>
	<!-- <button @click="countAct">{{ count }}</button>
	<HelloWorld msg="Hola Mundo"/> -->

	<h1>Books:</h1>
	<router-link to="/books/create">Book create</router-link>
	<ul>
		<!-- <li
			v-for="book in books"
			@click="open_desc_id = book.id"
		>
			{{ book.name }} - {{ book.price }}E
			<div v-if="open_desc_id == book.id">
				{{ book.description }}
			</div>
		</li> -->
		<BookComp 
			v-for="book in books"
			:book="book"
		/>
	</ul>

</template>

<!-- <script setup>
import { ref, onMounted } from 'vue'

import HelloWorld from './HelloWorld.vue'

const count = ref(0)

function countAct() {
	count.value++;
	console.log(count.value)
}

onMounted(() => {
	console.log('mounted');
})
</script> -->
<script>
import BookComp from './BookComp.vue'
import axios from 'axios';

const BASE_API_URL = "http://localhost:8080/api/v1";

export default{
	data() {

		return {
			count: 0,
			books: [],

			open_desc_id: -1
		}
	},
	components: {
		BookComp
	},
	methods: {

		countAct() {
			this.count++;
			console.log(this.count)
		},
		getBooks() {

			axios.get(BASE_API_URL + "/books")
					.then(res => {
						
						const books = res.data;

						console.log(books);

						this.books = books;
					})
					.catch(err => console.log(err));
		}
	},
	mounted() {

		this.getBooks();
	}
}

</script>