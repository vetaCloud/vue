<template>
  <div id="app">
    <div class="App d-flex flex-column justify-content-center align-items-center">
      <form @submit="uploadFile">
        <div class="mb-3">
          <label for="formFile" class="form-label">
            Default file input example
          </label>
          <input @change="setFile" class="form-control" type="file" id="formFile" />
        </div>
        <button class="btn btn-primary">Submit</button>
      </form>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { ref } from "vue";


const file = ref(null)

const setFile = (e) => {
  file.value = e.target.files[0];
}
const uploadFile = async (e) => {
  e.preventDefault();
  if (!file.value) {
    alert("Please select a file");
    return;
  }

  const formData = new FormData();
  formData.append("file", file.value);
  const headers = {
    "Content-Type": "application/json",
    X_API_KEY: "VTCD_PRIVATE_093a7a3f-f0f7-4db3-aab8-b577f289552b", // Add your api key here
    X_ROUTE_NAME: "user-images",
  };

  const data = await axios({
    method: 'post',
    headers: headers,
    url: "https://cloud.vetacloud.com/client",
    data: formData,
  });
  console.log(data);
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>