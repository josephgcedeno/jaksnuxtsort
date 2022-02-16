<template>
   
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'
interface Item {
  name: string
  title: string
  to: string
}
@Component
export default class Header extends Vue {
  //  * Data
  pages: Item[] = [
    {
      name: 'index',
      title: 'Home',
      to: '/',
    },
    {
      name: 'users',
      title: 'Users',
      to: '/users',
    },
    {
      name: 'about',
      title: 'About',
      to: '/about',
    },
  ]
  // * * Computed
  /**
   * return currect active page
   */
  get activePage(): string {
    if (this.$route?.name === undefined || this.$route?.name === null) {
      return ''
    }
    if (this.$route?.name === 'users-id') {
      return 'users'
    }
    return this.$route?.name
  }
  // * * Methods
  /**
   * return to selected page/route
   * @param Item     page item object
   */
  onPageClick(item: Item): void {
    this.$router.push({ name: item.name })
  }
}
</script>

<style scoped>
.header__container {
  height: 80px;
}
</style>