<script setup> 

import { ref, onMounted } from 'vue'

import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue'

const posts = ref([
  
])
   
const favorite = ref('')

const fav = (title) => {
  favorite.value = title
}

const s= ref(0)
const e = ref(10)
const previusState = ref(false)
const nextState = ref(false)
const loading =ref(true)



const next = () => {
  if(s.value <= 80){
    s.value += 10;
    e.value += 10
  }else{
    nextState.value = true
  }
  
}

const previus = () => {
  if(s.value >= 10){
    s.value -= 10
    e.value -= 10
  }else{
    previusState.value = true
  }


}

const fetchData = async () =>{
  try{
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    posts.value = await res.json()

  }catch(error){
    console.log(error)
  }finally{
    loading.value = false
  }
}

fetchData()


</script>


<template>

  <LoadingSpinner v-if="loading"/>

  <div class="container" v-else>
    <h1> APP</h1>
    <h2>My fav post: {{ favorite }}</h2>
    
    <PaginatePost 
    class="mb-2"
    @nextPag="next"
    @previusPag = "previus"
    :activeNext = 'nextState'
    :activePrevius = 'previusState'
    />

    <BlogPost 
    v-for="post in posts.slice(s, e)"
    class="mb-2"
    :key="post.id"
    :title="post.title"
    :body="post.body"  
    :id="post.id" 
    @fav ="fav"
    > </BlogPost>
  
    
  </div>


</template>