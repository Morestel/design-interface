<script setup>
defineProps({
  item: {
    type: Object,
    required: true
  }
})
</script>

<template>
    <foreignObject :x="100" :y="svgY(item)" width="40%" :height="svgHeight(item)">
        <div>{{item.title}}</div>
    </foreignObject>
</template>

<script>
export default{
    data: () => ({
        
    }),

    mounted(){
        console.log(this.item)
    },

    methods:{

        svgY: function (item) { // In function of the start of the item
            let hour = item["start-time"].slice(0, 2);
            let minutes = item["start-time"].slice(3, 5);
            return "" + (60 + (hour * 60) + minutes * 1);
        },

        svgHeight: function (item) {

            let hourBegin = item["start-time"].slice(0, 2);
            let minutesBegin = item["start-time"].slice(3, 5);

            let hourEnd = item["end-time"].slice(0, 2);
            let minutesEnd = item["end-time"].slice(3, 5);
            // Starting by convert hour in minutes then we add the minutes
            let timeHourBegin = hourBegin * 60 + minutesBegin; // 600 
            let timeHourEnd = hourEnd * 60 + minutesEnd;  // 720
            // Then we do the difference between them and we return it
            return "" + timeHourEnd - timeHourBegin;
        },

    }
}


</script>

