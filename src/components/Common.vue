<template>
    <div class="common-block">
    <h1>In common</h1>
    <ul>
        <li v-for="person in inCommon" :key="person">
            {{ person.name }}
        </li>
    </ul>
    </div> 
</template>

<script>
export default{
    data: () => ({
        
    }),

    props:{
        inCommon: Object
    },    

    methods:{

    }
}


</script>

