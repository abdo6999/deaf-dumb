<template>
  <Teleport to="#app">
    <Transition>
      <div v-if="show" @click="closeContent" class="overlay position-fixed top-0 end-0 bottom-0 start-0"></div>
    </Transition>
  </Teleport>
  <Transition>
    <div v-if="show" class="content rounded p-3 position-fixed start-50">
      <img  :src="imgSrc"  :alt="`${letter} sign language image`"  class="w-100 mt-5"  />
      <div class="close-btn w-100 position-absolute top-0 end-0 rounded-top">
        <span @click="closeContent" class="close-icon">
          <font-awesome-icon icon="fa-regular fa-circle-xmark" class="fs-4" />
        </span>
      </div>
      <div class="letter position-absolute">
        <span class="fw-bold">{{ letter }}</span>
      </div>
    </div>
  </Transition>
</template>

<script>
export default {
  props: ['show', 'letter', 'imgSrc'],
  emits: ['close-content'],
  data() {
    return {
    }
  },
  methods: {
    closeContent() {
      this.$emit('close-content', false)
    }
  }
}
</script>


<style lang="scss" scoped>
@import "@/scss/custom.scss";
.overlay {
  background-color: rgba(0, 0, 0, 0.5);
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease-in-out;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
.content {
    width: 60%;
    height: 500px;
    background-color: white;
    box-shadow: 0 1px 5px 2px rgb(0 0 0 / 10%);
    transform: translate(-50%, -50%);
    z-index: 1111;
    top: 55%;

    img {
      height: 420px;
    }
  }
  .close-btn {
    // cursor: pointer;
    // width: 100%;
    text-align: end;
    padding: 1rem;
    background-color: white;
    box-shadow: 0px 1px 4px 3px rgb(0 0 0 / 10%);

    .close-icon {
      cursor: pointer;

      svg {
        transition: all 0.3s ease-in-out;

        &:hover {
          color: orangered;
        }
      }
    }

  }
  .letter {
    top: 5%;
    left: 6%;

    span {
      font-size: 9rem;
      color: #bde910;
    }
  }

  @include media-breakpoint-down(lg) {
    .content {
      width: 90%;
      height: 400px;
      top: 60%;
      
      img {
        height: 90%;
      }
      .letter {
        top: 12%;
        left: 6%;
        span {
          font-size: 6rem;
        }
      }
    }
  }
</style>