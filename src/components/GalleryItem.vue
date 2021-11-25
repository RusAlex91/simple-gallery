<template>
  <div class="gallery-item" @click="openModal">
    <v-img max-height="281" max-width="455" :src="getSrc"></v-img>
  </div>
</template>

<script>
export default {
  props: {
    imgSrc: {
      type: String,
      required: true
    }
  },
  computed: {
    getSrc () {
      return this.imgSrc
    }
  },
  methods: {
    openModal () {
      this.$emit('giveImgSrc', this.imgSrc)
    }
  }
}
</script>

<style>
.gallery-item {
  cursor: pointer;
}
</style>
