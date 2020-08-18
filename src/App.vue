<template>
  <div id="app">
    <div class="container">
    <div class="row header">
      <div class="col-xs-12">
        <HeaderView v-bind:message="message"/>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-12 col-md-6 listView">
        <table class="table">
          <thead>
          <tr>
      <th scope="col">Title</th>
      <th scope="col">Publisher</th>
          </tr>
          </thead>
          <ListView v-bind:allPosts="allPosts"/>
        </table>
      </div>
      <div class="col-xs-12 col-md-6">

      </div>
    </div>
  </div>
  </div>
</template>

<script>
import ListView from './components/ListView'
import HeaderView from './components/HeaderView'

import gql from 'graphql-tag'

const getPost = gql`{
           allPosts(count: 1000) {
              id
              title
              author {
                id
                firstName
                lastName
              }
              body
            }
          }`

export default {
  name: 'App',
  apollo: {
    allPosts: {
      query: getPost,
      result ({ data }) {
        this.allPosts = Object.assign({}, data.allPosts)
      }
    }
  },  
  components: {
    ListView, HeaderView
  },
  data () {
    return {
       message: 'Welcome to DMR', 
       header: "Article",
       allPosts: '',
    }
  }
}
</script>

<style scoped>

</style>