<template>
  <v-app>

    <v-app-bar app color="primary" dark>
      Tic Tac Toe

      <v-spacer/>

      <v-btn href="https://github.com/hummingengineer/tic-tac-toe-with-vue.js" target="_blank" text>
        <span class="mr-2">개발자 홈페이지</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-content>
      <router-view :key="$route.fullPath"/>
    </v-content>

  </v-app>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>

</style>
