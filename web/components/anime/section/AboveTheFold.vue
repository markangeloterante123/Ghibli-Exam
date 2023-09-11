<template lang="html">
  <section :class="attr['fold']">
    <!-- Content  -->
    <container-template>
      <div :class="attr['fold__container']">
        <div :class="attr['fold__container-left']">
          <h2
            v-if="getMobile"
            :class="attr['fold__container-left__title']"
          >
            {{ above_the_fold.title }}
          </h2>
          <nuxt-img
            v-if="!getMobile"
            :src="above_the_fold.mobile_images.path"
            :alt="above_the_fold.mobile_images.alt"
          />
          <nuxt-img
            v-else
            :src="above_the_fold.images.path"
            :alt="above_the_fold.images.alt"
          />
          <div :class="attr['fold__container-left__score']">
            <div :class="attr['fold__container-left__score-content']">
              <span>Score</span>
              <p :class="attr['fold__container-left__score-content__score']">
                {{ above_the_fold.rating.score }}
              </p>
              <p :class="attr['fold__container-left__score-content__voted']">
                {{ above_the_fold.rating.voted }} Voted
              </p>
            </div>
          </div>
          <div :class="attr['fold__container-left__category']">
            <template v-for="(data, key) in above_the_fold.category">
              <span>{{ data.title }}</span>
            </template>
          </div>
          <div :class="attr['fold__container-left__info']">
            <h3 :class="attr['fold__container-left__info-item']">
              <strong>Type:</strong>
              {{ above_the_fold.type.name }}
            </h3>
            <h3 :class="attr['fold__container-left__info-item']">
              <strong>Aired:</strong>
              {{ $moment(above_the_fold.aired).format('MMM. DD, YYYY') }}
            </h3>
            <h3 :class="attr['fold__container-left__info-item']">
              <strong>Duration:</strong>
              {{ above_the_fold.duration }}
            </h3>
            <h3 :class="attr['fold__container-left__info-item']">
              <strong>Status:</strong>
              {{ above_the_fold.status.name }}
            </h3>
          </div>
        </div>
        <div :class="attr['fold__container-right']">
          <h2
            v-if="!getMobile"
            :class="attr['fold__container-right__title']"
          >
            {{ above_the_fold.title }}
          </h2>
          <iframe
            :class="attr['fold__container-right__video']"
            :src="`https://www.youtube.com/embed/${above_the_fold.youtube_id}?rel=0`"
            frameborder="0"
            allow="encrypted-media"
            allowfullscreen
          ></iframe>
          <div
            :class="attr['fold__container-right__description']"
            v-html="above_the_fold.excerpt"
          ></div>
        </div>
      </div>
    </container-template>
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
    padding-bottom: 80px
    &__container
      display: flex
      flex-flow: row wrap
      margin: -15px
      padding-top: 120px
      &-left
        flex: 0 0 calc(30% - 30px)
        margin: 0 15px
        &__title
          padding-bottom: 10px
          font-size: 32px
          font-weight: var(--bold)
        &__score
          padding: 20px 0
          &-content
            span
              padding: 2px 8px
              border-radius: 25px
              color: var(--theme_white)
              background-color: var(--theme_primary)
            &__score
              font-size: 42px
              font-weight: var(--bold)
              color: var(--theme_primary)
            &__voted
              font-size: 14px
        &__category
          display: flex
          flex-flow: row wrap
          padding-bottom: 20px
          span
            margin: 5px
            padding: 2px 8px
            border-radius: 25px
            background-color: var(--theme_white)
            border: 1px solid var(--theme_black)
            transition: 0.4s ease-in-out
            cursor: pointer
            &:hover
              background-color: var(--theme_primary)
              border: 1px solid var(--theme_primary)
              color: var(--theme_white)
        &__info
          &-item
            font-size: 18px
            color: var(--theme_primary)
            strong
              font-weight: var(--bold)
              color: var(--theme_black)
      &-right
        flex: 0 0 calc(70%- 30px)
        margin: 0 15px
        &__title
          padding-bottom: 10px
          font-size: 52px
          line-height: 1.2
          font-weight: var(--bold)
          color: var(--theme_black)
        &__video
          margin-bottom: 30px
          width: 100%
          height: 420px
        &__description
          font-size: 18px
          color: var(--theme_black)
          line-height: 1.4
  @media (max-width: 820px) and (min-width: 280px)
    .fold
      &__container
        &-left,
        &-right
          flex: 0 0 calc(100% - 30px)
        &-left
          padding-bottom: 30px
          img
            max-height: 480px
            object-fit: cover
            object-position: center
</style>
