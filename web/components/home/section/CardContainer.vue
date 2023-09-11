<template lang="html">
  <section :class="attr['section']">
    <!-- Content  -->
    <container-template>
      <div :class="attr['section__container']">
        <div
          v-for="(payload, key) in paginatedItems"
          :key="key"
          :class="attr['section__container-card']"
        >
          <nuxt-link :to="`/anime/${payload.slug}`">
            <card-template :payload="payload" />
          </nuxt-link>
        </div>
      </div>

      <!-- Pagination -->
      <div :class="attr['section__pagination']">
        <span :class="attr['section__pagination-counter']">
          {{ currentPage }} / {{ totalPages }}
        </span>
        <div :class="attr['section__pagination-button']">
          <button
            @click="goToPage(currentPage - 1)"
            :disabled="currentPage === 1"
          >
            Previous
          </button>
          <span>|</span>
          <button
            @click="goToPage(currentPage + 1)"
            :disabled="currentPage === totalPages"
          >
            Next
          </button>
        </div>
      </div>
    </container-template>
    <!-- Simulate Static Pagination -->
  </section>
</template>

<script>
  export default {
    components: {
      CardTemplate: () => import('~/components/templates/card/CardTemplate')
    },
    data() {
      return {
        items: [], // Simulated data
        itemsPerPage: 4, // Items per page
        currentPage: 1 // Current page
      }
    },
    computed: {
      totalPages() {
        return Math.ceil(this.items.length / this.itemsPerPage)
      },
      paginatedItems() {
        const startIndex = (this.currentPage - 1) * this.itemsPerPage
        const endIndex = startIndex + this.itemsPerPage
        return this.items.slice(startIndex, endIndex)
      }
    },
    methods: {
      goToPage(page) {
        if (page >= 1 && page <= this.totalPages) {
          this.currentPage = page
        }
      }
    },
    inject: ['records'],
    mounted() {
      this.items = this.records
    }
  }
</script>
<style lang="stylus" module="attr">
  .section
    position: relative
    margin: 80px 0 180px
    &__pagination
      display: flex
      position: relative
      justify-content: center
      margin-top: 20px
      &-counter
        position: absolute
        left: calc(50% - 10px)
        bottom: -20px
      &-button
        button
          cursor: pointer
          font-size: 16px
          font-weight: var(--bold)
    &__container
      display: flex
      flex-flow: row wrap
      margin: 0 -10px
      &-card
        flex: 0 0 calc((100% / 2) - 20px)
        margin: 0 10px 20px
        transition: 0.4s ease-in-out
        background-color: #f8f9fa
        border-radius: 10px
        overflow: hidden
        &:hover
          color: var(--theme_primary)
          box-shadow: 0px 6px 21px 0px rgba(0,0,0,0.75)

    @media (max-width: 768px) and (min-width: 280px)
      .section
        &__container
          &-card
            flex: 0 0 calc(100% - 20px)
</style>
