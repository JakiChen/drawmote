<template>
  <li class="text-bold mrgla hover">
    <a
      class="pdg block text-white footer-text"
      href="https://github.com/dulnan/drawmote"
    >
      <IconGithub class="icon icon--large" />
      <span class="hidden-sm-down">GitHub</span>
    </a>
  </li>
</template>

<script>
import IconGithub from '@/assets/icons/icon-github.svg'

export default {
  name: 'FooterCopyright',

  components: {
    IconGithub
  }
}
</script>
