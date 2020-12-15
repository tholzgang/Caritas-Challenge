<template>
  <div id="app">
    <h1>Salary estimator</h1>
    <img
      alt="Cover image"
      src="https://dl.airtable.com/.formViewCoverImages/67ae4a61fafddcf7ce8c979fd578076d/2142c67d"
      width="100%"
    />
    <ApplicantForm />
  </div>
</template>

<script>
import ApplicantForm from "./components/ApplicantForm";

export default {
  name: "App",
  components: {
    ApplicantForm,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#app > img {
  margin: 0;
  padding: 0;
}
h1 {
  font-size: 125%;
  color: #999;
}
</style>
