
<template>
  <div id="app" class="container">
    <div class ="page-header">
      <h1>Vue.js & firebase Sample App</h1>
    </div>

    <div class="panel panel-default">
      <div class="panel-heading">
        <h3>Add Book</h3>
      </div>
      <div class="panel-body">
        <form id="form" class="form-inline" v-on:submit.prevent="addBook">
          <div clss="form-group">
            <label for="bookTitle">Title : </label>
            <input type="text" id="bookTitle" class="form-control" v-model="newBook.title" />
          </div>
          <div clss="form-group">
            <label for="bookAuthor">Author : </label>
            <input type="text" id="bookAuthor" class="form-control" v-model="newBook.author" />
          </div>
          <div clss="form-group">
            <label for="bookUrl">url : </label>
            <input type="text" id="bookUrl" class="form-control" v-model="newBook.url" />
          </div>
          <input type="submit" class="btn btn-primary" value="Add Book"/>
        </form>
      </div>
    </div>


    <div class= "panel panel-default" >
      <div class="panel-heading">
        <h3>BookList</h3>
      </div>
      <div>
        <table class ="table table-striped" >
          <thead>
            <tr>
              <th>
                Title
              </th>
              <th>
                Author
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="book in books">
              <td>
                <a v-bind:href="book.url">{{book.title}}</a>
              </td>
              <td>
                {{book.author}}
              </td>
              <td>
                <span class="glyphicon glyphicon-trash" v-on:click="removeBook(book)"></span>
              </td>
            </tr>

          </tbody>
        </table>
      </div>
    </div>


  </div>
</template>

<script>
export default {
  name: 'App',
  firebase : function(){
    return {
        books : bookRef
    }
  },

  data(){
    return{
      newBook:{
        title:"",
        author: "",
        url : "http://"
      }
    }
  },
  methods:{
    addBook : function(){
      bookRef.push(this.newBook)
      this.newBook.title = '';
      this.newBook.author = '';
      this.newBook.url = '';
    },
    removeBook: function(){
      bookRef.child(book['.key']).remove();
    }
  }

}

import firebase from 'firebase'

let config = {
  apiKey: "AIzaSyBlobC4RRQJOJ-A5z7YJwi4At6IQhAa31c",
  authDomain: "vueboard-29fe6.firebaseapp.com",
  databaseURL: "https://vueboard-29fe6.firebaseio.com",
  projectId: "vueboard-29fe6",
  storageBucket: "vueboard-29fe6.appspot.com",
  messagingSenderId: "451490648446"
}

let app = firebase.initializeApp(config)
let db = app.database()

let bookRef = db.ref('books')

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
