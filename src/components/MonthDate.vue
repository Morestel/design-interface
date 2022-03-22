<template>
    
{{ month }}

<ul>
    <li v-for="day in this.days" :key="day">
        {{ day }}
    </li>
</ul>
</template>

<script>
export default{
    data: () => ({
        date: new Date(),
        month: '',
        days: [],
        monthInYear: ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"]

    }),

    mounted(){
        this.extractDate()
        this.getDaysInMonth(this.date.getMonth(), this.date.getFullYear())
    },

    methods:{
        extractDate: function(){
            this.month = this.monthInYear[this.date.getMonth()]
        },

        getDaysInMonth: function(month, year) {
            console.log(month)
            var date = new Date(year, month, 1);
            
            while (date.getMonth() === month) {
                this.days.push(new Date(date).getDate());
                date.setDate(date.getDate() + 1);
            }
        }
    }
}


</script>

