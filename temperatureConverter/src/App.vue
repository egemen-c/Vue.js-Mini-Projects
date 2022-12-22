<!-- eslint-disable vue/require-v-for-key -->
<template>
  <div class="container">
    <div class="inputs">
      <label>Degrees</label>
      <br />
      <input type="number" v-model="degree" />
      <select v-model="selectedType">
        <option v-for="(type, index) in types" :value="type" :key="index">
          {{ type }}
        </option>
      </select>
      <button @click="calculate()">Convert</button>
    </div>
    <div>
      <label for="">Result</label>
      <br />
      <span>{{ result }}</span>
    </div>
  </div>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      result: "result data",
      types: ["Fahrenheit", "Celcius"],
      selectedType: null,
      degree: null,
    };
  },
  methods: {
    calculate() {
      if (this.selectedType === null || this.degree === null) {
        alert("please fill in all fields");
      }
      this.selectedType == "Celcius"
        ? (this.result = fToCelcius(this.degree))
        : (this.result = celciusToF(this.degree));
    },
  },
};

function fToCelcius(degree) {
  return ((degree - 32) * 5) / 9;
}
function celciusToF(degree) {
  return degree * 1.8 + 32;
}
</script>
<style>
/* böyle css yazacaksan yazma be egemen. */
body {
  min-width: 100%;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #f8f9f9;
}
.container {
  background-color: #fff;
  padding: 50px;
  -webkit-box-shadow: 2px 3px 22px 7px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 2px 3px 22px 7px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 3px 22px 7px rgba(0, 0, 0, 0.57);
}
button {
  background-color: #559df8;
  padding: 5px;
  color: white;
  font-size: 16px;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}
label {
  font-size: 12px;
  color: rgb(106, 104, 104);
}
input,
select {
  padding: 5px;
  border: 1px solid rgb(201, 201, 201);
}
span {
  font-size: 16px;
  font-weight: 900;
}
</style>
