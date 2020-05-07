<template>
  <div class="container">
    <div class="row">
        <div class="col-lg-6">
            {{ books }}
        <b-form inline>
            <label class="sr-only" for="inline-form-input-name">Name</label>
            <b-input
            id="inline-form-input-name"
            class="mb-2 mr-sm-2 mb-sm-0"
            placeholder="Jane Doe"
            ></b-input>

            <label class="sr-only" for="inline-form-input-name">Name</label>
            <b-input
            id="inline-form-input-name"
            class="mb-2 mr-sm-2 mb-sm-0"
            placeholder="Jane Doe"
            ></b-input>

            <label class="sr-only" for="inline-form-input-name">Name</label>
            <b-input
            id="inline-form-input-name"
            class="mb-2 mr-sm-2 mb-sm-0"
            placeholder="Jane Doe"
            ></b-input>

            <label class="sr-only" for="inline-form-input-name">Name</label>
            <b-input
            id="inline-form-input-name"
            class="mb-2 mr-sm-2 mb-sm-0"
            placeholder="Jane Doe"
            ></b-input>

            <b-button variant="primary">Save</b-button>
        </b-form>
        </div>

        <div class="col-lg-6">
            <div class="list-group">
            <div>
                <div class="list-group-item list-group-item-action">
                    <div class="d-flex w-100 justify-content-between">
                    <h5 class="mb-1">List group item heading</h5>
                    <small class="text-muted">3 days ago</small>
                    </div>
                    <p class="mb-1">Donec id elit non mi porta gravida at eget metus. Maecenas sed diam eget risus varius blandit.</p>
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
            books: ''
        }
    },
    methods: {

    },
    mounted() {
        const config = { 
          headers: {
              'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8',
              'Access-Control-Allow-Origin': '*'
            } 
          }
        axios
            .get('https://isneverdead2.pythonanywhere.com/books/' ,config)
            .then(response => {
              this.books = response
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
