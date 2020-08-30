<template>
  <div
      class="pane"
      v-show="isShow"
  >
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "pane",
  props: {
    label: {
      type: String,
      default: ''
    },
    closeable: {
      type: Boolean,
      default: false
    }
  },
  data: () => {
    return {
      isShow: true,
    }
  },
  methods: {
    init() {
      this.$parent.init()
    }
  },
  watch: {
    label() {
      this.init()
    }
  },
  mounted() {
    this.init()
  }
}
</script>

<style scoped>
.pane {
  margin-top: 26px;
  font-size: 16px;
  line-height: 24px;
  color: #333;
  text-align: justify;
}
</style>