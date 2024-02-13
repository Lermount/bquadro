<template>
  <div class="container">
    <button class="btn btn-primary mt-4" @click="showModal">Открыть форму обратной связи</button>
    <Form v-if="showFeedbackForm" @close-modal="closeModal" />
  </div>
</template>

<script>
import Form from '@/components/feedBackForm.vue';

export default {
  data() {
    return {
      showFeedbackForm: false,
    };
  },
  components: { Form },

  methods: {
    showModal() {
      this.showFeedbackForm = true;
    },
    closeModal() {
      this.showFeedbackForm = false;
    },
  },


};
</script>