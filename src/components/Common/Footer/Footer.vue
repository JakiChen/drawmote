<template>
  <div ref="footer" class="footer">
    <div class="footer__content">
      <ul class="list-inline list-inline--tight text-small footer__list">
        <FooterBrowserSupport :is-mobile="isMobile" />
        <FooterLanguage />
        <FooterConnection v-if="!isMobile" />
        <FooterGithub />
        <FooterCopyright />
        <FooterAttribution />
      </ul>
    </div>
  </div>
</template>

<script>
import debouncedResize from 'debounced-resize'

import FooterBrowserSupport from '@/components/Common/Footer/FooterBrowserSupport.vue'
import FooterCopyright from '@/components/Common/Footer/FooterCopyright.vue'
import FooterConnection from '@/components/Common/Footer/FooterConnection.vue'
import FooterGithub from '@/components/Common/Footer/FooterGithub.vue'
import FooterLanguage from '@/components/Common/Footer/FooterLanguage.vue'
import FooterAttribution from '@/components/Common/Footer/FooterAttribution.vue'

export default {
  name: 'Footer',

  components: {
    FooterBrowserSupport,
    FooterCopyright,
    FooterConnection,
    FooterGithub,
    FooterLanguage,
    FooterAttribution
  },

  props: {
    isMobile: {
      type: Boolean,
      default: false
    }
  },

  mounted() {
    this.updateSizes()
    debouncedResize(() => {
      this.updateSizes()
    })
  },

  methods: {
    updateSizes() {
      const footer = this.$refs.footer
      this.$vuetamin.store.mutate('updateFooterRect', footer)
    }
  }
}
</script>

<style lang="scss">
.footer {
  position: fixed;
  right: 0;
  left: 0;
  bottom: 0;
  user-select: none;
  z-index: $index-footer;
  @include media('xs', $breakpoints-desc) {
    &:before {
      content: '';
      position: absolute;
      pointer-events: none;
      top: -1.5rem;
      left: 0;
      width: 100%;
      bottom: 0;
      background: linear-gradient(
        0deg,
        $alt-color-darkest,
        rgba($alt-color-darkest, 0.9),
        rgba($alt-color-darkest, 0)
      );
    }
  }
}

.footer__content {
  position: relative;
  z-index: $index-footer;
}

.footer__list {
  align-items: stretch !important;
  @include media('sm') {
    .hover {
      &:hover {
        background: $color-translucent-dark;
      }
    }
  }
}

.footer-text {
  @include media('xs', $breakpoints-desc) {
    font-size: 11px;
  }
}
</style>
