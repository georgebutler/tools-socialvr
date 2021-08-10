<template>
  <div class="">
    <input type="checkbox">
    <span class="p-1"><strong>{{ speaker }}</strong> spoke for a total of {{ duration }} seconds.</span>
  </div>
</template>

<script>
export default {
  props: {
    speaker: {
      type: String,
      default: 'Null'
    },
    duration: {
      type: Number,
      default: 0
    }
  }
}
</script>
