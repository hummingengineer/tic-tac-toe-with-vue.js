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
            <v-card :color="active ? 'primary' : ''" class="d-flex align-center" dark height="200" :disabled="squares[row - 1][col - 1] ? true : false" @click="clickSquare(row, col, toggle)">
              <v-scroll-y-transition>
                <div v-if="active" class="display-3 flex-grow-1 text-center">
                  {{ squares[row - 1][col - 1] }}
                </div>
              </v-scroll-y-transition>
            </v-card>
          </v-item>
        </v-col>
      </v-row>
    </v-item-group>

    <v-dialog v-model="dialog" max-width="400" persistent>
      <v-card>
        <v-card-title>{{ winPlayer }} 플레이어가 승리하였습니다!</v-card-title>
        <v-card-actions>
          <v-btn color="green darken-1" text @click="endGame">
            확인
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

  </v-container>
</template>

<script>
export default {
  name: 'home',

  data: function () {
    return {
      currentPlayer: 'X',
      squares: [
        Array(3).fill(null),
        Array(3).fill(null),
        Array(3).fill(null)
      ],
      dialog: false,
      winPlayer: null
    }
  },

  methods: {
    clickSquare: function (row, col, toggle) {
      this.squares[row - 1][col - 1] = this.currentPlayer
      if (this.isWin()) this.dialog = true
      toggle()
      this.currentPlayer === 'X' ? this.currentPlayer = 'O' : this.currentPlayer = 'X'
    },
    isWin: function () {
      //
    },
    endGame: function () {
      this.dialog = false
      window.location.reload(true)
    }
  }

}
</script>

<style>

</style>
