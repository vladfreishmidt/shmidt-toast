<template>
  <div class="toast" v-if="show">
    <div class="toast-icon">
      <icon-success />
    </div>
    <div class="toast-content">
      <div class="toast-title">
        {{ title }}
      </div>
      <div class="toast-message">
        {{ message }}
      </div>
    </div>
    <button @click="hideToast" class="toast-button">&times;</button>
  </div>
</template>

<script>
import IconError from "@/components/icons/IconError.vue";
import IconWarning from "@/components/icons/IconWarning.vue";
import IconSuccess from "@/components/icons/IconSuccess.vue";
export default {
  name: 'SToast',
  components: { IconError, IconWarning, IconSuccess },
  emits: ['hide'],
  props: ['title', 'message', 'show'],
  data() {
    return {
      timeout: null,
    }
  },
  methods: {
    hideToast() {
      this.$emit('hide');
    }
  },
  watch: {
    show() {
      if (this.timeout) {
        clearTimeout(this.timeout);
      }
      this.timeout = setTimeout(() => {
        this.hideToast();
      }, 3000)
    }
  }
}
</script>

<style scoped>
  .toast {
    width: 300px;
    background-color: #ecfdf5;
    display: flex;
    justify-content: space-around;
    align-items: center;
    padding: 1rem;
    box-shadow: 1px 5px 10px -5px rgba(0, 0, 0, .2);
    position: relative;
  }

  .toast::before {
    content: "";
    width: 4px;
    height: 100%;
    background: #34d399;
    position: absolute;
    top: 0;
    left: 0;
  }

  .toast-icon {
    width: 16px;
    height: 16px;
    background-color: #34d399;
    border-radius: 50%;
    padding: 7px;
  }

  .toast-icon svg {
    fill: #ecfdf5;
  }

  .toast-content {
    flex-grow: 1;
    margin: 0 1rem;
  }

  .toast-title {
    font-weight: 700;
    margin-bottom: 0.5rem;
  }

  .toast-message {
    font-size: 14px;
    color: #6b7280;
  }

  .toast-button {
    width: 1.5rem;
    height: 1.5rem;
    border: none;
    padding: 0;
    color: #9ca3af;
    opacity: 0.7;
    background: transparent;
    cursor: pointer;
    font-size: 1em;
  }

  .toast-button:hover {
    opacity: 1;
  }
</style>