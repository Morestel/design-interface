<template>
    
<span @click="changeDate(previousMonth, 'month')">{{ previousMonth }}</span> {{ month }} <span  @click="changeDate(nextMonth, 'month')">{{ nextMonth }}</span>

<ul>
    <li v-for="day in this.days" :key="day">
        <button @click="changeDate(day, 'day')">{{ day }}</button>
    </li>
</ul>
</template>

<script>
export default{
    data: () => ({
        date: new Date(),
        month: '',
        nextMonth:'',
        previousMonth:'',
        days: [],
        monthInYear: ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"]

    }),

    emits:['changeDate']
    ,

    mounted(){
        this.extractDate()
        this.getDaysInMonth(this.date.getMonth(), this.date.getFullYear())
    },
    

    methods:{
        extractDate: function(){
            this.month = this.monthInYear[this.date.getMonth()]
            this.previousMonth = (this.date.getMonth() == 0 ? this.monthInYear[11] : this.monthInYear[this.date.getMonth() - 1])
            this.nextMonth = (this.date.getMonth() == 11 ? this.monthInYear[0] : this.monthInYear[this.date.getMonth() + 1])
        },

        getDaysInMonth: function(month, year) {
            var date = new Date(year, month, 1);
            // We count the number of days in the month
            while (date.getMonth() === month) {
                this.days.push(new Date(date).getDate());
                date.setDate(date.getDate() + 1);
            }
        },

        changeDate: function(toChange, type){
            switch(type){
                case "day":
                    this.date.setDate(toChange);
                    break;
                case "month":
                    var month = ''
                    for (let i = 0; i < this.monthInYear.length; i++){
                        if (this.monthInYear[i] == toChange){
                            month = i
                        }
                    }
                    this.date.setMonth(month)
                    this.extractDate() // Once the month is changed, we extract once again the date in view of updating the visual
                    break;
                default:
                    break;
            }
            
            this.$emit('changeDate', this.date)
        }
    }
}


</script>

