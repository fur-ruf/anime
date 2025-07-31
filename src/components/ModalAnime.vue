<template>
    <div class="modal" v-if="isVisible" @click.self="closeModal">
      <div class="modal-content">
        <button class="close" @click="closeModal" style="border-radius: 15px; border: none"><img src="../../src/assets/img/no.png" alt="cross"></button>
        <img class="image_inner" :src="anime.images.jpg.large_image_url" alt="anime picture">
        <h2>{{ anime.title }}</h2>
        <p v-if="anime.synopsis != null"><strong>SYNOPSIS:</strong> <br> {{ anime.synopsis }}</p>
        <p v-if="anime.year != null"><strong>AGE LIMIT:</strong> {{ anime.rating }}</p> 
        <p v-if="anime.genres.length > 0"><strong>GENRE: </strong>{{ getGenres(anime.genres) }}</p>
        <p v-if="anime.year != null"><strong>AIRING:</strong> {{ anime.year }}</p> 
        <p v-if="anime.status != null"><strong>STATUS:</strong> {{ anime.status }}</p> 
        <p v-if="this.recommendationList.length > 0"><strong>RECOMMENDATIONS:</strong><li v-for="recom_el in this.recommendationList">{{ recom_el.entry.title }}</li></p>
      </div>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  
  export default {
    props: {
      isVisible: {
        type: Boolean,
        required: true,
      },
      anime: {
        type: Object,
        required: true,
      },
    },
    data() {
        return {
            recommendationList: []
        }
    },
    async created() {
        await this.fetchRecommendations(this.anime.mal_id);
    },
    methods: {
      closeModal() {
        this.$emit('close');
      },
      getGenres(genres) {
        return genres.map(genre => genre.name).join(', ');
      },
      async fetchRecommendations(id) {
      try {
        const response = await axios.get(`https://api.jikan.moe/v4/anime/${id}/recommendations`);
          this.recommendationList = response.data.data.slice(0, 10);
      } catch (err) {
          console.error("Ошибка при загрузке аниме: ", err);
      }
    }
    }
};
  </script>
  
  <style scoped>
  .modal {
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(59, 29, 56, 0.3);
    z-index: 200;
    color: #9074A8;
  }
  .modal-content {
    background-color: rgb(255 209 220 / .95);
    padding: 20px;
    border-radius: 8px;
    height: 650px;
    width: 600px;
	align-items: center;
	justify-content: center;
	text-align: center;
    margin-top: 65px;
    overflow: auto;
    font-family: Lora;
    font-size: 14px;
  }

  .modal-content li {
    text-align: justify;
  }

  .modal-content h2 {
    margin-bottom: 5px;
  }
  .modal-content p {
    text-align: justify;
    margin-bottom: 5px;
  }

.image_inner {
    width: 200px;
	height: 200px;
    border-radius: 8px;
    margin-top: -47px;
    margin-bottom: 7px;
  }
  .close {
    display: block;
    cursor: pointer;
    background-color: rgb(255 209 220 / .95);
  }
  .close img {
    width: 50px;
    height: 50px;
  }
  </style>
  