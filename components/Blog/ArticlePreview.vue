<template>
  <div class="preview my-8 flex flex-wrap lg:flex-no-wrap">
    <nuxt-link tag="a" :to="articleLink" class="thumbnail">
      <appImage v-if="article.thumbnail" :image="article.thumbnail" size="medium" />
      <img v-else :src="placeholderImage" />
    </nuxt-link>
    <div class="flex-grow">
      <h3 class="uppercase py-2 lg:pt-0 text-sm">
        <span v-for="(topic, index) in article.topics" :key="topic.id">
          {{ topic['title_' + $i18n.locale] }}{{ index != Object.keys(article.topics).length - 1 ? ', ' : ''}}
        </span>
      </h3>
      <nuxt-link :to="articleLink">
        <h2 class="mb-4 text-3xl">{{ article.title }}</h2>
      </nuxt-link>
      <p v-if="article.excerpt">{{article.excerpt}}</p>
      <p v-else>{{article.body | truncate(200) }}</p>
      <nuxt-link :to="articleLink"
        class="block py-4 text-josa-blue font-bold ltr:text-sm rtl:text-base hover:opacity-75">
        {{ $t('meta.readTheReport') }}
        <font-awesome-icon class="ltr:ml-2 rtl:mr-2 align-middle" :icon="['fas', arrowIcon ]" />
      </nuxt-link>
    </div>
  </div>
</template>

<script>
  import appImage from '~/components/UI/appImage';
  export default {
    name: 'BlogPreview',
    data() {
      return {
        placeholderImage: process.env.baseUrl + '/uploads/josabots_88f0a93786.jpeg'
      }
    },
    components: {
      appImage
    },
    props: {
      article: {
        type: Object,
        required: true
      }
    },
    computed: {
      articleLink() {
        const slug = this.$options.filters.stringToSlug(this.article.title)
        return this.localePath('/blog/' + this.article.id + '/' + slug)
      },
      arrowIcon() {
        if (this.$i18n.locale == "ar") {
          return 'long-arrow-alt-left'
        } else {
          return 'long-arrow-alt-right'
        }
      }
    }
  }

</script>

<style scoped>
  [lang="en"] p {
    @apply leading-normal;
  }

  [lang="ar"] p {
    @apply leading-normal;
  }

</style>
