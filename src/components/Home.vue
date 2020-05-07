<template>
  <div class="container">
    <div class="row">
        <div class="col-lg-6">
            {{ books }}
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

            <b-button @click="save" variant="primary">Save</b-button>
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
                    <p class="mb-0">Author : {{ book.first_sentence }}</p><br>
                    <p class="mb-1">First Sentence : {{ book.author }}</p>
                    <button class="text-muted mr-1">Edit</button> 
                    <button class="text-muted">Delete</button>
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
            books: '',
            author: '',
            title: '',
            published: '',
            first_sentence: ''
        }
    },
    methods: {
      save() {
        axios.post('https://isneverdead2.pythonanywhere.com/books', {
            author: this.author,
            title: this.title,
            published: this.published,
            first_sentence: this.first_sentence
        })
      }
    },
    mounted() {
        
        axios
            .get('https://isneverdead2.pythonanywhere.com/books/')
            .then(response => {
              this.books = response.data.developers
              console.log(response)
              })
            .catch(err => {console.log(err)})
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
