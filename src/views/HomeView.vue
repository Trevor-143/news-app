<template>
  <div class="home">
    <nav>
      <img src="../assets/news2.png" alt="" srcset="">
      <form>
        <input type="text" placeholder="search for news..">
        <button>Search</button>
      </form>
    </nav>
    
    <div class="healines">
      <h3 class="top">Top News Headlines</h3>
      <div class="headlineStories">
        <div class="hstory" v-for="story in breakingNews" :key="story.index">
          <img :src="story.urlToImage" :alt="story.title">
          <div class="note">
            <h3 class="title">{{ story.title }}</h3>
            <a :href="story.url">
              <div class="bar"></div>
              <h3 class="from">{{ story.source.name }}</h3>
            </a>
          </div>
        </div>
      </div>
    </div>

    <div class="latest">
      <h3>Latest</h3>
      <div class="latestItems">
        <div class="item" v-for="item in weather" :key="item.index">
          <img :src="item.urlToImage" :alt="item.title">
          <div class="see">
            <h3 class="title">{{ item.title }}</h3>
            <a :href="item.url">
              <div class="bar"></div>
              <h3 class="from">{{ item.source.name }}</h3>
            </a>
          </div>
        </div>
      </div>
    </div>

    <div class="healines">
      <h3 class="top">Tesla News</h3>
      <div class="headlineStories">
        <div class="hstory" v-for="story in teslaNews" :key="story.index">
          <img :src="story.urlToImage" :alt="story.title">
          <div class="note">
            <h3 class="title">{{ story.title }}</h3>
            <a :href="story.url">
              <div class="bar"></div>
              <h3 class="from">{{ story.source.name }}</h3>
            </a>
          </div>
        </div>
      </div>
    </div>

    <div class="healines">
      <h3 class="top">Apple News</h3>
      <div class="headlineStories">
        <div class="hstory" v-for="story in appleNews" :key="story.index">
          <img :src="story.urlToImage" :alt="story.title">
          <div class="note">
            <h3 class="title">{{ story.title }}</h3>
            <a :href="story.url">
              <div class="bar"></div>
              <h3 class="from">{{ story.source.name }}</h3>
            </a>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue'
import env from "@/env";

export default {
  name: 'HomeView',

  setup() {
    const breakingNews = ref([])
    const teslaNews = ref([])
    const appleNews = ref([])
    const weather = ref([])

    onBeforeMount(() => {
      fetch(`https://newsapi.org/v2/top-headlines?country=us&pageSize=16&apiKey=${env.apiKey}`)
      .then(resp => resp.json())
      .then(data => {
        // console.log(data)
        breakingNews.value = data.articles
      })
      fetch(`https://newsapi.org/v2/everything?q=tesla&pageSize=9&apiKey=${env.apiKey}`)
      .then(resp => resp.json())
      .then(data => {
        // console.log(data)
        teslaNews.value = data.articles
      })
      fetch(`https://newsapi.org/v2/everything?q=apple&pageSize=9&apiKey=${env.apiKey}`)
      .then(resp => resp.json())
      .then(data => {
        // console.log(data)
        appleNews.value = data.articles
      })
      fetch(`https://newsapi.org/v2/everything?q=weather&pageSize=50&apiKey=${env.apiKey}`)
      .then(resp => resp.json())
      .then(data => {
        // console.log(data)
        weather.value = data.articles
      })
    })
    return {
      breakingNews,
      teslaNews,
      appleNews,
      weather
    }
  }
}
</script>


<style>
  .home nav {
    margin-top: 1rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .home nav img {
    width: 50px;
  }
  .home nav form input {
    border: none;
    background-color: #eeeeee;
    padding: 10px;
  }
  .home nav form input:focus {
    outline: none;
  }
  nav form button {
    border: none;
    background-color: #000;
    color: #fff;

    padding: 10px;
  }

  .healines {
    margin-top: 2rem;
  }
  .healines .top {
    padding-bottom: 0.5rem;
  }
  .headlineStories img {
    width: 100%;
    aspect-ratio: 1/.8;
    object-fit: cover;
  }
  .headlineStories {
    display: grid;
    gap: 1rem;
    grid-template-columns: repeat(auto-fit, minmax(10rem, 1fr));
  }
  @media(min-width: 30rem) {
    .headlineStories .hstory:nth-child(1) {
      grid-row: span 2;
      grid-column: span 3;
    }
    .headlineStories .hstory:nth-child(1) img {
      aspect-ratio: 1/0.5;
      height: 100%;
      object-fit: cover; 
    }
  }
  .title {
    overflow: hidden;
    display: -webkit-box;
    -webkit-line-clamp: 2; /* number of lines to show */
            line-clamp: 2; 
    -webkit-box-orient: vertical;
    font-size: 13px;
    color: #ffffff;
  }
  .from {
    font-size: 14px;
  }
  .hstory {
    position: relative;
  }
  .bar {
    width: 80px;
    height: 2px;
    margin-top: 0.5rem;
    background-color: rgba(255, 255, 255, 0);
  }
  .note {
    padding: 0.5rem;
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    background-image: linear-gradient(to top, rgba(0, 0, 0, 1), rgba(0, 0, 0, 0.2));
  }
  .note a {
    text-decoration: none;
    color: #fff;
  }
  .latestItems {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    overflow-x: auto;
  }
  .see .title {
    overflow: hidden;
    display: -webkit-box;
    -webkit-line-clamp: 2; /* number of lines to show */
            line-clamp: 2; 
    -webkit-box-orient: vertical;
    font-size: 13px;
  }
  .item {
    margin: .5rem;
  }
  .latestItems img {
    width: 250px;
    height: 150px;
    object-fit: cover;
  }
  
</style>