<template>
  <section>
    <base-card>
      <h2>Submitted Experiences</h2>
      <div>
        <base-button @click="loadExperiences">Load Submitted Experiences</base-button>
      </div>
      <p v-if="isLoading">
        Loading...
      </p>
      <p v-else-if="!isLoading && (!results || results.length === 0)">
        No data there yet..
      </p>
      <p v-else-if="!isLoading && error">
        {{error}}
      </p>
      <ul v-else>
        <survey-result
          v-for="result in results"
          :key="result.id"
          :name="result.name"
          :rating="result.rating"
        ></survey-result>
      </ul>
    </base-card>
  </section>
</template>

<script>
import SurveyResult from './SurveyResult.vue';

export default {
  components: {
    SurveyResult,
  },
  data() {
    return {
      results: [],
      isLoading: false,
      error: null
    }
  },
  methods: {
    loadExperiences(){
      this.isLoading = true;
      this.error = null;
      fetch("http://jabosa.de:8080/data", {
        method: "GET"
      }).then(function(response){
        if(response.ok){
          return response.json();
        }
      }).then((jsonData) => {
        const newResults = [];
        for(let entry in jsonData){
          newResults.push(jsonData[entry]);
        }
        this.isLoading = false;
        this.results = newResults;
      }).catch(error => {
        this.error = "Data couldn't be fetched. Check the URL and make sure, the server is accessable."
      });
    }
  },
  mounted() {
    this.loadExperiences();
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>