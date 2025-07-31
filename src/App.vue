<template>
  <div>
    <header class="header">
    <div class="container">
        <div class="header__inner">
            <div class="header__logo">
                <img src="./assets/img/face.png" style="height: 40px; margin-bottom: -8px" alt="Anime Logo" />
                AnimeWorld
            </div>
            <nav class="nav">
                <div class="search">
                    <svg xmlns="http://www.w3.org/2000/svg" id="Layer_1" data-name="Layer 1" viewBox="0 0 24 24" width="30" height="30">
  <path d="m23.854,23.146l-7.295-7.295c1.517-1.684,2.442-3.912,2.442-6.351C19,4.262,14.738,0,9.5,0S0,4.262,0,9.5s4.262,9.5,9.5,9.5c2.44,0,4.667-.925,6.351-2.442l7.295,7.295c.098.098.226.146.354.146s.256-.049.354-.146c.195-.195.195-.512,0-.707ZM1,9.5C1,4.813,4.813,1,9.5,1s8.5,3.813,8.5,8.5-3.813,8.5-8.5,8.5S1,14.187,1,9.5Zm10.5-3.5c-.836,0-1.552.364-2,.949-.448-.585-1.164-.949-2-.949-1.379,0-2.5,1.193-2.5,2.66,0,1.901,2.279,4.222,3.484,5.183.3.239.657.358,1.016.358s.716-.119,1.015-.358c1.206-.961,3.485-3.281,3.485-5.183,0-1.467-1.121-2.66-2.5-2.66Zm-1.609,7.062c-.229.184-.552.184-.782,0-1.291-1.029-3.108-3.075-3.108-4.401,0-.915.673-1.66,1.5-1.66.883,0,1.5.602,1.5,1.464,0,.276.224.5.5.5s.5-.224.5-.5c0-.862.617-1.464,1.5-1.464.827,0,1.5.745,1.5,1.66,0,1.326-1.817,3.372-3.109,4.401Z"/>
</svg>
                <input class="nav__input" v-model="query" type="text" maxlength="40" placeholder="enter anime" @input="searchAnime"/>
                </div>
                <div class="nav__link"> <img src="./assets/img/settings.png" width="30" height="30" @click="openSettings()" :style="styleFlag()"/>
                </div>
                <div class="flag_sfw"><svg xmlns="http://www.w3.org/2000/svg" id="Layer_1" data-name="Layer 1" viewBox="0 0 24 24" width="30" height="30" :style="styleFlag()" @click="openSettings()"><path d="M24,11.5a3.5,3.5,0,0,0-2.149-3.226,10,10,0,0,0-19.7,0,3.5,3.5,0,0,0,1.119,6.718,10.607,10.607,0,0,0,2.071,2.955,8.908,8.908,0,0,0-2.272,4.928,1,1,0,0,0,.868,1.117A1.093,1.093,0,0,0,4.061,24a1,1,0,0,0,.991-.875,6.924,6.924,0,0,1,1.815-3.872A8.948,8.948,0,0,0,12,21a8.94,8.94,0,0,0,5.119-1.74,6.922,6.922,0,0,1,1.808,3.862,1,1,0,0,0,.991.876,1.063,1.063,0,0,0,.125-.008,1,1,0,0,0,.868-1.116,8.9,8.9,0,0,0-2.261-4.918,10.622,10.622,0,0,0,2.082-2.966A3.5,3.5,0,0,0,24,11.5Zm-3.752,1.473a.993.993,0,0,0-1.117.651C18.215,16.222,15.13,19,12,19s-6.215-2.78-7.131-5.378a.994.994,0,0,0-1.117-.651A1.606,1.606,0,0,1,3.5,13a1.5,1.5,0,0,1-.27-2.972,1,1,0,0,0,.816-.878A7.961,7.961,0,0,1,8.13,3a4.075,4.075,0,0,0-.022,1.942,4,4,0,0,0,7.688.318A.977.977,0,0,0,14.851,4H14.7a.867.867,0,0,0-.806.631A2,2,0,1,1,12,2a7.978,7.978,0,0,1,7.954,7.15,1,1,0,0,0,.816.878A1.5,1.5,0,0,1,20.5,13,1.606,1.606,0,0,1,20.248,12.973Z"/><circle cx="9.5" cy="11.5" r="1.5"/><circle cx="14.5" cy="11.5" r="1.5"/></svg></div>
            </nav>
        </div>
    </div>
