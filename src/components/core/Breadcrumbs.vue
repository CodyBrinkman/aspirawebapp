<template>
  <!-- <v-breadcrumbs :items="items" class="breadcrumbs" divider="/">
    <template slot="item" slot-scope="props">
      <v-layout>
      <v-flex md11><router-link :to="{ name: props.item.href }" class="link">{{ props.item.name }}</router-link></v-flex>
      <v-flex md1><v-icon @click="$router.push({ name: 'HelpSupport' })">search</v-icon></v-flex>
      <v-flex md1><v-icon @click="$router.push({ name: 'Home' })">home</v-icon></v-flex>
      </v-layout>
    </template>
  </v-breadcrumbs> -->
  <v-breadcrumbs>
    <template>
      <v-layout>
      <!-- <v-flex md11><router-link :to="{ name: props.item.href }" class="link">{{ props.item.name }}</router-link></v-flex> -->
      <v-flex md1><v-icon @click="$router.push({ name: 'HelpSupport' })">search</v-icon></v-flex>
      <v-flex md1><v-icon @click="$router.push({ name: 'Home' })">home</v-icon></v-flex>
      </v-layout>
    </template>
  </v-breadcrumbs>
</template>

<script>
export default {
  data() {
    return {
      items: []
    };
  },

  watch: {
    $route() {
      const vm = this;
      vm.updateBreadcrumbs();
    }
  },

  mounted() {
    const vm = this;
    vm.updateBreadcrumbs();
  },

  methods: {
    updateBreadcrumbs() {
      const vm = this;
      vm.items = vm.$route.meta.breadcrumb;
    }
  }
};
</script>

<style>
.breadcrumbs .link {
  text-decoration: none;
  color: #737373;
  font: bold 24px Sans-Serif;
  letter-spacing: -1px;
  white-space: nowrap;
  display: inline-block;
  position: relative;
}
</style>
