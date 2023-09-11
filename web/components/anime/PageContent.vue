<template lang="html">
  <section :class="attr['page']">
    <!-- Above the fold -->
    <above-the-fold />
  </section>
</template>

<script>
  export default {
    components: {
      AboveTheFold: () => import('~/components/anime/section/AboveTheFold')
      // CardContainer: () => import('~/components/home/section/CardContainer')
    }
  }
</script>
<style lang="stylus" module="attr">
  .page
    //
</style>