</header>

    <div class="main-wrapper">
      <div ref="slider1" class="swiper slider">  
        <div class="swiper-wrapper slider__wrapper">
          <div v-for="anime in groups[0]" :key="anime.mal_id" @click="openModal(anime)"  class="swiper-slide slider__item">
            <div class="slider__img">
                <h1>{{ anime.title }}</h1>
                <img :src="anime.images.jpg.large_image_url" class="image_inner" alt="Anime Image" />
                <p>{{ anime.synopsis }}</p>
            </div>
          </div>
        </div>
      </div>
      <div ref="slider2" class="swiper slider">  
        <div class="swiper-wrapper slider__wrapper">
          <div v-for="anime in groups[1]" :key="anime.mal_id" @click="openModal(anime)" class="swiper-slide slider__item">
            <div class="slider__img">
              <h1>{{ anime.title }}</h1>
            <img :src="anime.images.jpg.large_image_url" class="image_inner" alt="Anime Image" />
            <p>{{ anime.synopsis }}</p>
            </div>
          </div>
        </div>
      </div>
      <div ref="slider3" class="swiper slider">  
        <div class="swiper-wrapper slider__wrapper">
          <div v-for="anime in groups[2]" :key="anime.mal_id" @click="openModal(anime)" class="swiper-slide slider__item">
            <div class="slider__img">
              <h1>{{ anime.title }}</h1>
              <img :src="anime.images.jpg.large_image_url" class="image_inner" alt="Anime Image" />
              <p>{{ anime.synopsis }}</p>
            </div>
          </div>
        </div>
      </div>
      <div ref="slider4" class="swiper slider">  
        <div class="swiper-wrapper slider__wrapper">
          <div v-for="anime in groups[3]" :key="anime.mal_id" @click="openModal(anime)" class="swiper-slide slider__item">
            <div class="slider__img">
              <h1>{{ anime.title }}</h1>
              <img :src="anime.images.jpg.large_image_url" class="image_inner" alt="Anime Image" />
              <p>{{ anime.synopsis }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <AnimeModal
      v-if="modalVisible"
      :isVisible="modalVisible"
      :anime="selectedAnime"
      @close="modalVisible = false"
    />
    <Settings 
      v-if="settingsVisible"
      :isSet="settingsVisible"
      @close="settingsVisible = false"
    />
  </div>
</template>

<script>
import AnimeModal from './components/ModalAnime.vue';
import Settings from './components/Settings.vue';
import Swiper from 'swiper/bundle';
import 'swiper/swiper-bundle.css';
import axios from "axios";

export default {
  components: {
    AnimeModal,
  },
  data() {
    return {
      animeList: [],
      loading: true,
      swipers: [],
      groups: [],
      query: "",
      modalVisible: false,
      selectedAnime: {},
      colorFlag: 'rgb(255 209 220 / .95)',
      sfwFlag: false,
      settingsVisible: false  
    };
  },
  mounted() {
    this.fetchAnime();
    this.initializeSwipers();
  },
  methods: {
    changeFlag() {
      this.sfwFlag = !this.sfwFlag;
      if (this.sfwFlag) {
        this.colorFlag = '#da70d6';
      } else {
        this.colorFlag = 'rgb(255 209 220 / .95)';
      }
    },
    styleFlag() {
      return {
        background: this.colorFlag,
      };
    },
    openSettings() {
      this.settingsVisible = true;
    },
    openModal(anime) {
      this.selectedAnime = anime;
      this.modalVisible = true;
    },
    filterAnimeSFW() {
      this.animeList.filter((anime) => anime.sfw == this.sfwFlag);
      let gro = [];
      let len = this.animeList.length / 4;
      gro.push(this.animeList.slice(0, len));
      gro.push(this.animeList.slice(len, len * 2));
      gro.push(this.animeList.slice(len * 2, len * 3));
      gro.push(this.animeList.slice(len * 3, len * 4 ));
      this.groups = gro;
    },
    async fetchAnime() {
      try {
        const response = await axios.get("https://api.jikan.moe/v4/anime?order_by=score&page=1&limit=25");
        this.animeList = response.data.data;
        let gro = [];
        let len = this.animeList.length / 4;
        gro.push(this.animeList.slice(0, len));
        gro.push(this.animeList.slice(len, len * 2));
        gro.push(this.animeList.slice(len * 2, len * 3));
        gro.push(this.animeList.slice(len * 3, len * 4 ));
        this.groups = gro;
      } catch (error) {
        console.error("Ошибка при загрузке аниме: ", error);
      } finally {
        this.loading = false;
      }
    },
    async searchAnime() {
      if (this.query.length >= 2) {
        try {
          const response = await axios.get(`https://api.jikan.moe/v4/anime?q=${this.query}`);
          this.animeList = response.data.data;
          let gro = [];
          let len = this.animeList.length / 4;
          gro.push(this.animeList.slice(0, len));
          gro.push(this.animeList.slice(len, len * 2));
          gro.push(this.animeList.slice(len * 2, len * 3));
          gro.push(this.animeList.slice(len * 3, len * 4 ));
          this.groups = gro;
        } catch (error) {
          console.error("Ошибка при загрузке аниме: ", error);
        } finally {
          this.loading = false;
        }
      } else {
        fetchAnime();
      } 
    },
    initializeSwipers() {
      const sliders = [this.$refs.slider1, this.$refs.slider2, this.$refs.slider3, this.$refs.slider4];

      sliders.forEach((slider, index) => {
        const swiper = new Swiper(slider, {
          freeMode: true,
          centeredSlides: true,
          direction: 'vertical',
          mousewheel: true,
          slidesPerView: 1.75,
          slidesOffsetBefore: -125,
        });
        this.swipers.push(swiper);
      });

      this.bindSwipers(...this.swipers);
    },
    bindSwipers(...swiperList) {
      for (const swiper of swiperList) {
        swiper.setTranslate = function (translate, byController, doNotPropagate) {
          if (doNotPropagate) {
            Swiper.prototype.setTranslate.apply(this, arguments);
          } else {
            for (const swiper of swiperList) {
              swiper.setTranslate(translate, byController, true);
            }
          }
        };
        swiper.setTransition = function (duration, byController, doNotPropagate) {
          if (doNotPropagate) {
            Swiper.prototype.setTransition.apply(this, arguments);
          } else {
            for (const swiper of swiperList) {
              swiper.setTransition(duration, byController, true);
            }
          }
        };
      }
    },
  },
};
</script>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}
.swiper {
  margin-top: 30px;
  width: 100%;
  height: 100vh;
}
:root {
	--transition: 1.25s cubic-bezier(.2, .6, 0, 1);
}
html, body {
	height: 100vh;
  width: 100vw;
	overflow: hidden;
  background-image: url(assets/img/bg.jpg);
	background-size: cover;
	background-position: center;
}
.main-wrapper {
  display: flex;
}

