<template lang="html">
  <main
    :class="attr['page']"
    v-if="loaded"
  >
    <!-- Page Content -->
    <page-content />
  </main>
</template>

<script>
  import { mapGetters } from 'vuex'
  import { computed } from 'vue'
  export default {
    components: {
      PageContent: () => import('~/components/home/PageContent')
    },
    data: () => ({
      loaded: false,
      records: null,
      page: {
        title: 'Ghibli Movies'
      }
    }),
    computed: {
      ...mapGetters({
        getContents: 'global/content/getStories'
      })
    },
    provide() {
      return {
        above_the_fold: {
          title: 'Watch our latest in Ghibli studio',
          excerpt:
            'Stay tune and be updated to our new released anime this comming winter season.',
          images: {
            path: '/banner/banner-images.jpg',
            alt: 'banner-image'
          },
          button: {
            label: 'Watch latest Movie',
            path: '/',
            template: 'primary',
            action_type: 'router'
          }
        },
        records: computed(() => this.getContents)
      }
    },
    mounted() {
      setTimeout(() => {
        this.toggleModalStatus({
          type: 'loader',
          status: true,
          item: { start: false }
        })
        this.loaded = true
      }, 500)
    },

    asyncData({ $axios, store, error }) {
      store.commit('global/modal/toggleModalStatus', {
        type: 'loader',
        status: true,
        item: { start: true }
      })

      // return $axios
      //   .$get('web/calendar')
      //   .then(({ records }) => ({
      //     records: records
      //   }))
      //   .catch(() => {
      //     error({ statusCode: 500 })
      //   })
    },
    head() {
      let host = process.env.BASE_URL

      return {
        title: `Ghibli | ${this.page.title}`,
        link: [
          {
            rel: 'canonical',
            href: `${host}${this.$route.fullPath}`
          }
        ]
        // meta: [
        //   { hid: 'description', name: 'description', content: `${this.page.metadata.meta_description}` },
        //   { hid: 'og:title', property: 'og:title', content: `${this.page.metadata.meta_title}` },
        //   { hid: 'og:description', property: 'og:description', content: `${this.page.metadata.meta_description}` },
        //   { hid: 'og:url', property: 'og:url', content: `${host}${this.$route.fullPath}` },
        //   { hid: 'og:image', property: 'og:image', content: `${host}/logo.svg` },
        //   { hid: 'og:image:alt', property: 'og:image:alt', content: this.page.title },
        //   { hid: 'og:type', property: 'og:type', content: 'website' },
        //   { hid: 'og:site_name', property: 'og:site_name', content: 'C! Magazine' },
        // ]
      }
    }
  }
</script>
<style lang="stylus" module="attr">
  .page
    //
</style>
