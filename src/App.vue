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

import { ref } from 'vue'

function scrollElement(id){
  let element = document.getElementById(id);
  element.scrollIntoView({behavior: 'smooth'});
}

const modalActive = ref(false);
const navActive = ref(false);
let darkMode = ref(localStorage.getItem('darkMode'));
let showFavOnly = ref(false);

const body = document.body;

function toggleDarkMode(){
  if(darkMode.value == null || darkMode.value == false){
    darkMode.value = !darkMode.value;
    localStorage.setItem('darkMode', darkMode.value);
  }else{
    darkMode.value = !darkMode.value;
    localStorage.removeItem('darkMode')
  }
}

function toggleFavOnly(){
  showFavOnly.value = !showFavOnly.value
}

function showNav(){
    body.classList.toggle("body-navActive"); 
    navActive.value = !navActive.value;
}

function showModal(){
    body.classList.toggle("body-navActive");
    modalActive.value = !modalActive.value;
}

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
    <h5 class="text"><a href="https://www.youtube.com/@KannagiTenri"  target="_blank">巫てんり / Kannagi Tenri</a>
    </h5>
    <img src="./assets/img/twitter.png" class="logo2" />
    <h5 class="text"><a href="https://twitter.com/kannagi_tenri"  target="_blank">@kannagi_tenri</a>
    </h5>
  </div>
  
  <!-- <a class="burger-btn" @click="showNav()">
      <span></span>
      <span></span>
      <span></span>
    </a> -->
  
  <div class="nav-overlay">
    <div class="menu-column">
        <div @click.stop >
          <h2>Category 範疇</h2>
          <ul @click="scrollElement('General')">
            <li><a >General 一般</a></li>
          </ul>
          <ul @click="scrollElement('Greeting')">
            <li><a >Greeting 挨拶</a></li>
          </ul>
          <ul @click="scrollElement('Cute')">
            <li><a >Cute 可愛い</a></li>
          </ul>
          <ul @click="scrollElement('Scream')">
            <li><a >Scream 悲鳴</a></li>
          </ul>
          <ul @click="scrollElement('Laugh')">
            <li><a >Laugh 笑い声</a></li>
          </ul>
          <ul @click="scrollElement('Noises')">
            <li><a>Noises ランダム声</a></li>
          </ul>
          <ul @click="scrollElement('English')">
            <li><a>English　英語</a></li>
          </ul>
          <ul @click="scrollElement('Singing')">
            <li><a >Singing 歌唱</a></li>
          </ul>
          <ul><img id="btn-information" src="./assets/img/more-info.png" alt="Button Image" :class="{ darkmode: darkMode }" @click="showModal()" /></ul>
        </div>
      </div>
    </div>
    <div  class="content-column">
      <TenriRandomNoise :soundObjs="[General, Greeting, Cute, Singing, Scream, Laugh, Noises, English]" />
      <hr style="border-top: 1px solid black; margin: 20px auto; width:80%">
      <div class="category" id="General">
        <h2> General 一般</h2>
        <TenriNoise v-for="item in General" :toggleFav="showFavOnly" :category="item.category" :file="item.file" :title="item.title" :nouveau="item.new" />
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
  width: 20%; /* Adjust the width of the menu column */
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
  width: 80%; /* Adjust the width of the content column */
  float: right;
  margin-left: 20%;
  padding: 20px;
}

</style>
