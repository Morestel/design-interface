<script setup>
defineProps({
  avatar: {
    type: String,
    required: true
  }
})
</script>


<template>

    <img :src="avatar" alt="Profile Picture" />

</template>