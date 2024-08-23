<script setup>
import TenriNoise from './components/TenriNoise.vue';
import InfoModal from './components/InfoModal.vue';
import TenriRandomNoise from './components/TenriRandomNoise.vue';

import General from './assets/AudioLists/General.json';
import English from './assets/AudioLists/English.json';
import Noises from './assets/AudioLists/Noises.json';
import Greeting from './assets/AudioLists/Greeting.json';
import Scream from './assets/AudioLists/Scream.json';
import Cute from './assets/AudioLists/Cute.json';
import Singing from './assets/AudioLists/Singing.json';
import Laugh from './assets/AudioLists/Laugh.json';

import { ref, onMounted, onBeforeUnmount } from 'vue';

const modalActive = ref(false);
const navActive = ref(false);
const darkMode = ref(localStorage.getItem('darkMode') === 'true');
const showFavOnly = ref(false);
const isMobile = ref(window.innerWidth < 768);

const body = document.body;

function scrollElement(id) {
  const element = document.getElementById(id);
  element.scrollIntoView({ behavior: 'smooth' });
}

function toggleDarkMode() {
  darkMode.value = !darkMode.value;
  localStorage.setItem('darkMode', darkMode.value);
}

function toggleFavOnly() {
  showFavOnly.value = !showFavOnly.value;
}

function showNav() {
  navActive.value = !navActive.value;
  body.classList.toggle("body-navActive", navActive.value);
}

function showModal() {
  modalActive.value = !modalActive.value;
  body.classList.toggle("body-modalActive", modalActive.value);
}

function handleResize() {
  isMobile.value = window.innerWidth < 768;
}

onMounted(() => {
  window.addEventListener('resize', handleResize);
  handleResize(); // Initial check
});

onBeforeUnmount(() => {
  window.removeEventListener('resize', handleResize);
});

</script>

<template>
  <div id="mainPage-div" :class="{ darkmode: darkMode }">
    <Transition>
      <InfoModal v-show="modalActive" @close-modal="showModal()" />
    </Transition>

    <div class="header">
      <img src="./assets/img/tenrilove.png" class="logo" />
      <h1 class="title">KANNAGI TENRI SOUNDBOARD</h1>
      <img src="./assets/img/tenrilove.png" class="logo" />
    </div>
    
    <div class="social-links">
      <img src="./assets/img/youtube.png" class="logo2" />
      <h5 class="text">
        <a href="https://www.youtube.com/@KannagiTenri" target="_blank">巫てんり / Kannagi Tenri</a>
      </h5>
      <img src="./assets/img/twitter.png" class="logo2" />
      <h5 class="text">
        <a href="https://x.com/kannagi_tenri" target="_blank">@kannagi_tenri</a>
      </h5>
    </div>
    
    <!-- Button to toggle menu on mobile -->
    <button class="burger-btn" @click="showNav" v-if="isMobile">
      <span></span>
      <span></span>
      <span></span>
    </button>

    <!-- Navigation menu -->
    <div :class="{ 'nav-overlay': true, 'nav-active': navActive, 'nav-hidden': isMobile && !navActive }">
      <div class="menu-column">
        <div @click.stop>
          <h2>Category 範疇</h2>
          <ul @click="scrollElement('General')">
            <li><a>General 一般</a></li>
          </ul>
          <ul @click="scrollElement('Greeting')">
            <li><a>Greeting 挨拶</a></li>
          </ul>
          <ul @click="scrollElement('Cute')">
            <li><a>Cute 可愛い</a></li>
          </ul>
          <ul @click="scrollElement('Scream')">
            <li><a>Scream 悲鳴</a></li>
          </ul>
          <ul @click="scrollElement('Laugh')">
            <li><a>Laugh 笑い声</a></li>
          </ul>
          <ul @click="scrollElement('Noises')">
            <li><a>Noises ランダム声</a></li>
          </ul>
          <ul @click="scrollElement('English')">
            <li><a>English 英語</a></li>
          </ul>
          <ul @click="scrollElement('Singing')">
            <li><a>Singing 歌唱</a></li>
          </ul>
          <ul>
            <img id="btn-information" src="./assets/img/more-info.png" alt="Button Image" :class="{ darkmode: darkMode }" @click="showModal()" />
          </ul>
        </div>
      </div>
    </div>
    
    <!-- Content column -->
    <div class="content-column">
      <TenriRandomNoise :soundObjs="[General, Greeting, Cute, Singing, Scream, Laugh, Noises, English]" />
      <hr style="border-top: 1px solid black; margin: 20px auto; width:80%">
      <div class="category" id="General">
        <h2>General 一般</h2>
        <TenriNoise v-for="item in General" :key="item.file" :toggleFav="showFavOnly" :category="item.category" :file="item.file" :title="item.title" :nouveau="item.new" />
      </div>
      <hr style="border-top: 1px solid black; margin: 20px auto; width:80%">
      <div class="category" id="Greeting">
        <h2> Greeting 挨拶</h2>
        <TenriNoise  v-for="item in Greeting" :toggleFav="showFavOnly" :category="item.category" :file="item.file" :title="item.title" :nouveau="item.new" />
      </div>
      <hr style="border-top: 1px solid black; margin: 20px auto; width:80%">
      <div class="category" id="Cute">
        <h2> Cute 可愛い</h2>
        <TenriNoise v-for="item in Cute" :toggleFav="showFavOnly" :category="item.category" :file="item.file" :title="item.title" :nouveau="item.new" />
      </div>
      <hr style="border-top: 1px solid black; margin: 20px auto; width:80%">
      <div class="category" id="Scream">
        <h2> Scream 悲鳴</h2>
        <TenriNoise v-for="item in Scream" :toggleFav="showFavOnly" :category="item.category" :file="item.file" :title="item.title" :nouveau="item.new" />
      </div>
      <hr style="border-top: 1px solid black; margin: 20px auto; width:80%">
      <div class="category" id="Laugh">
        <h2> Laugh 笑い声</h2>
        <TenriNoise v-for="item in Laugh" :toggleFav="showFavOnly" :category="item.category" :file="item.file" :title="item.title" :nouveau="item.new" />
      </div>
      <hr style="border-top: 1px solid black; margin: 20px auto; width:80%">
      <div class="category" id="Noises">
        <h2> Noises ランダム声</h2>
        <TenriNoise v-for="item in Noises" :toggleFav="showFavOnly" :category="item.category" :file="item.file" :title="item.title" :nouveau="item.new" />
      </div>
      <hr style="border-top: 1px solid black; margin: 20px auto; width:80%">
      <div class="category" id="English">
        <h2> English 英語</h2>
        <TenriNoise v-for="item in English" :toggleFav="showFavOnly" :category="item.category" :file="item.file" :title="item.title" :nouveau="item.new" />
      </div>
      <hr style="border-top: 1px solid black; margin: 20px auto; width:80%">
      <div class="category" id="Singing">
        <h2> Singing 歌唱</h2>
        <TenriNoise v-for="item in Singing" :toggleFav="showFavOnly" :category="item.category" :file="item.file" :title="item.title" :nouveau="item.new" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.v-enter-active,
