<template lang="html">
  <section :class="attr['page']">
    <!-- Above the fold section -->
    <above-the-fold />
    <!-- Card Container -->
    <card-container />
  </section>
</template>

<script>
  export default {
    components: {
      AboveTheFold: () => import('~/components/home/section/AboveTheFold'),
      CardContainer: () => import('~/components/home/section/CardContainer')
    }
  }
</script>
<style lang="stylus" module="attr">
  .page
    //
</style>
