<template>
  <div class="dashboard">
    <!-- <v-btn @click="addDataToDatabase"> Add Data</v-btn>
    <v-btn @click="getDataFromDatabase"> get Data</v-btn>
    <v-btn @click="getAllDataFromDatabase"> get all Data</v-btn>
    <v-btn @click="getUpdated"> Update Data</v-btn>
    <v-btn @click="getFieldDeleted"> Delete a field</v-btn>
    <v-btn @click="getDocDeleted"> Detete a Doc</v-btn> -->

    <h1 class="subtitle-1 grey--text">Dashboard</h1>
    <v-container class="my-5">
      <v-row class="mb-3">
        <v-tooltip top>
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              text
              small
              color="grey"
              @click="sortBy('title')"
              v-bind="attrs"
              v-on="on"
            >
              <v-icon left small>mdi-folder</v-icon>
              <span class="caption text-lowercase">By projecy name</span>
            </v-btn>
          </template>
          <span>sort by project name</span>
        </v-tooltip>

        <v-tooltip top>
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              text
              small
              color="grey"
              @click="sortBy('person')"
              v-bind="attrs"
              v-on="on"
            >
              <v-icon left small>mdi-account</v-icon>
              <span class="caption text-lowercase">By person</span>
            </v-btn>
          </template>
          <span>sort by person name</span>
        </v-tooltip>
      </v-row>

      <v-card
        flat
        class="pa-1"
        v-for="project in projects"
        :key="project.title"
      >
        <v-row :class="`pa-3 project ${project.status}`">
          <v-col cols="12" md="6">
            <div class="caption grey--text">Project title</div>
            <div>{{ project.title }}</div>
          </v-col>
          <v-col cols="6" md="2" sm="4">
            <div class="caption grey--text">Person</div>
            <div>{{ project.person }}</div>
          </v-col>
          <v-col cols="6" md="2" sm="4">
            <div class="caption grey--text">Due By</div>
            <div>{{ project.due }}</div>
          </v-col>
          <v-col cols="2" md="2" sm="4">
            <div class="float-right">
              <v-chip
                small
                :class="`${project.status} white--text my-2 caption`"
                >{{ project.status }}</v-chip
              >
            </div>
          </v-col>
        </v-row>
        <v-divider></v-divider>
      </v-card>

      <!-- <v-row wrap>
        <v-col col="12" md="6" sm="12">
          <v-btn outlined block color="primary">1</v-btn>
        </v-col>
        <v-col col="6" md="2" sm="4">
          <v-btn outlined block color="primary">2</v-btn>
        </v-col>
        <v-col col="6" md="2" sm="4">
          <v-btn outlined block color="primary">2</v-btn>
        </v-col>
        <v-col col="6" md="2" sm="4">
          <v-btn outlined block color="primary">2</v-btn>
        </v-col>
      </v-row> -->
    </v-container>
  </div>
</template>

<script>
import { db } from "@/fb";
import { onSnapshot, collection } from "firebase/firestore";

// import { getData } from "@/services/app.serviceRead";
// import { addData } from "@/services/app.serviceAdd";
// import { getDataAll } from "@/services/app.serviceReadAll";
// import { updateVal } from "@/services/app.serviceUpdation";
// import { deleteFieldFromDoc } from "@/services/app.serviceDeleteField";
// import { deleteTheDoc } from "@/services/app.serviceDeleteDoc";

export default {
  data() {
    return {
      projects: [
        {
          title: "Design a new website",
          person: "The Net Ninja",
          due: "1st Jan 2019",
          status: "ongoing",
          content:
            "Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!",
        },
        {
          title: "Code up the homepage",
          person: "Chun Li",
          due: "10th Jan 2019",
          status: "complete",
          content:
            "Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!",
        },
        {
          title: "Design video thumbnails",
          person: "Ryu",
          due: "20th Dec 2018",
          status: "complete",
          content:
            "Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!",
        },
        {
          title: "Create a community forum",
          person: "Gouken",
          due: "20th Oct 2018",
          status: "overdue",
          content:
            "Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!",
        },
      ],
    };
  },
  methods: {
    sortBy(prop) {
      this.projects.sort((a, b) => (a[prop] < b[prop] ? -1 : 1));
    },
    // addDataToDatabase() {
    //   let dataToAdd = {
    //     name: "sandali singh",
    //     age: 24,
    //   };
    //   addData(dataToAdd);
    // },

    // getDataFromDatabase() {
    //   const docData = [{}];
    //   getData(docData);
    // },

    // getAllDataFromDatabase() {
    //   const docData = [{}];
    //   getDataAll(docData);
    // },
    // getUpdated() {
    //   updateVal();
    // },
    // getFieldDeleted() {
    //   deleteFieldFromDoc();
    // },
    // getDocDeleted() {
    //   deleteTheDoc();
    // },
  },
  created() {
    onSnapshot(collection(db, "Databook"), (snapshot) => {
      snapshot.docChanges().forEach((change) => {
        if (change.type === "added") {
          this.projects.push({
            ...change.doc.data(),
            id: change.doc.id,
          });
        }
      });
    });
    // db.collection("Databook").onSnapshot((res) => {
    //   const changes = res.docChanges();
    //   changes.forEach((change) => {
    //     if (change.type === "added") {
    //       this.projects.push({
    //         ...change.doc.data(),
    //         id: change.doc.id,
    //       });
    //     }
    //   });
    // });
  },
};
</script>

<style>
.project.complete {
  border-left: 4px solid #3cd1c2;
}
.project.ongoing {
  border-left: 4px solid orange;
}
.project.overdue {
  border-left: 4px solid tomato;
}

.theme--light .v-chip.complete {
  background: #3cd1c2;
}
.theme--light .v-chip.ongoing {
  background: #ffaa2c;
}
.theme--light .v-chip.overdue {
  background: #f83e70;
}

/* .v-chip.complete {
  background: #3cd1c2;
}
.v-chip.ongoing {
  background: #ffaa2c;
}
.v-chip.overdue {
  background: #f83e70;
} */
</style>
