<template>
  <div>
    <button class="btn btn-success" data-bs-toggle="modal" data-bs-target="#exampleModal">Generate</button>
  </div>

  <AiPromtModal ref="promtModal" @keep="keep" @generate-text="generate" :suggestion="suggestion"/>
</template>

<script>
import AiPromtModal from "@/components/AiPromtModal"
import axios from "axios";

export default {
  name: "AiPromt",
  components: {
    AiPromtModal,
  },
  data() {
    return {
      suggestion: '',
    }
  },
  methods: {
    async generate(promt) {
      console.log(promt)
      let data = {
        "model": `${process.env.VUE_APP_CHATGPT_MODEL}`,
        "messages": [
          {
            "role": "user",
            "content": promt
          }
        ],
        "temperature": 0.2
      }
      let headers = {
        Authorization: `Bearer ${process.env.VUE_APP_CHATGPT_TOKEN}`
      }
      try {
        let response =  await axios.post('https://api.openai.com/v1/chat/completions', data, { headers: headers })

        this.suggestion = response.data?.choices[0]?.message?.content
      } catch (e) {
        console.log(e);
      }
    },

    keep() {
      this.$emit('changeText', this.suggestion)
      this.$refs.promtModal.hide()
    }
  },
  computed: {

  }
}
</script>

<style scoped>

</style>