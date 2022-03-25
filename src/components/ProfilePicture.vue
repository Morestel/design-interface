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

<style lang="scss">

.avatar {
  display: block;
  margin: auto;
  top: 10px;
  transition : opacity 0.5s;
}

.avatar:hover {
  opacity: 0.7;
  cursor: pointer;
}

</style>