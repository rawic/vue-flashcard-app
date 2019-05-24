<template>
  <li class="card-box" :class="card.color">
    <transition name="flip">
      <article
        @click="flipCard(card, $event)"
        :key="card.flipped"
        class="single-card"
      >
        <button type="button" class="delete-icon" @click="deleteCard(card.id)">
          <svg
            class="icon"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 52 52"
          >
            <path
              d="M26 0C11.664 0 0 11.663 0 26s11.664 26 26 26 26-11.663 26-26S40.336 0 26 0zm0 50C12.767 50 2 39.233 2 26S12.767 2 26 2s24 10.767 24 24-10.767 24-24 24z"
            />
            <path
              d="M35.707 16.293a.999.999 0 0 0-1.414 0L26 24.586l-8.293-8.293a.999.999 0 1 0-1.414 1.414L24.586 26l-8.293 8.293a.999.999 0 1 0 1.414 1.414L26 27.414l8.293 8.293a.997.997 0 0 0 1.414 0 .999.999 0 0 0 0-1.414L27.414 26l8.293-8.293a.999.999 0 0 0 0-1.414z"
            />
          </svg>
        </button>
        <h2 class="title">{{ card.flipped ? card.back : card.front }}</h2>
        <button
          type="button"
          class="like-icon"
          :class="{ '-liked': card.liked }"
          @click="likeCard(card)"
        >
          <svg
            class="icon"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 50 50"
          >
            <path
              d="M24.85 10.126c2.018-4.783 6.628-8.125 11.99-8.125 7.223 0 12.425 6.179 13.079 13.543 0 0 .353 1.828-.424 5.119-1.058 4.482-3.545 8.464-6.898 11.503L24.85 48 7.402 32.165c-3.353-3.038-5.84-7.021-6.898-11.503-.777-3.291-.424-5.119-.424-5.119C.734 8.179 5.936 2 13.159 2c5.363 0 9.673 3.343 11.691 8.126z"
            />
          </svg>
        </button>
      </article>
    </transition>
  </li>
</template>

<script>
export default {
  name: "Card",
  props: ["card"],
  methods: {
    flipCard(card) {
      if (event.target && event.target.parentNode.nodeName !== "svg") {
        card.flipped = !card.flipped;
      }
    },
    deleteCard(id) {
      this.$emit("deleteTrigger", id);
    },
    likeCard(card) {
      card.liked = !card.liked;
      this.$emit("likeTrigger", !!card.liked);
    }
  }
};
</script>

<style scoped lang="sass">
@import 'src/assets/sass/_variables.sass';

svg
  width: 100%

.card-box
  padding: 0.8rem
  flex: 1 1 0
  max-width: 283.5px
  @media(max-width: 551px)
    margin-left: auto
    margin-right: auto
  &.-orange .single-card
    background-color: $card-orange
    box-shadow: 0 0 12px 1px rgba($card-orange, .3)
    &:hover
      box-shadow: 0 0 14px 2px rgba($card-orange, .7)
  &.-red .single-card
    background-color: $card-red
    box-shadow: 0 0 8px 1px rgba($card-red, .3)
    &:hover
    box-shadow: 0 0 14px 2px rgba($card-red, .7)
  &.-purple .single-card
    background-color: $card-purple
    box-shadow: 0 0 12px 1px rgba($card-purple, .3)
    &:hover
      box-shadow: 0 0 14px 2px rgba($card-purple, .7)
  &.-blue .single-card
    background-color: $card-blue
    box-shadow: 0 0 8px 1px rgba($card-blue, .3)
    &:hover
      box-shadow: 0 0 14px 2px rgba($card-blue, .7)
  &.-green .single-card
    background-color: $card-green
    box-shadow: 0 0 8px 1px rgba($card-green, .3)
    &:hover
      box-shadow: 0 0 14px 2px rgba($card-green, .7)

.single-card
  width: 250px
  border-radius: $radius
  height: 335px
  padding: 80px 30px
  background-color: $card-blue
  margin: 5px
  text-align: center
  cursor: pointer
  position: relative
  color: #fff
  box-shadow: 0 0 8px 1px rgba($card-blue, .3)
  transition: box-shadow .3s
  &:hover
    box-shadow: 0 0 8px 1px rgba($card-blue, 1)
  .title
    font-size: 1.286rem
    line-height: 1.6
    font-weight: $bold

button
  border: 0
  background-color: transparent
  position: absolute
  fill: white
  padding: 0

.delete-icon
  right: 15px
  top: 15px
  width: 25px
  .icon
    opacity: 0.5
    transition: all .5s
    &:hover
      transform: rotate(180deg)
      opacity: 1

.like-icon
  bottom: 15px
  width: 30px
  left: 0
  right: 0
  margin-left: auto
  margin-right: auto
  fill: white
  opacity: .4
  &:hover
    opacity: 0.6
  &.-liked
    opacity: 1

.flip-enter-active
  transition: all 0.6s
.flip-leave-active
  display: none
.flip-enter, .flip-leave
  transform: rotateY(180deg)
  opacity: 0
</style>
