<script setup>
defineProps({
  item: {
    type: Object,
    required: true
  }
})
</script>

<template>
    
        <foreignObject x="12.5%" :y="svgY(item)" width="40%" :height="svgHeight(item)" class="box item" @click="changeCommon(item.members)">
            <div>{{item.title}}</div>
            <div class="timer-item">{{ item["start-time"] }} - {{ item["end-time"] }}</div>
            <div class="breadcrumb has-dot-separator">
                
                <ul>
                    <span>Members : &nbsp;</span>
                    <li v-for="member in item.members" :key="member">
                        <span class="image is-32x32"><img class="is-rounded" :src="member.avatar_url" alt="Profile picture" :title="member.name"></span>
                    </li>
                </ul>
            </div>
            
        </foreignObject>
</template>

<script>
export default{
    data: () => ({
        
    }),

    emits:['changeCommon'],

    methods:{

        svgY: function (item) { // In function of the start of the item
            let hour = item["start-time"].slice(0, 2);
            let minutes = item["start-time"].slice(3, 5);
            return "" + ((hour * 60) + minutes * 1);
        },

        svgHeight: function (item) {

            let hourBegin = item["start-time"].slice(0, 2);
            let minutesBegin = item["start-time"].slice(3, 5);

            let hourEnd = item["end-time"].slice(0, 2);
            let minutesEnd = item["end-time"].slice(3, 5);

            // Starting by convert hour in minutes then we add the minutes
            let timeHourBegin = hourBegin * 60 + minutesBegin * 1; // 600 
            let timeHourEnd = hourEnd * 60 + minutesEnd * 1;  // 720

            // Then we do the difference between them and we return it
            return "" + timeHourEnd - timeHourBegin;
        },

        changeCommon: function (members) {
            this.$emit('changeCommon', members) // Change the people who are in the box
        }

    }
}


</script>

<style lang="scss">

.item{
  position: relative;
  width:70%;
  background-color: var(--themeColor);
  text-align: center;
  overflow: auto;
  box-sizing: border-box;
  border: solid 1px rgba(255, 255, 255, 0.4);
  border-radius: 5%;
}

</style>