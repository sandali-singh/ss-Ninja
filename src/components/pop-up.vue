<template>
  <v-dialog max-width="600px" v-model="dialog">
    <template v-slot:activator="{ on, attrs }">
      <v-btn color="success" dark v-bind="attrs" v-on="on">
        Add a New Project</v-btn
      >
    </template>
    <v-card>
      <v-card-title>
        <h2>Add a New Project</h2>
      </v-card-title>
      <v-card-text>
        <v-form class="px-3" ref="form">
          <v-text-field
            required
            :rules="nameRules"
            label="Title"
            v-model="title"
            prepend-icon="mdi-folder"
          ></v-text-field>
          <v-textarea
            required
            :rules="nameRules"
            label="Information"
            v-model="content"
            prepend-icon="mdi-pencil"
          ></v-textarea>

          <v-menu
            min-width="auto"
            v-model="menu"
            :close-on-content-click="true"
          >
            <template v-slot:activator="{ on, attrs }">
              <v-text-field
                :rules="nameRules"
                required
                clearable
                label="Due Date"
                prepend-icon="mdi-calendar"
                v-bind="attrs"
                v-on="on"
                :value="formattedDate"
              ></v-text-field>
            </template>
            <v-date-picker v-model="due"></v-date-picker>
          </v-menu>
          <v-btn
            flat
            class="success mx-0 mt-3"
            @click="submit"
            :loading="loading"
          >
            Add Project
          </v-btn>
        </v-form>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
//import format from "date-fns/format";
import moment from "moment";

import { addData } from "@/services/app.serviceAdd";

export default {
  data() {
    return {
      title: "",
      content: "",
      due: null,
      menu: false,
      dialog: false,
      nameRules: [(v) => !!v || "Is required"],
      loading: false,
    };
  },
  methods: {
    submit() {
      if (this.$refs.form.validate()) {
        this.loading = true;
        //console.log(this.title, this.content);
        const project = {
          title: this.title,
          content: this.content,
          due: moment(this.due).format("Do MMM YYYY"),
          person: "The Net Ninja",
          status: "ongoing",
        };
        addData(project).then(() => {
          this.loading = false;
          this.dialog = false;
          this.$emit("projectAdded");
        });
      }
    },
  },
  computed: {
    formattedDate() {
      console.log(this.due);
      return this.due ? moment(this.due).format("Do MMM YYYY") : "";
    },
  },
};
</script>
