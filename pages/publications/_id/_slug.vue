<template>
  <publicationSingle :publication="publication" />
</template>

<script>
  import axios from 'axios';
  import publicationSingle from '~/components/Publications/PublicationSingle';
  export default {
    layout: "default",
    asyncData(context) {
      return axios.get(process.env.baseUrl + '/publications/' + context.params.id)
        .then(res => {
          return {
            publication: res.data
          }
        })
        .catch(e => context.error(e))
    },
    components: {
      publicationSingle
    },
    head() {
      const i18nSeo = this.$nuxtI18nSeo()
      return {
        title: this.pageTitle + ' - ' + (this.$i18n.locale == 'ar' ? 'الجمعية الأردنية للمصدر المفتوح': 'Jordan Open Source Association'),
        meta: [{
            name: 'description',
            content: this.publication['excerpt_' + this.$i18n.locale] ? this.publication['excerpt' + this
              .$i18n.locale] : ''
          },
          ...this.$options.filters.ogTags('publication', this.publication, this.$route.path, this.$i18n.locale),
          ...i18nSeo.meta
        ]
      }
    },
    computed: {
      pageTitle() {
        return this.publication['title_' + this.$i18n.locale]
      }
    }
  };

</script>
