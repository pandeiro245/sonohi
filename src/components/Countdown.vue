<template>
  <div id="countdown">
  <p>{{ targetDateStr }}からあと{{remain}}日。</p>
  </div>
</template>
<script>
  export default {
  name: 'countdown',
  props: ['targetDateStr', 'remain'],
  data () {
    return {
    }
  },
  methods: {
  }
}
</script>
