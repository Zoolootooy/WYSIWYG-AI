<template>
  <div>
    <AiPromt @change-text="changeText"/>
    <VueEditor v-model="mymodel" :editor-toolbar="customToolbar"/>
  </div>
</template>

<script>
import { VueEditor } from 'vue3-editor'
import AiPromt from "@/components/AiPromt"

export default {
  name: "MyEditor",
  components: {
    VueEditor,
    AiPromt
  },
  data() {
    return {
      mymodel: '',

      customToolbar: [
        ["bold", "italic", "underline"],
        [{list: "ordered"}, {list: "bullet"}],
        ['blockquote', 'link'],
        [{template: '<button><span>123</span></button>'}]
      ]
    }
  },
  methods: {
    changeText(newText) {

      this.mymodel = newText
    }
  }
}
</script>

<style scoped>

</style>