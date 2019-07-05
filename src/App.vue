<template>
  <div id="app">
    <h1>Stadt Land Fluss</h1>

    <div class="selection-menu">
      <label
        for="theme"
        class="label"
      >
        Theme:
        <select
          name="theme"
          id="theme"
          class="select"
        >
          <option value="1">Standard</option>
          <option value="2">Krimi</option>
          <option value="3">Quatsch</option>
        </select>
      </label>
      <label
        for="categories"
        class="label"
      >
        Kategorien:
        <select
          name="categories"
          id="categories"
          class="select"
        >
          <option value="4">4</option>
          <option value="5">5</option>
          <option value="6">6</option>
          <option value="7">7</option>
          <option value="8">8</option>
          <option value="9">9</option>
        </select>
      </label>
      <label
        for="rows"
        class="label"
      >
        Reihen:
        <select
          name="rows"
          id="rows"
          class="select"
        >
          <option value="5">5</option>
          <option value="10">10</option>
          <option value="15">15</option>
        </select>
      </label>
      <button
        class="button"
        @click="printTemplate('printArea')"
      >Drucken</button>
    </div>

    <Template id="printArea" />

    <div class="generator">
      <p id="result">{{ result }}</p>
      <button
        class="button"
        @click="randomChar"
      >LOS!</button>
    </div>
  </div>
</template>

<script>
import Template from "./components/Template.vue";

export default {
  name: "app",
  components: {
    Template
  },
  data() {
    return {
      result: "A"
    };
  },
  methods: {
    printTemplate(divName) {
      let printContents = document.getElementById(divName).innerHTML;
      let originalContents = document.body.innerHTML;
      document.body.innerHTML = printContents;
      window.print();
      document.body.innerHTML = originalContents;
    },
    randomChar() {
      let randomNum = Math.random() * (90 - 65) + 65;
      this.result = String.fromCharCode(randomNum);
      // TODO: remove already selected chars from pool
    }
  }
};
</script>

<style>
html,
body {
  color: black;
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

#app {
  background-color: white;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
