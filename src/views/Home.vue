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
      if (this.isWin()) { this.winPlayer = this.currentPlayer; this.dialog = true }
      toggle()
      this.currentPlayer === 'X' ? this.currentPlayer = 'O' : this.currentPlayer = 'X'
    },
    isWin: function () {
      for (let i = 0; i < 3; i++) if (this.squares[i][0] && this.squares[i][0] === this.squares[i][1] && this.squares[i][0] === this.squares[i][2]) return true
      for (let j = 0; j < 3; j++) if (this.squares[0][j] && this.squares[0][j] === this.squares[1][j] && this.squares[0][j] === this.squares[2][j]) return true
      if (this.squares[0][0] && this.squares[0][0] === this.squares[1][1] && this.squares[0][0] === this.squares[2][2]) return true
      if (this.squares[0][2] && this.squares[0][2] === this.squares[1][1] && this.squares[0][2] === this.squares[2][0]) return true
      return false
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
