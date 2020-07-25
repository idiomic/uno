<template>
  <v-app id="inspire">
    <v-content>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col>
            <v-card class="elevation-12">
              <v-toolbar color="primary" dark flat>
                <v-toolbar-title>Game List</v-toolbar-title>
                <v-spacer></v-spacer>
                <v-tooltip bottom></v-tooltip>
              </v-toolbar>
              <v-data-table
                :headers="headers"
                :items="game_list"
                :items-per-page="5"
              >
                <template v-slot:item.HasPassword="{ item }">
                  <v-icon v-if="item.HasPassword">mdi-lock</v-icon>
                </template>
              </v-data-table>
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
      headers: [
        {
          text: "Game ID",
          value: "Name"
        },
        {
          text: "Cur Players",
          value: "NumPlayers"
        },
        {
          text: "Max Players",
          value: "MaxPlayers"
        },
        {
          text: "In Progress",
          value: "HasStarted"
        },
        {
          text: "Password",
          value: "HasPassword"
        },
      ],
      game_list: [],
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