.v-leave-active {
  transition: opacity 0.2s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.logo {
  margin-top: 4em;
  will-change: filter;
  transition: filter 300ms;
  width: 40px;
  height: 40px;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #1b1616);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}

.social-links {
  display: flex;
  align-items: center;
  justify-content: center; /* Center content horizontally */
  font-size: 14px; /* Adjust font size as needed */
}

.logo2 {
  margin-top: 1em;
  margin-right: -15px;
  will-change: filter;
  transition: filter 300ms;
  width: 40px;
  height: 40px;
}

.text {
  font-family: 'Riffic'; 
  padding-top: 15px;
  margin-right: 10px;
  font-size: 25px; /* Adjust font size as needed */
}

.menu-column {
  width: 20%; /* Default width for desktop */
  float: left;
  position: fixed; /* Fix the menu in place */
  top: 200px; /* Align the menu to the top */
  bottom: 0; /* Stretch the menu to the bottom */
  overflow-y: auto;
  font-family: 'Riffic';
  padding-left: -1rem;
  padding-right: 1rem;
  font-size: 25px;
} 

.menu-column::-webkit-scrollbar {
  width: 8px; /* Width of the scrollbar */
}

.menu-column::-webkit-scrollbar-track {
  border-radius: 4px;
  background: #f1f1f1; /* Track color */
}

.menu-column::-webkit-scrollbar-thumb {
  background: #888; /* Thumb color */
  border-radius: 4px; /* Rounded corners */
}

.menu-column::-webkit-scrollbar-thumb:hover {
  background: #555; /* Hover color */
}

.content-column {
  width: 80%; /* Default width for desktop */
  float: right;
  margin-left: 20%;
  padding: 20px;
}

.burger-btn {
  display: none; /* Hidden by default */
}

/* Mobile Styles */
@media (max-width: 768px) {
  .menu-column {
    width: 50%; /* Width of the menu on mobile */
    position: fixed;
    top: 0;
    left: -80%; /* Start off-screen */
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5); /* Background color for the menu */
    overflow-y: auto;
    padding-top: 4rem;
    padding-left: 18rem;
    padding-right: 4rem;
    font-size: 25px;
    transition: left 0.3s ease; /* Smooth slide-in effect */
    z-index: 1001; /* Ensure the menu is above other content */
  }

  .burger-btn {
    display: block;
    position: fixed;
    top: 10px;
    left: 10px;
    background: transparent; /* No background color */
    border: none; /* No border */
    outline: none; /* No outline */
    padding: 10px; /* Adjust padding as needed */
    z-index: 1002; /* Above other content */
    cursor: pointer; /* Pointer cursor */
  }

  .burger-btn span {
    display: block;
    border: 3px solid rgb(255, 255, 255); /* Border color and thickness */
    border-radius: 4px; /* Optional: round the corners */
    width: 25px; /* Width of the bars */
    height: 3px; /* Height of the bars */
    background: #c5b3b3; /* Color of the bars */
    margin: 3px 0; /* Space between bars */
    transition: background 0.3s ease; /* Smooth transition */
  }

  .burger-btn:hover span {
    background: #444; /* Change color on hover */
  }

  .logo {
    width: 20px;
    height: 20px;
    margin-top: 2em;
  }

  .logo2 {
    width: 20px;
    height: 20px;
    margin-top: 0.5em;
  }

  .text {
    font-size: 20px;
    padding-top: 8px;
    margin-right: 5px;
  }

  .nav-overlay {
    display: none;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5); /* Semi-transparent background */
    z-index: 1000; /* Ensure the overlay is below the button but above other content */
  }

  .nav-overlay.nav-active {
    display: block;
  }

  .menu-column.nav-active {
    left: 0; /* Slide in */
  }

  .menu-column.nav-hidden {
    left: -70%; /* Slide out */
  }

  .content-column {
    width: 90%; /* Full width for content on mobile */
    margin-left: 0;
  }
}


</style>
