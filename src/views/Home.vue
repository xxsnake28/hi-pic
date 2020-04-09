<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <upload-field></upload-field>
  </div>
</template>

<script>
// @ is an alias to /src
import UploadField from '@/components/Home/UploadField.vue'

export default {
  name: 'home',
  components: {
    UploadField
  }
}
</script>
