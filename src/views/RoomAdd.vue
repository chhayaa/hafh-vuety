<template>
  <div>
    <v-app id="inspire">
      <v-card flat>
        <v-container fluid>
          <div>
            <v-toolbar>
              <v-btn icon href="">
                <v-icon>mdi-arrow-left</v-icon>
              </v-btn>

              <v-toolbar-title> Add Room/Area</v-toolbar-title>
            </v-toolbar>
          </div>
        </v-container>
      </v-card>
      <br />

      <v-form class="px-3">
        <!-- <v-text-field v-model="data.title" label="Name Of Rv"></v-text-field> -->
        <p class="para-title">Name Of Room/Area</p>
        <v-text-field
          v-model="data.room"
          placeholder="Family Rv"
          solo-inverted
          style="margin: 0px 20px 0px 20px"
        >
        </v-text-field>
        <p class="para-title">Add an Image</p>

        <v-text-field
          v-model="data.image"
          prepend-icon="mdi-camera"
        ></v-text-field>

        <v-spacer></v-spacer>
      </v-form>
      <br />
      <!-- <router-link :to="{ name: 'Room' }" tag="v-btn"> -->
      <div class="text-center">
        <v-btn
          @click="createNewRoom"
          style="width: 100px"
          rounded
          color="#ffab01"
          dark
        >
          Add Room
        </v-btn>
      </div>
      <!-- </router-link> -->

      <!-- <router-link :to="{ name: 'Rv' }">
        
        <v-btn @click="createNewRv" class="success mx-0 mt-3">Add RV</v-btn>
      </router-link> -->
      <br />
      <div class="text-center">
        <v-btn outlined rounded color="#ffab01" dark>
          <v-icon style="padding-right: 5px"> mdi-share </v-icon>
          Share with people
        </v-btn>
      </div>
    </v-app>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: " RoomAdd",
  data() {
    return {
      title: "RoomAdd",
      rvId: this.$route.params.rvId,
      data: {},
      newRoom: [],
    };
  },

  methods: {
    async createNewRoom() {
      const options = {
        method: "POST",
        url: "http://localhost:3000/Room/create",
        headers: { "Content-Type": "application/json" },
        data: {
          name: this.data.room,
          image: this.data.image,
          creator: "507f1f77bcf86cd799439014",
          Rv: "60a27169c189465f8d338141",
        },
      };

      const newRoomCreated = await axios.request(options);
      this.newRoom = newRoomCreated.data.data;
      console.log(this.newRoom);
    },
  },
};
</script>

<style scoped>
.para-title {
  margin-right: 60%;
}

.para {
  margin-right: 50%;
}
/* .v-btn {
  width: 100px;
} */
</style>
