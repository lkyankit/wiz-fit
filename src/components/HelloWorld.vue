<template>
  <div class="">
    <header>
      <img src="@/assets/banner.png" alt="WizFit banner" class="">
    </header>

    <div class="content">
      <div class="challenge mt-5">
        <h2 class="fs-1 fw-bold text-danger">What is WizFit Challenge?</h2>
        <button @click="playVideo" class="watch-video "> <span class="triangle"></span><span
            class="ms-2 fw-bold m-auto">Watch Video</span></button>
      </div>


      <div class="challenge-section">
        <img src="@/assets/player.png" alt="WizFit Player" class="player">
        <div class="border-css shadow  rounded p-2">
          <h3 class="fs-1 fw-bold text-danger">Are you ready to take the challenge?</h3>
          <div class="mt-4">
            <span class="fs-6 fw-bold ">Download Harlem Wizards Apps </span>
            <div class="w-75 m-auto">
              <img class="w-25" src="@/assets/goolge-store.png" alt="">
              <img class="w-25" src="@/assets/apple-store.png" alt="">
            </div>
            <div class="mt-4 w-75 m-auto mb-4">
              <div class="line"></div>
              <div class="d-inline m-4">or you can sign up right now</div>
              <div class="line"></div>

            </div>
          </div>
          <input v-model="searchQuery" @input="fetchSchools" type="text" placeholder="Search for school..."
            class="search-input" />
          <ul v-if="schools.length">
            <li class="row mt-2 p-2 bg-body-secondary text-dark" v-for="school in schools" :key="school.id">
              <div class=" col name-diplay text-start ms-2">
                <img :src="school.logo" alt="" class="school-logo">
                {{ school.school_name }}
              </div>
              <button class="col-3 btn btn-outline-danger btn-sm me-3" @click="joinCampaign(school.id)">Join
                Campaign</button>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      searchQuery: '',
      schools: []
    };
  },
  mounted() {
    this.fetchSchools();
  },
  created() {
    this.fetchSchools();
  },
  methods: {
    async fetchSchools() {

      try {
        const response = await axios.get(`http://api.devharlemwizardsinabox.com/campaign/campaign_school_list/?search=${this.searchQuery}`);
        console.log("data", response.data.school_list)
        this.schools = response.data.school_list;
      } catch (error) {
        console.error('Error fetching schools:', error);
      }

    },
    joinCampaign(schoolId) {
      // Handle the campaign joining process
      console.log(`Joining campaign for school ID: ${schoolId}`);
    },
    playVideo() {
      // Logic to play the challenge video
      console.log("Playing the video...");
    }
  }
};
</script>

<style scoped>
.challenge {
  display: flex;
  justify-content: center;
  margin: 20px;

}

h2 {
  margin-right: 20px;
}

.container {
  text-align: center;
}

.banner {
  max-width: -webkit-fill-available;
  max-height: -webkit-fill-available;
}

.watch-video {
  display: flex;
  background-color: #f2005e;
  color: white;
  padding: 10px 20px;
  border: none;
  cursor: pointer;

}

.triangle {
  margin: auto;
  width: 10px;
  border-left: solid 10px white;
  border-bottom: solid 10px transparent;
  border-top: solid 10px transparent;
}

.border-css {
  width: 70%;
  margin: auto;
}

.player {
  width: 40%;
}

.search-input {
  width: 70%;
  padding: 10px;
  margin: 20px 0;
  border-radius: 10px;
}

ul {
  list-style: none;
  padding: 0;
}

li {


  width: 70%;
  margin: auto;

  border-radius: 10px;


}

.name-diplay {
  width: 20px;
  height: 20px;
}

.school-logo {
  max-width: 100%;
  max-height: 100%;
}

.line {
  width: 30%;
  height: 0;
  border: 1px solid #C4C4C4;
  margin: 3px;
  display: inline-block;
}
</style>
