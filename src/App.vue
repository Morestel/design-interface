<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import ProfilePictureVue from './components/ProfilePicture.vue';
import MonthDateVue from './components/MonthDate.vue';
import TaskCardVue from './components/TaskCard.vue';
import TaskCard from './components/TaskCard.vue';
</script>

<template>
  <header>
    <ProfilePictureVue avatar="https://interactive-examples.mdn.mozilla.net/media/cc0-images/grapefruit-slice-332-332.jpg" />
  </header>

  <main>
    <MonthDateVue />
    <svg id="svgBlock" width="100%" height="1500px">

      <foreignObject v-for="h in hours" :key="h.t" v-bind:x="h.x" v-bind:y="h.y" v-bind:width="h.w" v-bind:height="h.h">
            <div>{{h.t}}</div>
        </foreignObject>
     

      <TaskCard v-for="item in listItem" :key="item" :item="item"/>
    </svg>
    
  </main>
</template>
<script>
export default{
    data: () => ({
        hours: [{ t: "00:00", x: "0", y: "60", w: "12.5%", h: "60px" },
                    { t: "01:00", x: "0", y: "120", w: "12.5%", h: "60px" },
                    { t: "02:00", x: "0", y: "180", w: "12.5%", h: "60px" },
                    { t: "03:00", x: "0", y: "240", w: "12.5%", h: "60px" },
                    { t: "04:00", x: "0", y: "300", w: "12.5%", h: "60px" },
                    { t: "05:00", x: "0", y: "360", w: "12.5%", h: "60px" },
                    { t: "06:00", x: "0", y: "420", w: "12.5%", h: "60px" },
                    { t: "07:00", x: "0", y: "480", w: "12.5%", h: "60px" },
                    { t: "08:00", x: "0", y: "540", w: "12.5%", h: "60px" },
                    { t: "09:00", x: "0", y: "600", w: "12.5%", h: "60px" },
                    { t: "10:00", x: "0", y: "660", w: "12.5%", h: "60px" },
                    { t: "11:00", x: "0", y: "720", w: "12.5%", h: "60px" },
                    { t: "12:00", x: "0", y: "780", w: "12.5%", h: "60px" },
                    { t: "13:00", x: "0", y: "840", w: "12.5%", h: "60px" },
                    { t: "14:00", x: "0", y: "900", w: "12.5%", h: "60px" },
                    { t: "15:00", x: "0", y: "960", w: "12.5%", h: "60px" },
                    { t: "16:00", x: "0", y: "1020", w: "12.5%", h: "60px" },
                    { t: "17:00", x: "0", y: "1080", w: "12.5%", h: "60px" },
                    { t: "18:00", x: "0", y: "1140", w: "12.5%", h: "60px" },
                    { t: "19:00", x: "0", y: "1200", w: "12.5%", h: "60px" },
                    { t: "20:00", x: "0", y: "1260", w: "12.5%", h: "60px" },
                    { t: "21:00", x: "0", y: "1320", w: "12.5%", h: "60px" },
                    { t: "22:00", x: "0", y: "1380", w: "12.5%", h: "60px" },
                    { t: "23:00", x: "0", y: "1440", w: "12.5%", h: "60px" },],
        listItem: [{"id":1,"date":"12/02/2022","start-time":"09:00","end-time":"10:00","title":"Mobile app design","members":[{"name":"Mike","avatar_url":"https://reqres.in/img/faces/3-image.jpg",},
{"name":"Anita","avatar_url":"https://reqres.in/img/faces/3-image.jpg",},]}],
    }),
    methods:{
        
    }
}


</script>

<style>
@import './assets/base.css';

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
