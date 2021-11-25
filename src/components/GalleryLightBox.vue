<template>
  <div class="lightbox">
    <v-overlay>
      <v-app class="d-flex flex-row " v-click-outside="hideLightBox">
        <v-card max-width="750px" class="mt-10">
          <v-img max-height="600" max-width="1000" :src="getSrc"> </v-img>

          <img
            @click="likeIsActive = !likeIsActive"
            class="like"
            :class="{ likeActive: likeIsActive }"
            height="40"
            width="40"
            src="../assets/gallery/lightbox/like_icon.svg"
            alt=""
          />
        </v-card>

        <v-card
          class="mx-auto mt-3 pa-8"
          min-width="550px"
          max-width="650px"
          max-height="650px"
        >
          <div>COMMENTS:</div>
          <v-divider></v-divider>
          <p
            v-if="comments.length < 1"
            class="caption grey--text text-center pa-7"
          >
            No one commented yet!
          </p>

          <section v-else class="mt-3">
            <div
              v-for="(comment, i) in comments"
              :key="i"
              class="d-flex align-start"
            >
              <v-icon x-large class="pr-3 pt-1" :color="comment.color"
                >mdi-account-circle</v-icon
              >
              <div>
                <div class="caption grey--text">{{ comment.author }}</div>
                <p class="commentFormat">{{ comment.text }}</p>
              </div>
              <v-divider v-if="i + 1 < comments.length"></v-divider>
            </div>
          </section>

          <v-text-field
            background-color="#F3FDF9"
            v-model="author"
            placeholder="Your name"
            solo
            flat
            dense
            hide-details
            class="body-2 mb-2"
          ></v-text-field>

          <v-textarea
            background-color="#F3FDF9"
            v-model="comment"
            class="body-2"
            solo
            flat
            auto-grow
            rows="3"
            placeholder="Write a comment..."
          ></v-textarea>

          <v-btn @click="saveComment">Send</v-btn>
        </v-card>
      </v-app>
    </v-overlay>
  </div>
</template>

<script>
export default {
  props: {
    imgSrc: {
      type: String,
      required: false
    }
  },
  data () {
    return {
      comments: [
        {
          text: 'Just a comment! Nice picture!',
          color: 'teal',
          author: 'Lily Munster'
        },
        {
          text: 'Like!',
          color: 'purple',
          author: 'Peter Steele'
        }
      ],
      comment: '',
      author: '',
      likeIsActive: false
    }
  },
  computed: {
    getSrc () {
      return this.imgSrc
    }
  },
  methods: {
    saveComment () {
      this.comments.push({
        text: this.comment,
        color: this.randomColor(),
        author: this.author
      })
      this.comment = ''
      this.author = ''
    },
    randomColor () {
      const letters = '0123456789ABCDEF'
      let color = '#'
      for (var i = 0; i < 6; i++) {
        color += letters[Math.floor(Math.random() * 16)]
      }
      return color
    },
    hideLightBox () {
      console.log('click')
      this.$emit('hideLightBox')
    }
  }
}
</script>

<style>
.v-application--wrap {
  align-items: center;
  font-size: 12px;
  overflow: scroll;
  background-color: gray;
}
.v-application--wrap::-webkit-scrollbar {
  display: none;
}
.like {
  position: absolute;
  bottom: 10px;
  right: 10px;
  filter: grayscale(0.5);
}

.likeActive {
  filter: grayscale(0);
  transform: scale(120%);
  transition: 0.3s all ease;
}
</style>
