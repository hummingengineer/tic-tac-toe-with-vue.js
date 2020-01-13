<template>
  <v-container>

    <v-row>
      <v-col>
        <div class="text-center display-1"><span style="color: red">{{ currentPlayer }}</span> 플레이어의 차례입니다</div>
      </v-col>
    </v-row>

    <v-item-group multiple>
      <v-row v-for="row in 3" :key="row">
        <v-col v-for="col in 3" :key="col">
          <v-item v-slot:default="{ active, toggle }">
            <v-card :color="active ? 'primary' : ''" class="d-flex align-center" dark height="200" @click="toggle(); clickSquare()">
              <v-scroll-y-transition>
                <div v-if="active" class="display-3 flex-grow-1 text-center">
                  {{ currentPlayer }}
                </div>
              </v-scroll-y-transition>
            </v-card>
          </v-item>
        </v-col>
      </v-row>
    </v-item-group>

  </v-container>
</template>

<script>
export default {
  name: 'home',

  data: function () {
    return {
      currentPlayer: 'X'
    }
  },

  methods: {
    clickSquare: function () {
      this.currentPlayer === 'X' ? this.currentPlayer = 'O' : this.currentPlayer = 'X'
    }
  }

}
</script>

<style>

</style>
