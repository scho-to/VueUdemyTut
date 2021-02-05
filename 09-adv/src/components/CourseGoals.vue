<template>
  <ul>
    <li v-for="gloa in goals" :key="gloa">
      <slot :item="gloa" another-prop="..."></slot>
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      goals: ['Finish the COurse', 'Learn Vue']
    }
  }
}
</script>