.image_inner {
	width: 200px;
	height: 200px;
  border-radius: 8px;
}

.slider__img p {
	margin: 5px;
	max-height: 400px;
	font-size: 13px;
  -webkit-line-clamp: 7; /* Число отображаемых строк */
  display: -webkit-box; /* Включаем флексбоксы */
  -webkit-box-orient: vertical; /* Вертикальная ориентация */
  overflow: hidden; 
  color: #B39BC8;
  padding-top: 10px;
  font-family: Bokor;
}

.slider__img h1 {
  font-family: Cookie;
  color: #B39BC8;
  margin-top: 10px;
  margin-bottom: 10px;
  -webkit-line-clamp: 2;
  display: -webkit-box; 
  -webkit-box-orient: vertical;
  overflow: hidden; 
}
.main-wrapper {
	height: 100%;
	display: flex;
	gap: 80px;
	background-image: url(assets/img/bg.jpg);
	background-size: cover;
	background-position: center;
}
.slider {
	transform: rotate(12.5deg);
	overflow: visible;
}
.slider:nth-child(odd) {
	transform: rotate(192.5deg);
}
.slider .slider__wrapper {
	transition: var(--transition)!important;
	will-change: transform;
}
.slider__item {
	width: 21vw;
	margin-bottom: 20px;
	cursor: pointer;
	transition: transform var(--transition);
	will-change: transform;
	box-shadow: rgb(208 151 162 / .2) 0 0 30px 10px;
  display: flex;
	align-items: center;
	justify-content: center;
	text-align: center;
  border-radius: 8px;
  background-color: rgb(255 209 220 / .35) ;
  max-height: 500px;
}
.slider__item:hover {
	transform: scale(1.04);
}
.slider__item a{
  text-decoration: none;
	width: 100%;
	height: 100%;
}
.slider:nth-child(odd) .slider__img {
	transform: rotate(-180deg);
}

/* Container */
.container {
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
}

/* Header */
.header {
    width: 100%;
    padding-top: 20px;

    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 1000;
    background-color: rgb(255 209 220 / .95) ;
}

.header__inner {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.header__logo {
    font-size: 30px;
    font-weight: 700;
    color: #9074A8;
    margin-bottom: 10px;
}

/* Nav */
.nav {
    font-size: 14px;
    vertical-align: top;
    display: inline-block;
    text-transform: uppercase;
}

.search {
    position: relative;
    display: inline-block;
    vertical-align: top;
}

.search svg {
    margin-top: -5px;
}

.nav__input {
    border: none;
    border-bottom: 1px solid #9074A8;
    background-color: transparent;
    color: inherit;
    outline: none;
    color: #da70d6;
    margin-left: 10px;
    font-size: 18px;
    text-transform: uppercase;
    vertical-align: top;
    margin-top: 5px;
}

::placeholder {
    color: #9074A8;
}

.flag_sfw {
  display: inline-block;
}

.flag_sfw svg {
  background: rgb(255 209 220 / .95);
  border-radius: 10px;
  padding: 2px 2px;
  cursor: pointer;
}

.nav__link {
    display: inline-block;
    vertical-align: top;
    margin: 0 15px;
    position: relative;

    color: #9074A8;
    text-decoration: none;

    transition: color .1s linear;
}

.nav__link:after {
    content: "";
    display: block;
    width: 100%;
    height: 3px;

    background-color: #da70d6;
    opacity: 0;

    position: absolute;
    top: 100%;
    left: 0;
    z-index: 1;

    transition: opacity .1s linear;
}

.nav__link.active {
    color: #da70d6;
}

</style>
