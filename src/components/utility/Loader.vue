<template>
    <div class="loader" v-show="visible">
        <div class="spinner"></div>
    </div>
</template>

<script>
export default {
  name: "Loader",
  components: {},
  props: {
    visible: { type: Boolean }
  },
  watch: {},
  created(){},
  computed: {},
  methods: {}
};
</script>

<style lang="scss">
.loader {
  display: flex;
  justify-content: center;
  align-items: center;
}

.spinner {
  height: 5vh;
  width: 5vh;
  border: 6px solid $loader-spinner-blue;
  border-top-color: $loader-spinner-border-blue;
  border-radius: 100%;
  animation: rotation 0.6s infinite linear 0.25s;
  opacity: 0;
}

@keyframes rotation {
  from {
    opacity: 1;
    transform: rotate(0deg);
  }
  to {
    opacity: 1;
    transform: rotate(359deg);
  }
}
</style>