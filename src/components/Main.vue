<template>
  <section id="hero">
    <div class="hero-container">
      <h1>Welcome to Random Photo Sharing App</h1>
      <h2>This is a Vue app that randomly shares photos via Unsplash API.</h2>
      <h6 style="color: #afeafe">Information about the identities and profiles of the owners of the photos will also be shared.</h6>

      <button class="btn-get-started" v-b-modal.modal-img variant="primary" @click="getRandomPhoto()">
        Get a Photo
      </button>
    </div>

    <!-- Modal -->
    <b-modal id="modal-img" size="xl" title="Extra Large Modal" hide-footer hide-header>
      <!-- Description -->
      <h5 v-if="this.photo.description == '' || this.photo.description == null">No description.</h5>
      <h5 v-else>{{this.photo.description}}</h5>

      <!-- Location -->
      <h6 v-if="this.photo.location.city !== null">{{this.photo.location.city}}</h6>
      <h6 v-if="this.photo.location.country !== null">{{this.photo.location.country}}</h6>
      <h6 v-if="this.photo.location.name !== null">{{this.photo.location.name}}</h6>
      <h6 v-if="this.photo.location.city !== null && this.photo.location.country !== null && this.photo.location.name !== null">No location entered.</h6>

      <!-- Image -->
      <img alt="" :src="photo.link">

      <!-- See the original -->
      <a class="btn-get-started mt-3" :href="this.photo.original" target="_blank">See the original size of the photo on Unsplash.</a>

      <!-- See the author -->
      <a class="btn-get-started mt-3" v-b-modal.modal-others variant="primary">See the author of this photograph.</a>
      <!-- Author Modal -->
      <b-modal id="modal-others" size="md" title="Extra Large Modal" hide-footer hide-header>
        <!-- Image -->
        <h4>{{this.author.name}}</h4>
        <h5>{{this.author.username}}</h5>
        <h6>{{this.author.bio}}</h6>
        <img alt="author profile picture" :src="this.author.profileImg">
        <a :href="author.profileURL" target="_blank">Go to author's profile.</a>
      </b-modal>
    </b-modal>
  </section>
</template>

<script>
import axios from "axios";

export default {
  name: "Main",
  data() {
    return {
      accessKey: "BO9YzGiriDcodBa8nVMcYNWxRikMZhR2nT1FTeJ1Vfg",
      url: "https://api.unsplash.com/photos/random",
      photo: {
        link: "",
        description: "",
        original: "",
        location: {
          city: "",
          country: "",
          name: "",
        },
      },
      author: {
        name: "",
        username: "",
        bio: "",
        profileImg: "",
        profileURL: ""
      }
    };
  },
  methods: {
    getRandomPhoto() {
      axios.get(this.url + `?client_id=${this.accessKey}`)
      .then((response) => {
        console.log(response);
        // Photo
        this.photo.link = response.data.urls.small;
        this.photo.description = response.data.alt_description;
        this.photo.original = response.data.urls.full;
        // Location
        this.photo.location.city = response.data.location.city;
        this.photo.location.country = response.data.location.country;
        this.photo.location.name = response.data.location.name;
        // Author
        this.author.name = response.data.user.name;
        this.author.username = response.data.user.username;
        this.author.bio = response.data.user.bio;
        this.author.profileImg = response.data.user.profile_image.large;
        this.author.profileURL = response.data.user.links.html;
      });
    },
  },
};
</script>

<style>
.modal-body {
  display: flex;
  align-items: center;
  flex-direction: column;
}
</style>
