<template>
  <Modal :open="open" @close="$emit('close')">
    <div class="modal-body px-4">
      <h2 class="mb-5">Select wallet</h2>
      <button
        class="d-flex text-left mb-7 button button-select"
        @click="service = !service ? 'metamask' : ''"
        :class="{ active: service === 'metamask' }"
      >
        <span class="flex-auto">MetaMask</span>
        <img src="~/@/assets/metamask.svg" height="30" class="mt-2 pt-1" />
      </button>
      <div class="d-flex mb-2">
        <button class="button button-outline col-6 mr-2" @click="$emit('close')">Cancel</button>
        <button
          class="button button-primary col-6 ml-2"
          @click="handleLogin"
          :disabled="!service || isLoading"
        >
          <VueLoadingIndicator v-if="isLoading" class="big" />
          <template v-else>Confirm</template>
        </button>
      </div>
    </div>
  </Modal>
</template>

<script>
import { mapActions } from 'vuex';

export default {
  props: ['open'],
  data() {
    return {
      isLoading: false,
      service: ''
    };
  },
  methods: {
    ...mapActions(['login']),
    async handleLogin() {
      this.isLoading = true;
      await this.login();
      this.$emit('close');
    }
  }
};
</script>
