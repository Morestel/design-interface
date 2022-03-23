<script setup>
defineProps({
  avatar: {
    type: String,
    required: true
  }
})
</script>


<template>

    <div class="image is-128x128 avatar">
      <img class="is-rounded" :src="avatar" alt="Profile Picture" />
    </div>

</template>