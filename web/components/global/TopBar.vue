<template lang="html">
  <nav
    id="__n"
    :class="[
      attr['nav'], //
      toggled_side_nav && attr['nav--active'],
      active_nav && attr['nav--sticky']
    ]"
  >
    <!-- Container Template -->
    <container-template :theme="'transparent'">
      <div :class="attr['nav__wrapper']">
        <div :class="attr['nav__wrapper-left']">
          <nuxt-link
            to="/"
            custom
            v-slot="{ navigate }"
          >
            <svg
              :class="[
                attr['nav__wrapper-left__img'],
                attr['nav--pointer'],
                toggled_side_nav && attr['nav__wrapper-left__img--active']
              ]"
              @click="navigate"
              id="Component_122_57"
              data-name="Component 122 – 57"
              xmlns="http://www.w3.org/2000/svg"
              width="45"
              height="45"
              viewBox="0 0 45 45"
            >
              <circle
                id="Ellipse_288"
                data-name="Ellipse 288"
                cx="22.5"
                cy="22.5"
                r="22.5"
                fill="#0099d8"
              />
              <path
                id="home_FILL1_wght400_GRAD0_opsz24"
                d="M160,232.875v-11.25L167.5,216l7.5,5.625v11.25h-5.625v-6.562h-3.75v6.563Z"
                transform="translate(-145 -202)"
                fill="#fff"
              />
            </svg>
          </nuxt-link>
        </div>
        <!-- Right -->
        <div :class="attr['nav__wrapper-right']">
          <div :class="attr['nav__wrapper-right__content']">
            <div
              :class="attr['nav__wrapper-right__content-burger']"
              @click="toggleSideNav()"
            >
              <div
                :class="[
                  attr['nav__wrapper-right__content-burger__bar'],
                  toggled_side_nav &&
                    attr['nav__wrapper-right__content-burger__bar-top']
                ]"
              ></div>
              <div
                :class="[
                  attr['nav__wrapper-right__content-burger__bar'],
                  attr['nav__wrapper-right__content-burger__bar--small'],
                  toggled_side_nav &&
                    attr['nav__wrapper-right__content-burger__bar-bottom']
                ]"
              ></div>
            </div>
            <span
              :class="[
                attr['nav__wrapper-right__content-label'],
                toggled_side_nav &&
                  attr['nav__wrapper-right__content-label--hide']
              ]"
            >
              <p
                @click="toggleSideNav()"
                v-if="!getMobile"
              >
                Contents
              </p>
            </span>
          </div>
        </div>
      </div>
    </container-template>
  </nav>
</template>

<script>
  import { mapGetters } from 'vuex'
  export default {
    components: {},
    data: () => ({
      toggle: {
        scroll: false,
        background: false,
        burger: false
      }
    }),
    methods: {
      toggleSideNav() {
        if (this.toggled_side_nav) {
          this.$store.commit('global/settings/TOGGLE_SIDENAV', false)
          document.body.classList.remove('no_scroll')
        } else {
          this.$store.commit('global/settings/TOGGLE_SIDENAV', true)
          document.body.classList.add('no_scroll')
        }
      },
      autoSpacer() {
        let nav = document.getElementById('__n'),
          nav_padding = nav.offsetHeight,
          root = document.querySelector(':root')
      },
      topBarSetter() {
        let path = this.$route.path
        switch (path) {
          case '/featured-projects':
            this.$store.commit('global/settings/ACTIVE_NAV', true)
            break
        }
      }
    },
    computed: {
      ...mapGetters({
        toggled_side_nav: `global/settings/getSideNavStatus`,
        active_nav: `global/settings/getActiveNavStatus`
      })
    },
    mounted() {
      setTimeout(() => {
        this.autoSpacer()
        let nav = document.querySelector('#__n')
        this.topBarSetter()

        document.body.style.setProperty('--topspace', nav.scrollHeight + 'px')
      }, 500)
    },
    created() {
      this.$nuxt.$on('nav-toggle', (type, status) => {
        this.toggle[type] = status
        setTimeout(
          () => {
            if (type === 'burger') {
              if (status) {
                document.body.classList.add('no_scroll')
              } else {
                document.body.classList.remove('no_scroll')
              }
            }
          },
          type === 'burger' ? 100 : 0
        )
      })
    },
    beforeDestroy() {
      this.$nuxt.$off('nav-toggle')
    },
    destroyed() {
      this.$nuxt.$off('nav-toggle')
    }
  }
</script>

<style lang="stylus" module="attr">
    .nav
      position: absolute
      top: 0
      left: 0
      right: 0
      z-index: 998
      transition: .3s ease-in-out
      background-color: transparent
      transition: 0.4s ease-in-out
      background-color: var(--theme_primary)
      &--sticky
        position: fixed
        background-color: var(--theme_white)
        box-shadow: 0px 13px 17px -7px rgba(0,0,0,0.2)
        & ^[0]__wrapper
          &-left
            & ^[0]__wrapper-left__span
              color: var(--theme_black)
            svg
              path
                fill: var(--theme_black)
          &-right
            & ^[0]__wrapper-right__content-burger__bar
              background-color: var(--theme_black)
            & ^[0]__wrapper-right__content-label
              color: var(--theme_black)
      &--pointer
        cursor: pointer
      &--active
        background-color: var(--theme_white)
        box-shadow: 0px 13px 17px -7px rgba(0,0,0,0.2)
      &__wrapper
        position: relative
        display: flex
        flex-flow: row wrap
        align-items: center
        justify-content: space-between
        margin: 0 -15px
        padding: 10px 0
        &-left
          flex: 0 0 calc(50% - 30px)
          margin: 0 15px
          &__img
            width: 50px
            height 50px
            &--active
              path
                fill: var(--theme_black)
            circle
              fill: transparent
              transition: 0.4s ease-in-out
            &:hover
              circle
                fill: #0099d8
          &__span
            margin: 0 0 0 15px
            font-size: 28px
            color: var(--theme_white)
            &--active
              color: var(--theme_black)
        &-right
          display: flex
          justify-content: flex-end
          flex: 0 0 calc(50% - 30px)
          margin: 0 15px
          &__content
            display: flex
            align-items: center
            &-burger
              position: relative
              width: 30px
              height: 22px
              display: flex
              flex-flow: row wrap
              align-items: center
              transition: 0.4s ease-in-out
              cursor: pointer
              &__bar
                width: 100%
                height: 3px
                background-color: var(--theme_white)
                transition: .3s ease-in-out
                &--small
                  width: 60%
                  margin: 0 0 0 auto
                &-top
                  top: 50%
                  width: 60%
                  background-color: var(--theme_black)
                  transform: translateX(12px) translateY(4px) rotate(-135deg)
                &-bottom
                  bottom: 50%
                  width: 60%
                  background-color: var(--theme_black)
                  transform: translateY(-7px) rotate(135deg)
            &-label
              padding-left: 10px
              font-size: 16px
              color: var(--theme_white)
              &--hide
                opacity: 0
  /**
  * Mobile Responsive
  */
  @media (max-width: 1024px) and (min-width: 280px)
    .nav
      &__wrapper
        &-right
          margin: 0
</style>
