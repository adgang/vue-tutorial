<template>
  <div class="about">
    <h1>{{ msg }}</h1>
  </div>
</template>
<script>
export default {
  name: 'about',
  props: ['msg'],
  data () {
    return {
      msg: 'This is the About page. Really its just a fun experimental app'
    }
  }
}
</script>
