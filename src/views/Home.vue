<template>
  <v-container>
    <v-row>
      <v-col>
        <div class="text-center display-1"><span style="color: red">{{ currentPlayer }}</span> 플레이어의 차례입니다</div>
      </v-col>
    </v-row>

    <v-row>
      <v-col>

        <v-card>
          <v-container>

            <v-row v-for="row in 3" :key="row" class="px-3">
              <v-card v-for="col in 3" :key="col" class="flex-grow-1" tile outlined :disabled="squares[row - 1][col - 1] ? true : false" @click="count < 9 ? clickSquare(row, col) : null">
                <div class="display-4 my-10 text-center">{{ squares[row - 1][col - 1] }}</div>
              </v-card>
            </v-row>

          </v-container>
        </v-card>

      </v-col>
    </v-row>

    <v-dialog v-model="winnerBanner" max-width="500">
      <v-card>
        <v-card-title>{{ currentPlayer }} 플레이어가 승리했습니다!</v-card-title>
        <v-card-actions>
          <v-spacer/>
          <v-btn color="green darken-1" text @click="dialogFunc">
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
      squares: [
        Array(3).fill(null),
        Array(3).fill(null),
        Array(3).fill(null)
      ],
      currentPlayer: 'X',
      count: 0,
      winnerBanner: false
    }
  },

  methods: {
    clickSquare: function (row, col) {
      if (this.count > 4) this.calculateWinner()
      this.count++
      this.squares[row - 1][col - 1] = this.currentPlayer
      this.currentPlayer === 'X' ? this.currentPlayer = 'O' : this.currentPlayer = 'X'
    },
    calculateWinner: function () {
      for (let i = 0; i < 3; i++) {
        if (this.squares[i][0] && this.squares[i][0] === this.squares[i][1] && this.squares[i][0] === this.squares[i][2]) { this.winnerBanner = true; return }
      }
      for (let j = 0; j < 3; j++) {
        if (this.squares[0][j] && this.squares[0][j] === this.squares[1][j] && this.squares[0][j] === this.squares[2][j]) { this.winnerBanner = true; return }
      }
      if (this.squares[0][0] && this.squares[0][0] === this.squares[1][1] && this.squares[0][0] === this.squares[2][2]) { this.winnerBanner = true; return }
      if (this.squares[0][2] && this.squares[0][2] === this.squares[1][1] && this.squares[0][2] === this.squares[2][0]) { this.winnerBanner = true }
    },
    dialogFunc: function () {
      this.winnerBanner = false
      window.location.reload(true)
    }
  }

}
</script>

<style>

</style>
