<template>
  <v-app id="inspire">
    <v-content>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="4">
            <v-card class="elevation-12">
              <v-toolbar color="primary" dark flat>
                <v-toolbar-title>Game List</v-toolbar-title>
                <v-spacer></v-spacer>
                <v-tooltip bottom></v-tooltip>
              </v-toolbar>
              <ul id="game-list">
                <li v-for="game in game_list" :key="game.Name">
                  {{ game.Name }}
                  {{ game.NumPlayers }}
                  {{ game.MaxPlayers }}
                  {{ game.HasStarted }}
                  {{ game.HasPassword }}
                </li>
              </ul>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import unoService from "../services/unoService";
export default {
  name: "Lobby",
  data: () => {
    return {
      game_list: "",
      sim: true // Only true while debugging
    };
  },
  created: function () {
      this.getGameList();
  },
  methods: {
    async getGameList() {
      let res = await unoService.getGameList();
      this.game_list = res.data;
    }
  }
};
</script>