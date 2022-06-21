<template>
  <v-app id="app">
    <template v-if="!$route.path.includes('login')">
      <Navigation/>
    </template>
    <v-content>
        <keep-alive :include="['Login']">
          <router-view/>
        </keep-alive>
    </v-content>
  </v-app>
</template>

<script>
import Navigation from './components/Navigation.vue';

export default {
  name: 'App',
  components: { Navigation },

  data: () => ({
    //
  }),
};
</script>
