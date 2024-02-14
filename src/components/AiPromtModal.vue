<template>
  <div class="d-inline-block" data-bs-toggle="modal" :data-bs-target="`#AiPromtModal`" ref="showBtn">
    <slot name="modal-show-button"></slot>
  </div>

  <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title fs-5" id="exampleModalLabel">Generate Text</h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          <button type="button" data-bs-dismiss="modal"  ref="hideBtn" hidden>Hide</button>
        </div>
        <div class="modal-body">
          <div class="container">
            <div class="row">
              <div class="col-12">
                <label for="promt-area">Features and keywords</label>
                <textarea name="" id="promt-area" cols="20" rows="4" class="form-control" v-model="promt"></textarea>
              </div>
            </div>

            <div class="row mt-3">
              <div class="col-12">
                <button class="btn btn-success" @click="$emit('generateText', promt)" :disabled="disableGenerateBtn">Generate</button>
              </div>
            </div>

            <div v-if="suggestion" class="row mt-3">
              <div class="col-12">
                Sugession:
                <p>{{suggestion}}</p>
              </div>
            </div>
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
          <button type="button" class="btn btn-primary" @click="$emit('keep')">Keep</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ModalMixin from "@/components/Mixins/ModalMixin";

export default {
  name: "AiPromtModal",
  mixins: [
    ModalMixin,
  ],
  props: {
    suggestion: {
      type: String,
    }
  },
  data() {
    return {
      promt: '',
    }
  },
  methods: {
  },
  computed: {
    disableGenerateBtn() {
      return !this.promt.length > 0
    }
  }
}
</script>

<style scoped>

</style>