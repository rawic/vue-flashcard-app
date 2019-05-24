<template>
  <div class="addcard-box" :class="{ '-showerror': error }">
    <div class="form-box">
      <label>
        <input
          v-model="front"
          :class="{ '-error': error }"
          type="text"
          class="input"
          placeholder="Front"
        />
      </label>
      <label>
        <input
          @keypress.enter="addCard"
          v-model="back"
          type="text"
          class="input"
          :class="{ '-error': error }"
          placeholder="Back"
        />
      </label>
      <button @click="addCard()" type="button" class="addcard">
        Add a new card
      </button>
    </div>
    <!-- end of add card box -->
    <span :class="{ '-show': error }" class="error"
      >Oops! Flashcards must be completed with a front and back field.</span
    >
  </div>
</template>

<script>
const uuidv4 = require("uuid/v4");
const colors = ["-orange", "-red", "-purple", "-blue", "-green"];

export default {
  name: "AddNewCard",
  data() {
    return {
      front: "",
      back: "",
      error: false
    };
  },
  methods: {
    addCard() {
      if (!this.front || !this.back) {
        this.error = true;
      } else {
        const card = {
          id: uuidv4(),
          front: this.front,
          back: this.back,
          flipped: false,
          liked: false,
          color: `${colors[Math.floor(Math.random() * colors.length)]}`
        };
        this.$emit("addCardTrigger", card);
        this.front = "";
        this.back = "";
        this.error = false;
      }
    }
  }
};
</script>

<style scoped lang="sass">
@import 'src/assets/sass/_variables.sass';

.addcard-box
  margin-top: 40px
  margin-bottom: .5rem
  transition: margin-bottom .3s
  &.-showerror
    margin-bottom: 2rem
    .error
      opacity: 1
      visibility: visible
  .error
    margin-top: 15px
    display: block
    font-size: 0.8571rem
    color: red
    opacity: 0
    transition: all .5s
    visibility: hidden
    line-height: 1.4

.form-box
  display: flex
  justify-content: center
  @media (max-width: 700px)
    flex-direction: column
    align-items: center
    label
      max-width: 300px
      width: 100%
  .input, .addcard
    padding-left: 20px
    padding-right: 20px
    height: 40px
    border-width: 1px
    border-style: solid
    border-radius: $radius
    display: inline-block
    @media (max-width: 700px)
      max-width: 300px
      width: 100%
  .input
    border-color: $input-border
    font-size: 1.071rem
    color: $muted
    transition: border-color .3s
    @media (min-width: 701px)
      margin-right: 1.3rem
    @media (max-width: 700px)
      margin-bottom: 1rem
    &:hover
      border-color: darken($input-border, 20%)
    &.-error
      border-color: red
    &:not(.-error):focus
      border-color: $highlight

.addcard
  background-color: $highlight
  border-color: $highlight
  color: white
  box-shadow: 0 0 8px 1px rgba(96,69,255,0.28)
  transition: background-color .3s
  font-weight: $medium
  &:hover
    background-color: darken($highlight, 5%)
</style>
