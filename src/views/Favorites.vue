<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/">
        <img
          src="../../public/movieSearch.png"
          alt="Quick Movie Search"
          class="featured-img"
        />
        <div class="detail">
          <h3>Favorites</h3>
        </div>
      </router-link>
    </div>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie._id">
        <router-link :to="'/movie/' + movie._id" class="movie-link">
          <div class="movie-image">
            <img :src="movie.poster" alt="Movie Poster" />
            <div class="type">{{ movie.type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.year }}</p>
            <h3>{{ movie.title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";

export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    onBeforeMount(() => {
      getData(
          'http://104.248.250.129:3000/favorites'
        )
          .then((data) => {
            console.log(data);
            movies.value = data;
          });
    });

    async function getData(url = '') {
      const response = await fetch(url, {
        method: 'GET', 
        mode: 'cors', 
        cache: 'no-cache', 
        credentials: 'same-origin', 
        headers: {
          'Content-Type': 'application/json'
    },
      redirect: 'follow',
      referrerPolicy: 'no-referrer'
  });
  return response.json();
}

    return {
      search,
      movies,
    };
  },
};
</script>

<style lang="scss">
.home {
  .feature-card {
    position: relative;

    .featured-img {
      display: block;
      width: 100%;
      height: 500px;
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
        color: #fff;
        margin-bottom: 16px;
      }

      p {
        color: #fff;
      }
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
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        }
      }

      &[type="submit"] {
        width: 100%;
        max-width: 300px;
        background-color: #42b883;
        padding: 16px;
        border-radius: 8px;
        color: #fff;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;

        &:active {
          background-color: #3b8070;
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

        .movie-image {
          position: relative;
          display: block;

          img {
            display: block;
            width: 100%;
            height: auto;
            object-fit: cover;
          }

          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: #42b883;
            color: #fff;
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
            color: #aaa;
            font-size: 14px;
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
}
</style>