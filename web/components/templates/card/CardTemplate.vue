<template lang="html">
  <section :class="attr['card']">
    <div :class="attr['card__container']">
      <div :class="attr['card__container-top']">
        <nuxt-img
          :src="payload.images.path"
          :alt="payload.images.alt"
        />
      </div>
      <div :class="attr['card__container-bottom']">
        <nuxt-img
          :class="attr['card__container-bottom__img']"
          :src="payload.mobile_images.path"
          :alt="payload.mobile_images.alt"
        />
        <div :class="attr['card__container-bottom__rating']">
          <span :class="attr['card__container-bottom__rating-type']">
            Score
          </span>
          <h3 :class="attr['card__container-bottom__rating-rate']">
            {{ payload.rating.score }}
          </h3>
          <p :class="attr['card__container-bottom__rating-vote']">
            {{ payload.rating.voted }} Votes
          </p>
        </div>
        <div :class="attr['card__container-bottom__detail']">
          <h2 :class="attr['card__container-bottom__detail-title']">
            {{ payload.title }}
          </h2>
          <div
            :class="attr['card__container-bottom__detail-excerpt']"
            v-html="payload.excerpt"
          ></div>
          <div :class="attr['card__container-bottom__detail-other']">
            <span
              :class="[
                attr['card__container-bottom__rating-type'],
                attr['card__container-bottom__rating-type--info']
              ]"
            >
              Category
            </span>

            <div
              :class="attr['card__container-bottom__detail-other__category']"
            >
              <nuxt-link
                :to="`/anime?category=${data.slug}`"
                v-for="(data, key) in payload.category"
                :class="
                  attr['card__container-bottom__detail-other__category-item']
                "
              >
                {{ data.title }}
              </nuxt-link>
            </div>
            <div :class="attr['card__container-bottom__detail-other__date']">
              <h3>
                Release Date:
                <span>
                  {{ $moment(payload.aired).format('MMM. DD, YYYY') }}
                </span>
              </h3>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
  export default {
    props: {
      payload: {
        type: Array / Object,
        default: null
      }
    }
  }
</script>

<style lang="stylus" module="attr">
  .card
    position: relative
    &__container
      cursor: pointer
      color: var(--theme_black)
      &:hover
        color: var(--theme_primary)
      &-top
        img
          height: 320px
          object-fit: cover
          object-position: top center
      &-bottom
        position: relative
        padding: 20px
        &__img
          position: absolute
          top: -90px
          left: 20px
          height: 180px
          width: 160px
          object-fit: cover
          object-position: center
        &__rating
          position: absolute
          top: 10px
          left: 190px
          width: 120px
          &-type
            padding: 2px 8px
            border-radius: 25px
            background-color: var(--theme_primary)
            font-size: 16px
            color: var(--theme_white)
            &--info
              background-color: var(--theme_tertiary)
          &-rate
            font-size: 32px
            font-weight: var(--bold)
          &-vote
            font-size: 14px
        &__detail
          padding-top: 90px
          &-title
            padding-bottom: 20px
            font-size: 32px
            font-weight: var(--bold)
            line-hieght: 1.4
            display: -webkit-box
            -webkit-box-orient: vertical
            overflow: hidden
            word-break: break-all
            text-overflow: ellipsis
            -webkit-line-clamp: 2
          &-excerpt
            margin-bottom: 20px
            font-size: 18px
            line-height: 1.4
            display: -webkit-box
            -webkit-box-orient: vertical
            overflow: hidden
            word-break: break-all
            text-overflow: ellipsis
            -webkit-line-clamp: 5
          &-other
            &__category
              display: flex
              flex-flow: row wrap
              padding-top: 10px
              &-item
                margin-right: 10px
                margin-bottom: 10px
                padding: 2px 8px
                border-radius: 25px
                color: var(--theme_primary)
                border: 1px solid var(--theme_black)
                transition: 0.4s ease-in-out
                &:hover
                  background-color: var(--theme_primary)
                  color: var(--theme_white)
                  border: 1px solid var(--theme_primary)
            &__date
              padding-top: 10px
              h3
                display:flex
                align-items: center
                font-size: 16px
                span
                  margin-left: 15px
  /**
   * Responsive
   */

  @media (max-width: 1024px) and (min-width: 280px)
    .card
      &__container
        &-bottom
          &__detail
            padding-top: 90px
            &-title
              font-size: 24px
            &-excerpt
              font-size: 16px
</style>
