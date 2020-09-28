<template>
  <v-app>
    <v-main>
      <Keeb/>
    </v-main>
  </v-app>
</template>

<script>
import Keeb from './components/Keeb2';

export default {
  name: 'App',

  components: {
    Keeb,
  },

  data: () => ({
    //
  }),
};
</script>
<style lang="scss">

</style>
