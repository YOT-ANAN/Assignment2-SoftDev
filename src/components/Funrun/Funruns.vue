<template>
  <v-container>
    <v-layout row wrap v-for="funrun in funruns" :key="funrun.id" class="mb-2">
      <v-flex xs12 sm10 md8 offset-sm1 offset-md2>
        <v-card class="info">
        <v-container fluid>
          <v-layout row>
            <v-flex xs5 sm4 md3>
              <v-card-media
              :src="funrun.imageUrl"
              height="125px"
              ></v-card-media>
            </v-flex>
            <v-flex xs7 sm8 md9>
              <v-card-title primary-title>
                <div>
                  <h2 class="white--text mb-0">{{ funrun.title }}</h2>
                  <div>{{ funrun.location }}</div>
                </div>
              </v-card-title>
              <v-card-actions>
                <v-btn flat :to="'/funreads/' + funrun.id"><v-icon left light>arrow_forward</v-icon>อ่านเพิ่มเติม</v-btn>
              </v-card-actions>
          </v-flex>
          </v-layout>
      </v-container>
    </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    computed: {
      funruns () {
        return this.$store.getters.loadedFunruns
      }
    }
  }
</script>
