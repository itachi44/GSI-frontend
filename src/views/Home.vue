<template>
  <div class="container">
    <section class="content">
      <p style="font-size:1.5em; color:#CA7900;">Implementation de la page d'accueil ici</p>
    </section>
    <!-- 
    <div class="large-12 medium-12 small-12 cell">
      <label>
        File
        <input type="file" id="file" ref="file" v-on:change="handleFileUpload()" />
      </label>
      <button v-on:click="submitFile()">Submit</button>
    </div>

    <br />
    <br />

    <div v-if="user">
      <pdf :src="user.get_cv"></pdf>
    </div>-->
  </div>
</template>



<script>
import axios from "axios";
import { mapState } from "vuex";
//import pdf from "vue-pdf";

export default {
  name: "Home",
  components: {
    // pdf
  },
  props: {
    user: {
      type: []
    }
  },
  data() {
    return {
      file: ""
    };
  },

  methods: {
    handleFileUpload() {
      this.file = this.$refs.file.files[0];
    },

    submitFile() {
      let formData = new FormData();
      formData.append("cv", this.file);

      //TODO: change the URI it's just a test

      axios
        .patch("/api/etudiant/1/", formData, {
          headers: {
            "Content-Type": "multipart/form-data"
          }
        })
        .then(function() {
          console.log("SUCCESS!!");
        })
        .catch(function() {
          console.log("FAILURE!!");
        });
    }
  },
  computed: {
    ...mapState({
      isAuthenticated: "isAuthenticated"
    })
  }
};
</script>

<style >
</style>