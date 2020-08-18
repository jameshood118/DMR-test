<template>
          <tbody>
            <tr v-for="posts in allPosts" v-bind:key="posts.id" v-bind:title="posts.title" class="articles" v-on:click="getValue(posts.id)">
              <td><p>{{posts.title}}</p></td>
              <td>{{posts.author.firstName}} {{posts.author.lastName}}</td>
            </tr>
          </tbody>
</template>


<script>
import {bus} from '../main'

export default {
  name: 'ListView',
  props: {
    allPosts: {
      required: true
    }
    },
  methods: {
    getValue: function(event){
      console.log(this.posts[event].title);
      bus.$emit('changeArticle', this.posts[event]);
    }
  }
}
</script>

<style scoped>
#app {
  background: #ffffff
}

div.listView {
  border-right: 1px solid rgb(222, 226, 230);
}

tr.articles {
  cursor:pointer;
}

tr.articles:hover{
    background-color:slategray;
}
</style>
