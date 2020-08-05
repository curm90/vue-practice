<template>
  <div id="app" class="container">
    <h1 class="text-center">Player Score counter</h1>
    <div class="card">
      <div class="card-body text-center">
        <h3>Player One</h3>
        <button @click="decreaseScore(player_1)" class="btn btn-success">Down</button>
        <span class="player-score">{{player_1.score}}</span>
        <button @click="increaseScore(player_1)" type="button" class="btn btn-danger">Up</button>
      </div>
      <div class="card-body text-center">
        <h3>Player Two</h3>
        <button @click="decreaseScore(player_2)" class="btn btn-success">Down</button>
        <span class="player-score">{{player_2.score}}</span>
        <button @click="increaseScore(player_2)" type="button" class="btn btn-danger">Up</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      player_1: {
        score: 0,
      },
      player_2: {
        score: 0,
      },
    };
  },
  methods: {
    increaseScore(player) {
      player.score += 1;
    },

    decreaseScore(player) {
      if (player.score > 0) {
        player.score -= 1;
      }
    },
  },
};
</script>

<style>
.player-score {
  font-size: 3em;
}
</style>
