<template>
    <div class="common-block">
        <div class="card">
            <header class="card-header">
                <p class="card-header-title is-size-4">In common</p>
            </header>
            <div class="card-content">
                <div class="content">
                    <ul>
                        <li v-for="person in inCommon" :key="person">
                            <div class="member">
                                <span class="image is-64x64"><img :src="person.avatar_url" alt="Profile picture" class="is-rounded" /></span> 
                                <span><a href="#">{{ person.name }}</a></span> <!-- Maybe redirect toward the profile of this user -->
                                <span class="image is-24x24 common-icon"><img src="../assets/message-icon.png" alt="message icon" /></span>
                                <span class="image is-24x24 common-icon"><img src="../assets/phone-icon.png" alt="phone icon" /></span>
                            </div>
                        </li>
                    </ul>
                </div>
            </div>
            
    </div>
    </div> 
</template>

<script>
export default{
    props:{
        inCommon: Object
    },    
}


</script>

<style lang="scss">

@media screen and(max-width: 1280px) {
  .common-block {
    visibility: hidden;
  }
}

.common-block{
  margin-right: 40px;
  float:right;
  width:25%;
}

.card-content .content ul{
  list-style: none;
}

.member span{
  display: inline-block;
  vertical-align: middle;
  margin-left: 10px;
}

.common-icon:hover{
  cursor: pointer;
  opacity: 0.5;
}
</style>