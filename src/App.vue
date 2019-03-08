<template>
  <v-app id="inspire">
    <main>
      <v-content>
        <v-container fluid fill-height>
          <v-layout>
            <v-card id="services-card" class="ma-2 pa-2" height="100%">
              <services></services>
            </v-card>
            <v-card id="divisions-card" class="ma-2 pa-2" height="100%">
              <divisions></divisions>
            </v-card>
          </v-layout>
        </v-container>
      </v-content>
    </main>
  </v-app>
</template>

<script>
  import draggable from 'vuedraggable'
  import Services from '../Components/Services.vue'
  import Divisions from '../Components/Divisions.vue'

  export default {
    data: () => ({
      drawer: false
    }),
    props: {
      source: String
    },
    components: {
      draggable,
      services: Services,
      divisions: Divisions
  },
  }
</script>

<style>
  #services-card {
    min-height: 600px;
    width: 50%;
  }

   #divisions-card {
     min-height: 600px;
     width: 50%;
   }
</style>


