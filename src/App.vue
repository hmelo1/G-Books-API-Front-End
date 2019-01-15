<template>
  <div id="app">
    <div class="container">
      <div class="row justify-content-center">
        <div class="form-group search-input">
          <input placeholder="Enter title of book..." class="form-control input-lg" v-model="bookToSearch">
          <button style ="btn btn-primary" v-on:click="searchBook()"/>
        </div>
      </div>
    </div>
    <div class="resultsOutput">
      Total: {{ totalBooks }} 
      Book Titles:
      <div v-for="book in results">
        <img v-if="book.volumeInfo.imageLinks" :src="book.volumeInfo.imageLinks.thumbnail" />
        <p>
          Title: {{book.volumeInfo.title}}
        </p>
        <p>
          Subtitle: {{book.volumeInfo.subtitle}}
        </p>
        <p v-for="author in book.volumeInfo.authors">
          author: {{author}}
        </p>
      </div>
    </div>
  </div>
</template>
  <script src="https://unpkg.com/axios@0.12.0/dist/axios.min.js"></script>
<script>

export default {
  name: 'app',
  data () {
    return {
      results: [],
      totalBooks: 0,
      bookToSearch: ''
    }
  },
  methods: {
    searchBook() {
      /* eslint-disable no-console */
      var bookSearch = this.bookToSearch.replace(" ", "+")
      axios.get(`https://www.googleapis.com/books/v1/volumes?q=${bookSearch}&key=AIzaSyB5EHX0bII6xf10IovVVN-5QVWZ9Ggd4wg`)
        .then(({data}) => {
          this.results = data.items
          this.totalBooks = data.items.length
        })
      /* eslint-disable no-console */
    }
  }
}
</script>

<style>

</style>
    <!--<img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>-->

<!-- https://www.googleapis.com/books/v1/volumes?q=flowers+inauthor:keyes&key=AIzaSyB5EHX0bII6xf10IovVVN-5QVWZ9Ggd4wg -->