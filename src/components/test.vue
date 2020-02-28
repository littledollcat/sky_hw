<template>
<div>
    <div v-for="repo in repo_data" :key="repo.id">
        <div style="text-align:left; font-size:20px">Name: {{repo.name}}</div>
        <div style="text-align:left; font-size:15px">Description: {{repo.description}}</div>
        <div style="text-align:left; font-size:15px">URL: {{repo.url}}</div>
    </div>
    <div id="app" class="container">
    <!-- <card data-image="https://images.unsplash.com/photo-1479660656269-197ebb83b540?dpr=2&auto=compress,format&fit=crop&w=1199&h=798&q=80&cs=tinysrgb&crop="> -->
    <card :data-image="img">
    <h1 slot="header">Vue</h1>
    <p slot="content">Vue is nice!</p>
  </card>
  <div v-for="i in coo" :key="i">{{i}}</div>
    </div>
    
</div>
</template>

<script>
import axios from 'axios'
import card from './card.vue'
import img1 from '@/assets/logo.png'

export default {
    components:{
        card
    },
    data(){
    return {
      repo_data: [],
      coo: 100,
      img: '\'' + img1+ '\''
    }
  },
  methods:{
      handleScroll() {
        let scrollTop =window.pageYOffset ||document.documentElement.scrollTop ||document.body.scrollTop;
    
    if (scrollTop > 900) {
        this.titlePositon = "fixed";
        this.titleColor = "#fff";
        this.titleBorder = "1px solid #e5e5e5";
    } else {
        this.titlePositon = "static";
        this.titleColor = "transparent";
        this.titleBorder = "0";
    }
    },
      scoll(){
          let isLoading = false
          window.onscroll = () =>{
              let bottomOfWindow = document.documentElement.offsetHeight - document.documentElement.scrollTop - window.innerHeight <= 200
              if (bottomOfWindow && !isLoading) {
                  isLoading = true
                  this.coo+=100
                  isLoading = false
              }
}
      }
  },
  mounted(){
      window.addEventListener("scroll", this.handleScroll);
      this.scoll()
  },
  created(){
    axios.get('https://api.github.com/users/littledollcat/repos')
    .then((response)=>{
      this.repo_data = response.data
      
      
    })
  }
}
</script>

<style>

</style>