<template>

    <div class="image is-128x128 avatar">
      <img class="is-rounded" :src="avatar" alt="Profile Picture" />
    </div>

</template>

<script>
export default {
  props:["avatar"]

}
</script>
