<script>
import filmsData from "../assets/data/films.json";

export default {
  name: "Film",
  data() {
    return {
      films: filmsData,

      film: {
        title: "",
        director: "",
        release: "",
        summary: "",
      },
      dialog: false,
      editDialog: false,
    };
  },

  methods: {
    addElement() {
      this.films.push(this.film);
      localStorage.setItem("films", JSON.stringify(this.films));
    },
    removeElement(id) {
      this.films.splice(id, 1);
    },
  },
};
</script>

<template>
  <v-container fluid>
    <v-row justify="center">
      <v-dialog v-model="dialog" persistent width="1024">
        <template v-slot:activator="{ props }">
          <v-btn color="primary" v-bind="props"> Add film </v-btn>
        </template>
        <v-card>
          <v-card-title>
            <span class="text-h5">Add a film</span>
          </v-card-title>
          <v-card-text>
            <v-container>
              <v-row>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field
                    label="Title"
                    required
                    v-model="film.title"
                  ></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field
                    label="director"
                    v-model="film.director"
                  ></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field
                    label="release"
                    v-model="film.release"
                    required
                  ></v-text-field>
                </v-col>
                <v-col cols="12">
                  <v-text-field
                    label="summary"
                    v-model="film.summary"
                    required
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-card-text>
          <v-card-actions>
            <v-btn color="blue-darken-1" variant="text" @click="dialog = false">
              Close
            </v-btn>
            <v-btn
              color="blue-darken-1"
              variant="text"
              @click.prevent="
                addElement();
                dialog = false;
              "
            >
              Save
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-row>

    <v-row>
      <v-col v-for="(film, index) in films" lg="3" cols="12">
        <h3>{{ film.title }}</h3>
        <h4>{{ film.director }}</h4>
        <h5>{{ film.release }}</h5>
        <p>{{ film.summary }}</p>
        <v-btn
          color="primary"
          @click.prevent="removeElement(index)"
          type="submit"
        >
          Delete
        </v-btn>

        <v-dialog>
          <template v-slot:activator="{ props }">
            <v-btn color="primary" v-bind="props"> edit </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="text-h5">Edit film</span>
            </v-card-title>
            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      type="text"
                      v-model="film.title"
                      placeholder="Title"
                      ref="textField"
                    />
                    <v-text-field
                      type="text"
                      v-model="film.director"
                      placeholder="Director"
                      ref="textField"
                    />
                    <v-text-field
                      type="text"
                      v-model="film.release"
                      placeholder="Release date"
                      ref="textField"
                    />
                    <v-text-field
                      type="text"
                      v-model="film.summary"
                      placeholder="Summary"
                      ref="textField"
                    />
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>
          </v-card>
        </v-dialog>
      </v-col>
    </v-row>
  </v-container>
</template>
