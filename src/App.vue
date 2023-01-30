<template>
  <button @click="showToast = true">Show Toast</button>
  <s-toast title="Success!" message="Message has been sent." :show="showToast" @hide="handleHide"/>
</template>

<script>

import SToast from "@/components/toast/SToast.vue";

export default {
  name: 'App',
  components: {
    SToast
  },
  data() {
    return {
      showToast: false
    }
  },
  methods: {
    handleHide() {
      this.showToast = false
    }
  }

}
</script>