<template>
  <img :src="src">
</template>
<script>
import template from 'template-string'
  export default {
    props: ['api','id'],
    data () {
      return {
        src: null
      }
    },
    watch: {
      id () {
        if (this.id) {
          let xhr = new XMLHttpRequest()
          xhr.open('GET', template(this.api, {id: this.id}), true)
          xhr.onload = (e) => {
            if (xhr.status === 200) {
              let res = JSON.parse(xhr.response)
              this.src = res.message
            }
          }
          xhr.send()
        }
      }
    }
  }
</script>