<template>
  <li class="">
    <span class="p-1">{{ name }}</span>
  </li>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      default: 'Null'
    },
    rank: {
      type: Number,
      default: -1
    }
  }
}
</script>
