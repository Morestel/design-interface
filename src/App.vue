<script setup>

import ProfilePictureVue from './components/ProfilePicture.vue';
import MonthDateVue from './components/MonthDate.vue';
import TaskCard from './components/TaskCard.vue';
import Common from './components/Common.vue';


</script>

<template>
  <header>
    <ProfilePictureVue :avatar="data.avatar_url" />
  </header>
    
  <main>
    <MonthDateVue @changeDate="changeDate($event)" />
    <svg id="svgBlock" width="70%" height="1440px">

      <foreignObject v-for="h in hours" :key="h.t" v-bind:x="h.x" v-bind:y="h.y" v-bind:width="h.w" v-bind:height="h.h" class="hour">
            <div>{{h.t}}</div>
      </foreignObject>
     
      <foreignObject x="5%" :y="timeLine" width="100%" height="1px" id="time-actual">

      </foreignObject>

      <TaskCard v-for="task in this.listItem" :key="task" :item="task" @changeCommon="changeCommon($event)"/>
    </svg>
    
    <Common :inCommon="inCommon" />
    
  </main>
</template>
<script>
export default{
    data: () => ({
        hours: [{ t: "00:00", x: "0", y: "0", w: "12.5%", h: "60px" },
                    { t: "01:00", x: "0", y: "60", w: "12.5%", h: "60px" },
                    { t: "02:00", x: "0", y: "120", w: "12.5%", h: "60px" },
                    { t: "03:00", x: "0", y: "180", w: "12.5%", h: "60px" },
                    { t: "04:00", x: "0", y: "240", w: "12.5%", h: "60px" },
                    { t: "05:00", x: "0", y: "300", w: "12.5%", h: "60px" },
                    { t: "06:00", x: "0", y: "360", w: "12.5%", h: "60px" },
                    { t: "07:00", x: "0", y: "420", w: "12.5%", h: "60px" },
                    { t: "08:00", x: "0", y: "480", w: "12.5%", h: "60px" },
                    { t: "09:00", x: "0", y: "540", w: "12.5%", h: "60px" },
                    { t: "10:00", x: "0", y: "600", w: "12.5%", h: "60px" },
                    { t: "11:00", x: "0", y: "660", w: "12.5%", h: "60px" },
                    { t: "12:00", x: "0", y: "720", w: "12.5%", h: "60px" },
                    { t: "13:00", x: "0", y: "780", w: "12.5%", h: "60px" },
                    { t: "14:00", x: "0", y: "840", w: "12.5%", h: "60px" },
                    { t: "15:00", x: "0", y: "900", w: "12.5%", h: "60px" },
                    { t: "16:00", x: "0", y: "960", w: "12.5%", h: "60px" },
                    { t: "17:00", x: "0", y: "1020", w: "12.5%", h: "60px" },
                    { t: "18:00", x: "0", y: "1080", w: "12.5%", h: "60px" },
                    { t: "19:00", x: "0", y: "1140", w: "12.5%", h: "60px" },
                    { t: "20:00", x: "0", y: "1200", w: "12.5%", h: "60px" },
                    { t: "21:00", x: "0", y: "1260", w: "12.5%", h: "60px" },
                    { t: "22:00", x: "0", y: "1320", w: "12.5%", h: "60px" },
                    { t: "23:00", x: "0", y: "1380", w: "12.5%", h: "60px" },],
        data: [],
        listItem :[],
        date: new Date(2022, 2, 22), // When the user arrives, the date is the date of the current date but he can change it from MonthDate component  
        inCommon: [],
        timeLine: 0,
    }),

    mounted(){
      this.loadData();
      this.setTimeLine();
      setInterval(this.setTimeLine, 1000*60); // Every minutes, the timeLine is updated
    },

    updated(){
       // We update the theme color depending of the json file
        try{
          document.documentElement.style.setProperty("--themeColor", this.data.primary_color)
        }catch(e){ // If an error happen we choose a color by default
          document.documentElement.style.setProperty("--themeColor", "#6caaaa")
        }
    },

    methods:{
       
        async loadData(){
          let url = 'http://localhost:3000/data.json'
          let res = await fetch(url)
          this.data = await res.json() // We put our data in an object data

          // Now we put all the tasks of the day in a list
          for (let i in this.data.tasks){
            if (this.data.tasks[i].date == this.date.toLocaleDateString('fr')){
              this.listItem.push(this.data.tasks[i])
            }
          }
        },

        changeDate(event){
          this.date = event
          this.listItem = []
          for (let i in this.data.tasks){
            if (this.data.tasks[i].date == this.date.toLocaleDateString('fr')){ // The date are in the french format in the JSON file
              this.listItem.push(this.data.tasks[i])
            }
          }
        },

        changeCommon(event){ // We change the people who are in the common list
          this.inCommon = event
        },

        setTimeLine(){
          // extract hour and minutes
          let date = new Date()
          let hour = date.getHours()
          let minutes = date.getMinutes()
          this.timeLine = hour*60 + minutes
        }
    }
}


</script>

<style lang="scss">
@charset "utf-8";

$background-color: #171923;

// Themes of the body
$body-background-color: $background-color;
$body-color: #E7E8F2;

:root {
  --themeColor: $background-selected;
}

// Themes of the box (For the item)
$box-background-color: var(--themeColor);
$box-color: #E7E8F2;
$box-padding: 1px;

* {
  margin: 0px;
  padding: 0px;
}

html {
  overflow-x:hidden;
}

header{
  width: 100%;
  height:20%;
}

main{
  position: relative;
  top:20%;
}

::-webkit-scrollbar{
    height: 8px;
    width: 8px;
}

.selected-day{
  background-color: var(--themeColor);
}

.selected-month{
  color:var(--themeColor) !important;
}

#svgBlock{
  background-image: url(./assets/scheduleWall.png);
  background-repeat: repeat;
  background-size: 12.5% 60px;
}

@media screen and (max-width: 1280px) {
  svg {
    width:100%;
  }
}

svg .hour div {
  width: 100%;
  height: 100%;
  font-size: 16px;
  text-align: center;
  margin: 1px;
  box-sizing: border-box;
}

#time-actual{
  border: 1px solid white;
}


@import "../node_modules/bulma/bulma.sass";

</style>
