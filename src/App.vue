<template>
  <div id="app">
    <div class="container">
      <h1 id="headline">Stadt Land Fluss</h1>

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
            <option value="3">3</option>
            <option value="4">4</option>
            <option value="5">5</option>
            <option value="6">6</option>
            <option value="7">7</option>
            <option value="8">8</option>
            <option value="9">9</option>
            <option value="10">10</option>
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

      <slfTemplate id="print-area" :theme="theme" :fields="fields" ref="slfTemp">
        <div v-for="item in items" :key="item" class="field"><span>{{ item }}</span></div>
        <div v-for="field in fields" :key="field" class="field" contentEditable="true">
          <span></span>
        </div>
      </slfTemplate>

      <Generator />
    </div>
  </div>
</template>

<script>
import slfTemplate from "./components/slfTemplate.vue";
import Generator from "./components/Generator.vue";
import json from './assets/categories.json';

export default {
  name: "app",
  components: {
    slfTemplate,
    Generator
  },
  data() {
    return {
      json,
      items: json["Standard"].slice(0, 4),
      theme: "Standard",
      cats: 3,
      rows: 5,
      fields: 25
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
    }
  },
  computed: {
    buildTheme() {
      let temp = this.json[this.theme].slice(0, this.cats + 1);
      temp.push(this.json[this.theme][11]);
      return temp;
    }
  },
  created() {
    let temp = this.json[this.theme].slice(0, this.cats + 1);
    temp.push(this.json[this.theme][11]);
    this.items = temp;
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Permanent+Marker&display=swap');

* {
  color: rgb(33, 32, 43);
  font-family: 'Permanent Marker', cursive;
  margin: 0;
  padding: 0;
}

:root {
  --primary: rgb(29, 29, 29);
  --secondaray: rgb(126, 126, 126);
  --accent: #007AA2;
  --hover: #86D5E7;
}

#app {
  width: 100vw;
  height: 100vh;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: url("https://images.pexels.com/photos/1919287/pexels-photo-1919287.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260");
  background-position: center center;
  background-size: cover;
}

.container {
  background-color: white;
  padding: 50px;
  margin: 25px;
  border-radius: 20px;
  box-shadow: 0px 3px 15px 0 rgba(0,0,0,0.75);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

#headline {
  font-family: 'Permanent Marker', cursive;
  font-size: 2.5em;
  margin-bottom: 50px;
}

.select {
  margin: 0 5px;
  border: none;
  font-size: 1em;
  color: var(--accent);
}

.select:hover {
  color: var(--hover);
}

.select:focus {
  outline: none;
}

#print-area {
  width: 100%;
  margin-top: 10px;
}

.button {
  background-color: var(--accent);
  color: white;
  border: none;
  border-radius: 4px;
  padding: 5px 10px;
}

.button:hover {
  background-color: var(--hover);
}

.button:active {
  position: relative;
  top: 2px;
  background-color: var(--accent);
}

.button:focus {
  outline: none;
}
</style>
