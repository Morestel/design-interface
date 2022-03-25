<template>
<div class="block">
    <div class="block has-text-centered">
        <div class="month-date">
            <span class="previous-month" @click="changeDate(previousMonth, 'month')">{{ previousMonth }}</span> 
            <span class="content is-medium selected-month actual-month">{{ month }}</span> 
            <span class="next-month" @click="changeDate(nextMonth, 'month')">{{ nextMonth }}</span>
        </div>
        <div class="select is-small is-rounded">
            <select v-model="year" class="is-hovered" @click="changeDate($event, 'year')">
                <option v-for="y in years" :key="y">{{ y }}</option>
            </select>
        </div>
    </div>


    <div class="tabs is-centered">
        <ul>
            <li v-for="day in this.days" :key="day">
                <div v-if="day == this.date.getDate()">
                    <a class="selected-day" @click="changeDate(day, 'day')">{{ day }} <br>{{ dayOfWeek(day) }}</a>
                </div>
                <div v-else>
                    <a @click="changeDate(day, 'day')">{{ day }} <br>{{ dayOfWeek(day) }}</a>
                </div>
                
            </li>
        </ul>
    </div>
    
</div>
</template>

<script>
export default{
    data: () => ({
        date: new Date(),
        month: '',
        nextMonth:'',
        previousMonth:'',
        days: [],
        monthInYear: ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"],
        dayInWeek: ["Sun.", "Mon.", "Tue.", "Wed.", "Thu.", "Fri.", "Sat."],
        year: new Date().getFullYear(),
        years: [],
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
            for (let i = 2017; i < 2100; i++){
                this.years.push(i)
            }
        },

        getDaysInMonth: function(month, year) {
            var date = new Date(year, month, 1);
            this.days = []
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
                    console.log(this.date.getDate())
                    break;
                case "month":
                    var month = ''
                    for (let i = 0; i < this.monthInYear.length; i++){
                        if (this.monthInYear[i] == toChange){
                            month = i
                        }
                    }
                    // We update the year if needed
                    if (this.date.getMonth() == 0 && month == 11){
                        this.year--;
                        this.date.setFullYear(this.year);
                    }
                    if (this.date.getMonth() == 11 && month == 0){
                        this.year++;
                        this.date.setFullYear(this.year);
                    }
                    this.date.setMonth(month)
                    this.extractDate() // Once the month is changed, we extract once again the date in view of updating the visual
                    this.getDaysInMonth(month, this.date.getFullYear()) // And we update the day of the month too
                    break;

                case "year":
                    this.date.setFullYear(toChange.target.value);
                    this.getDaysInMonth(this.date.getMonth(), this.date.getFullYear());
                    break;
                default:
                    break;
            }
            this.$forceUpdate() // ? Maybe not the good way to proceed to update the render
            
            this.$emit('changeDate', this.date)
        },

        dayOfWeek: function(day){ // Given a day we want to return the day of week
            let dayWeek = new Date(this.date.getFullYear(), this.date.getMonth(), day)
            return this.dayInWeek[dayWeek.getDay()]
        }
    }
}


</script>

