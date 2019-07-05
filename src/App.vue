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
          @change="changeTheme($event)"
          v-model="theme"
        >
          <option value="Standard">Standard</option>
          <option value="Krimi">Krimi</option>
          <option value="Quatsch">Quatsch</option>
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
          @change="changeCats($event)"
          v-model="cats"
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
          @change="changeRows($event)"
          v-model="rows"
        >
          <option value="5">5</option>
          <option value="10">10</option>
          <option value="15">15</option>
        </select>
      </label>
      <button
        class="button"
        @click="printTemplate('print-area')"
      >Drucken</button>
    </div>

    <div><span>Theme: {{theme}} Cats: {{cats}} Rows: {{rows}} Fields: {{fields}}</span></div>

    <slfTemplate id="print-area" :theme="theme" :fields="fields" ref="slfTemp">
      <div v-for="item in items" :key="item" class="field"><span>{{ item }}</span></div>
      <div v-for="field in fields" :key="field" class="field"><span style="display: none;">invisible</span></div>
    </slfTemplate>

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
import slfTemplate from "./components/slfTemplate.vue";
import json from './assets/categories.json';

export default {
  name: "app",
  components: {
    slfTemplate
  },
  data() {
    return {
      json,
      items: json["Standard"].slice(0, 5),
      theme: "Standard",
      cats: 4,
      rows: 5,
      fields: 30,
      result: "A"
    };
  },
  methods: {
    changeTheme(event) {
      this.theme = event.target.value;
      this.items = this.buildTheme;
    },
    changeCats(event) {
      this.cats = parseInt(event.target.value);
      this.$refs.slfTemp.$refs.frame.style["grid-template-columns"] = `auto repeat(${this.cats}, minmax(75px, auto)) auto`;
      this.items = this.buildTheme;
      this.fields = (this.cats + 2) * this.rows;
    },
    changeRows(event) {
      this.rows = parseInt(event.target.value);
      this.fields = (this.cats + 2) * this.rows;
    },
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
  },
  computed: {
    buildTheme() {
      let ulf = this.json[this.theme].slice(0, this.cats + 1);
      ulf.push(this.json[this.theme][10]);
      return ulf;
    }
  },
  created() {
    let ulf = this.json[this.theme].slice(0, 5);
    ulf.push(this.json[this.theme][10]);
    this.items = ulf;
  }
};
</script>

<style>
html,
body {
  color: rgb(33, 32, 43);
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
