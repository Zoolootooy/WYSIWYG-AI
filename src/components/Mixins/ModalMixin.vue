<script>
export default {
  name: "ModalMixin",
  methods: {
    show() {
      this.$refs.showBtn.click()
    },

    hide() {
      this.$refs.hideBtn.click()
    },
  }
}
</script>
