<template lang="html">
  <section :class="attr['fold']">
    <!-- Content  -->
    <container-template>
      <div :class="attr['fold__top']">
        <h1 :class="attr['fold__top-title']">
          {{ above_the_fold.title }}
        </h1>
        <p :class="attr['fold__top-excerpt']">
          {{ above_the_fold.excerpt }}
        </p>
        <button-template
          :payload="{
            link: above_the_fold.button.path,
            action_type: above_the_fold.button.action_type,
            with_icon: false
          }"
          :template="above_the_fold.button.template"
        >
          {{ above_the_fold.button.label }}
        </button-template>
      </div>
    </container-template>
    <!-- Banner Image -->
    <nuxt-img
      :class="attr['fold__banner']"
      :src="above_the_fold.images.path"
      :alt="above_the_fold.images.alt"
    />
  </section>
</template>

<script>
  export default {
    inject: ['above_the_fold']
  }
</script>
<style lang="stylus" module="attr">
  .fold
    position: relative
    height: 580px
    &:before
      content: ''
      position: absolute
      top: 0
      left: 0
      right: 0
      bottom: 0
      background-color: rgba(0,0,0, 0.5)
      z-index: -1
    &__top
      padding-top: 180px
      z-index: 2
      color: var(--theme_white)
      &-title
        padding-bottom: 10px
        max-width: 480px
        font-size: 52px
        font-weight: var(--bold)
        line-hieght: 1.2
      &-excerpt
        padding-bottom: 30px
        max-width: 520px
        font-size: 22px
        font-weight: var(--med)
        line-height: 1.4
    &__banner
      position: absolute
      top: 0
      left: 0
      right: 0
      bottom: 0
      max-height: 580px
      object-fit: cover
      object-position: 80% 80%
      z-index: -2
  @media (max-width: 1024px) and (min-width: 280px)
    .fold
      &__banner
        height: 100%
        max-height: unset
      &__top
        &-title
          font-size: 32px
        &-excerpt
          font-size: 16px
</style>
