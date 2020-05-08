<template>
  <div class="container">
    <a href="https://isneverdead.pythonanywhere.com/books">lihat json</a>
    <div class="row">
        <div class="col-lg-6">
        <b-form inline>
            <label class="sr-only" for="inline-form-input-name">Author</label>
            <b-input
            v-model="author"
            id="inline-form-input-name"
            class="mb-2 mr-sm-2 mb-sm-0"
            placeholder="Author"
            ></b-input>

            <label class="sr-only" for="inline-form-input-name">Title</label>
            <b-input
            v-model="title"
            id="inline-form-input-name"
            class="mb-2 mr-sm-2 mb-sm-0"
            placeholder="Title"
            ></b-input>

            <label class="sr-only" for="inline-form-input-name">first sentence</label>
            <b-input
            v-model="first_sentence"
            id="inline-form-input-name"
            class="mb-2 mr-sm-2 mb-sm-0"
            placeholder="first sentence"
            ></b-input>

            <label class="sr-only" for="inline-form-input-name">Published</label>
            <b-input
            v-model="published"
            id="inline-form-input-name"
            class="mb-2 mr-sm-2 mb-sm-0"
            placeholder="Published"
            ></b-input>

            <b-button @click="tambahBuku" variant="primary">Save</b-button>
        </b-form>
        </div>

        <div class="col-lg-6">
            <div class="list-group">
            <div v-for="book in books" :key="book.id">
                 <div class="list-group-item list-group-item-action">
                    <!-- <div class="d-flex w-100 justify-content-between">
                    </div> -->
                    <h5 class="mb-1">{{ book.title }}</h5>
                    <small class="text-muted">Published : {{ book.published }}</small>
                    <p class="mb-0">First Sentence : {{ book.first_sentence }}</p><br>
                    <p class="mb-1">Author : {{ book.author }}</p>
                    <button class="text-muted mr-1 " @click="editBook(book)">Edit</button> 
                    <button class="text-muted" @click="deleteBook(book)" >Delete</button>
                </div>
            </div>
            
            </div>
        </div>
    </div>

  </div>
</template>

<script>

export default {
  
    name: 'Home',
    data() {
        return {
            id: '',
            books: '',
            author: '',
            title: '',
            published: '',
            first_sentence: ''
        }
    },
    methods: {
      fetchBook() {
        axios
            .get('https://akbar-cors.herokuapp.com/https://isneverdead.pythonanywhere.com/books/')
            .then(response => {
              this.books = response.data.developers
              console.log(response)
              })
            .catch(err => {console.log(err)})
      },
      tambahBuku() {
        if(this.id) this.saveBook()
        else this.addBook()
      },
      addBook() {
        let data = JSON.stringify({
          author: this.author,
          title: this.title,
          published: this.published,
          first_sentence: this.first_sentence
        })
        axios.post('https://akbar-cors.herokuapp.com/https://isneverdead.pythonanywhere.com/books', data, {
          headers: {
            'Content-Type': 'application/json',
        }
        })
        .then(response => {
              console.log(response)
              })
            .catch(err => {console.log(err)})
        this.fetchBook()
      },
      deleteBook(book) {
        axios.delete('https://akbar-cors.herokuapp.com/https://isneverdead.pythonanywhere.com/books/'+book.id )
      this.fetchBook()
      },

      editBook(book) {
        this.id = book.id
        this.author = book.author,
        this.title = book.title,
        this.published = book.published,
        this.first_sentence = book.first_sentence
      }, 
      saveBook(){
        axios.put('https://akbar-cors.herokuapp.com/https://isneverdead.pythonanywhere.com/books/'+this.id+'/', {
          author: this.author,
          title: this.title,
          published: this.published,
          first_sentence: this.first_sentence
        }) 
      }
    },
    mounted() {
        this.fetchBook()
    }
}
</script>

<style>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
