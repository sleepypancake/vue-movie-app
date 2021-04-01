<template>
  <div class="home wrapper">

    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img src="https://animego.org/upload/anime/images/5a3fbf0c1fd3c.jpg" 
        alt="Наруто" class="featured-img">
        <div class="detail">
          <h3>Наруто</h3>
          <p> Наруто грезит всю жизнь – стать Х
             окагэ – вождем деревни, что скрыта в листве. Много соперников встретит юнец, но это путь ниндзя! Путь Узумаки! Путь настоящего Хокагэ!</p>
        </div>
      </router-link>
    </div>

    <form @submit.prevent="SearchMovies()" class="search-box">
      <input type="text" placeholder="Что вы ищете?" v-model="search">
      <input type="submit" value="Найти">
    </form>
    
    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
              <img :src="movie.Poster" alt="Movie Poster" />
              <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="product-detail ">
            <p class="year"> {{ movie.Year }} </p>
            <h3> {{ movie.Title }} </h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import env from '@/env.js';

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
   }

   .featured-img {
     display: block;
     width: 100%;
     height: 300px;
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
   }

   h3 {
     color: #fff;
     margin-bottom: 16px;
   }

   p {
     color: #fff;
   }
}

.search-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 16px;

  input {
    display: block;
    appearance: none;
    border: none;
    outline: none;
    background: none;

    &[type="text"] {
      width: 100%;
      color: #fff;
      background-color: #496583;
      font-size: 20px;
      padding: 10px 16px;
      border-radius: 8px;
      margin-bottom: 15px;
      transition: 0.4s;

      &::placeholder {
        color: #f3f3f3;
      }

      &:focus {
        box-shadow: 0 3px 6 px rgba(0, 0, 0, 0.2);
      }
    }

    &[type="submit"] {
      width: 100%;
      max-width: 300px;
      background-color: #42B883;
      padding: 16px;
      border-radius: 8px;
      color: #fff;
      font-size: 20px;
      text-transform: uppercase;
      transition: 0.4s;

      &:active {
        background-color: #42B070;
      }
    }
  }
}

.movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0 8px;

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
            height: 275px;
            object-fit: cover;
          }

          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: #42B883;
            color: #fff;
            bottom: 16px;
            left: 0;
            text-transform: capitalize;
          }
        }

        .product-detail {
          background-color: #496583;
          padding: 16px 8px;
          flex: 1 1 100%; 
          border-radius: 0 0 8px 8px;

          .year {
            color: #AAA;
            font-size: 14px;
            margin-bottom: 6px;
          }

          h3 {
            color: #fff;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
}

@media (min-width: 479px) {
  .home {
    .feature-card {
      position: relative;
      padding: 0 20px;
    }

    .detail {
      margin: 0 20px;
    }
  }
  .search-box {
      flex-direction: row;

      input {
         &[type="text"] {
           margin-bottom: 0;
           margin-right: 20px;
         }

         &[type="submit"] {
           padding: 10px;
           max-width: 200px;
         }
      }
  }
}

@media (min-width: 1441px) {
    .movies-list {
      display: grid;
      grid-template-columns: repeat(3, 1fr);

      .movie {
        max-width: 100%;
        padding: 0;
        margin: 30px 20px;
      }

      .movie:hover {
            transform: translateY(-10px);
            box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.6);
        }

  }
}

</style>