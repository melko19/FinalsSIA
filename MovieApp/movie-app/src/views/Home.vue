<template>
    <div class="home">
        <div class="container">
          <div class="feature-card">
          <router-link to="/movie/tt1457767">
            <img src="../assets/back.jpg" alt="The Conjuring" class="featured-img" />
            <div class="detail">
              <h3>The Conjuring </h3>
              <p>A chilling story of terror, murder and unknown evil that shocked even experienced real-life paranormal
                investigators Ed and Lorraine Warren. One of the most sensational cases from their files, it starts with a fight for the soul of a young boy, then takes them beyond anything they'd ever seen before, to mark the first time in U.S. 
                history that a murder suspect would claim demonic possession as a defense. Written by Tiboriyo</p>
            </div>
          </router-link>
        </div>
        </div>

      <form @submit.prevent="SearchMovies()" class="search-box">
        <input type="text" placeholder="Discover new movies..." v-model="search" />
        <input type="submit" value="Search" />
      </form>

      <div class="container">
          <div class="movies-list">
          <div class="movie" v-for="movie in movies" :key="movie.imdbID">
            <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
              <div class="product-image">
                <img :src="movie.Poster" alt="Movie Poster" />
                <div class="type">{{ movie.Type }}</div>
              </div>
              <div class="detail">
                <p class="year">{{ movie.Year }}</p>
                <h3>{{ movie.Title }}</h3>
              </div>
            </router-link>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
import { ref } from 'vue';
import env from '@/env.js'

export default {
  setup () {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then(response => response.json())
          .then(data => {
            movies.value = data.Search;
            search.value = "";
          });
      }
    }

    return {
      search,
      movies,
      SearchMovies
    }
  }
}
</script>

<style lang="scss">
.home {
  .feature-card {
    position: relative;

    .featured-img {
      display: block;
      width: 100%;
      height: 550px;
      object-fit: cover;

      position: relative;
      z-index: 0;
    }

    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;

      h3 {
        color:#FFF;
        margin-bottom: 16px;
      }

      p {
        color: #FFF;
      }
    }
  }

  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding:30px;

    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;

      &[type="text"] {
        width: 70%;
        color: #FFF;
        background-color: #079396;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 20px;
        margin-bottom: 30px;
        transition: 0.4s;

        &::placeholder {
          color: #f3f3f3;
        }

        &:focus {
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        }
      }

      &[type="submit"] {
        width: 100%;
        max-width: 200px;
        height: 50px;
        background-color: #57beee;
        padding: 16px;
        border-radius: 20px;
        color: #FFF;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;

        &:active {
          background-color: #3B8070;
        }
      }
    }
  }

  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;

    .movie {
      max-width: 50%;
      flex: 1 1 50%;
      padding: 16px 8px;

      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;

        .product-image {
          position: relative;
          display: block;

          img {
            display: block;
            width: 100%;
            height: 900px;
            object-fit: cover;
          }

          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: #42B883;
            color: #FFF;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
          }
        }

        .detail {
          background-color: #496583;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;

          .year {
            color: #AAA;
            font-size: 14px;
          }

          h3 {
            color: #FFF;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
}
</style>