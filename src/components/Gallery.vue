<template>
  <div class="div">
    <v-container>
      <v-row class="">
        <!-- Временный индекс пока не будет API  -->
        <v-col
          class="d-flex child-flex"
          cols="4"
          v-for="item in gallery"
          :key="item"
        >
          <galleryItem
            @giveImgSrc="getLightBoxImgSrc"
            :imgSrc="item"
          ></galleryItem>
        </v-col>
      </v-row>
    </v-container>
    <galleryLightBox
      v-if="this.lightBoxSrc != null"
      :imgSrc="lightBoxSrc"
      @hideLightBox="hideLightBox"
    ></galleryLightBox>
  </div>
</template>

<script>
import GalleryItem from './GalleryItem'
import GalleryLightBox from './GalleryLightBox'

export default {
  components: {
    GalleryItem,
    GalleryLightBox
  },
  data () {
    return {
      gallery: [
        'https://picsum.photos/id/12/1000/600',
        'https://picsum.photos/id/23/1000/600',
        'https://picsum.photos/id/34/1000/600',
        'https://picsum.photos/id/45/1000/600',
        'https://picsum.photos/id/56/1000/600',
        'https://picsum.photos/id/11/1000/600',
        'https://picsum.photos/id/22/1000/600',
        'https://picsum.photos/id/33/1000/600',
        'https://picsum.photos/id/44/1000/600',
        'https://picsum.photos/id/55/1000/600',
        'https://picsum.photos/id/111/1000/600',
        'https://picsum.photos/id/222/1000/600',
        'https://picsum.photos/id/334/1000/600',
        'https://picsum.photos/id/444/1000/600',
        'https://picsum.photos/id/555/1000/600'
      ],
      lightBoxSrc: null
    }
  },
  methods: {
    getLightBoxImgSrc (src) {
      this.lightBoxSrc = src
    },
    hideLightBox () {
      this.lightBoxSrc = null
    }
  }
}
</script>

<style></style>
