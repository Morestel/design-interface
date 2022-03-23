<script setup>

import ProfilePictureVue from './components/ProfilePicture.vue';
import MonthDateVue from './components/MonthDate.vue';
import TaskCard from './components/TaskCard.vue';


</script>

<template>
  <header>
    <ProfilePictureVue :avatar="data.avatar_url" />
  </header>
    
  <main>
    <MonthDateVue @changeDate="changeDate($event)" />
    <svg id="svgBlock" width="100%" height="1500px">

      <foreignObject v-for="h in hours" :key="h.t" v-bind:x="h.x" v-bind:y="h.y" v-bind:width="h.w" v-bind:height="h.h">
            <div>{{h.t}}</div>
        </foreignObject>
     

      <TaskCard v-for="task in this.listItem" :key="task" :item="task"/>
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
        data: [],
        listItem :[],
        date: new Date(), // When the user arrives, the date is the date of the current date but he can change it from MonthDate component  
    }),

    created(){
      this.loadData();
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
    }
}


</script>

<style lang="scss">
@charset "utf-8";

$background-color: #171923;
$font-color: white;
$primary-color:red;
$purple: #8A4D76;
$background-selected: #6caaaa;

$primary:$purple;

* {
  margin: 0px;
  padding: 0px;
}

html {
  scroll-behavior: smooth;
  min-width: 100%;
  min-height: 100%;
  overflow-x: hidden;
  color: white;
}

body{
  margin: 0;
  background-color: $background-color;
}

header{
  height:150px;
}

main{
  position: relative;
  top:20%;
}

::-webkit-scrollbar{
    height: 8px;
    width: 8px;
}

.avatar {
  position: absolute;
  display: block;
  margin-left: auto;
  margin-right: auto;
  top: 10px;
}

.avatar:hover {
  opacity: 0.7;
  cursor: pointer;
}

.selected-day{
  background-color: $background-selected;
}

.selected-month{
  color:#6caaaa;
}
 

@import "../node_modules/bulma/bulma.sass";

</style>
