<template>
  <div class="field">
    <label class="label">{{label}}</label>
    <div class="control">
      <div class="select centered">
        <select ref="dropdown" @change="change">
          <option v-for="item in list">{{item}}</option>
        </select>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    props: ['api', 'label'],
    data () {
      return {
        list: []
      }
    },
    methods: {
      change: function () {
        this.$emit('change', this.$refs.dropdown.value)
      }
    },
    mounted () {
      let xhr = new XMLHttpRequest()
      xhr.open('GET', this.api, true)
      xhr.onload = (e) => {
        if (xhr.status === 200) {
          let res = JSON.parse(xhr.response)
          this.list = res.message
        }
      }
      xhr.send()
    }
  }
</script>