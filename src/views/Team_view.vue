<template>
  <div class="team">
    <h1 class="subtitle-1 grey--text">Team</h1>

    <v-container class="my-5">
      <v-row wrap>
        <v-col
          cols="12"
          sm="6"
          md="4"
          lg="3"
          v-for="person in team"
          :key="person.name"
        >
          <v-card class="text-center ma-3">
            <v-responsive class="pt-4">
              <v-avatar size="100" class="grey lighten-3">
                <img :src="person.avatar" alt="" />
              </v-avatar>
            </v-responsive>
            <v-card-text>
              <div class="body-1">{{ person.name }}</div>
              <div class="grey--text">{{ person.role }}</div>
            </v-card-text>
            <v-card-actions>
              <v-btn plain color="grey">
                <v-icon small left>mdi-message-text</v-icon>
                <span>Message</span>
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      team: [
        {
          name: "Sandali singh",
          role: "Web developer",
          avatar: "/avatar5.png",
        },
        { name: "Ryu", role: "Graphic designer", avatar: "/avatar3.png" },
        { name: "Chun Li", role: "Web developer", avatar: "/avatar6.png" },
        {
          name: "Gouken",
          role: "Social media maverick",
          avatar: "/avatar4.png",
        },
        { name: "Yoshi", role: "Sales guru", avatar: "/avatar1.png" },
      ],
    };
  },
};
</script>
