<template>
  <div>
    <appImage class="mb-4 image" v-if="program.picture" :image="program.picture" />
    <nuxt-link :to="programLink">
      <h3 class="text-3xl">
        {{ program['title_' + $i18n.locale] ? program['title_' + $i18n.locale] : program['title_en'] }}</h3>
    </nuxt-link>
    <p class="my-4">
      {{ program['description_' + $i18n.locale] ? program['description_' + $i18n.locale] : program['description_en']}}
    </p>
    <nuxt-link :to="programLink" class="block text-josa-blue font-bold ltr:text-sm rtl:text-base hover:opacity-75">
      {{ $t('meta.readMore') }} ></nuxt-link>
  </div>
</template>

<script>
  import appImage from '~/components/UI/appImage';
  export default {
    components: {
      appImage
    },
    props: {
      program: {
        type: Object,
        required: true
      },
    },
    computed: {
      programLink() {
        var title = ''
        if (this.program['title_' + this.$i18n.locale]) {
          title = this.program['title_' + this.$i18n.locale]
        } else {
          title = this.program.title_en
        }
        const slug = this.$options.filters.stringToSlug(title)
        return this.localePath('/programs/' + this.program.id + '/' + slug)
      }
    }
  }
</script>

<style scoped>
  .image {
    width: 125px;
  }

  h3 {
    @apply font-bold;
  }
</style>