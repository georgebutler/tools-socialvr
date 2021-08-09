<template>
  <div class="">
    <input type="checkbox">
    <span class="p-1"><strong>{{ speaker }}</strong> spoke for {{ duration }} seconds.</span>
  </div>
</template>

<script>
export default {
  props: {
    speaker: {
      type: String,
      default: 'Unknown'
    },
    duration: {
      type: Number,
      default: 0
    }
  }
}
</script>
