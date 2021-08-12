<template>
  <AisInstantSearchSsr>
    <AisSearchBox />
  </AisInstantSearchSsr>
</template>

<script>
export default {
  layout() {
    return "BasicLayout";
  },
  serverPrefetch() {
    return this.instantsearch.findResultsState(this).then(algoliaState => {
      this.$ssrContext.nuxt.algoliaState = algoliaState;
    });
  },
  beforeMount() {
    const results =
      this.$nuxt.context.nuxtState.algoliaState || window.__NUXT__.algoliaState;
    this.instantsearch.hydrate(results);
  },
  data() {
    const mixin = createServerRootMixin({
      searchClient,
      indexName,
      routing: {
        router: nuxtRouter(this.$router)
      }
    });
    return {
      ...mixin.data()
    };
  },
  provide() {
    return {
      $_ais_ssrInstantSearchInstance: this.instantsearch
    };
  },
  setup(_, context) {
    const uiState = useUiState();

    return {
      AisSortBy,
      AisRefinementList,
      ...uiState
    };
  },
  components: {
    AisInstantSearchSsr,
    AisHits,
    AisHighlight,
    AisSearchBox,
    AisPagination,
    AisSnippet,
    AisSortBy,
    AisStats,
    AisRefinementList,
    SfSidebar,
    SfButton,
    SfList,
    SfIcon,
    SfHeading,
    SfMenuItem,
    SfProductCard,
    SfProductCardHorizontal,
    SfPagination,
    SfAccordion,
    SfSelect,
    SfBreadcrumbs,
    SfLoader,
    SfNotification,
    LazyHydrate
  }
};
</script>
