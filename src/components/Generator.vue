<template>
  <div class="generator">
    <div class="description">
      <p>Drücke den Knopf um ein zufälligen Buchstaben zu genereieren.</p>
    </div>

    <div
      class="generate-btn"
      @click="randomChar"
    >
      <p id="result">{{ result }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "Generator",
  data() {
    return {
      result: "A",
      charArr: []
    };
  },
  methods: {
    randomChar() {
      if (this.charArr.length === 0) {
        for (let i = 0; i < 26; i++) {
          this.charArr.push(String.fromCharCode(65 + i));
        }
        alert("Das waren alle Buchstaben, jetzt geht es von vorne los!");
      }

      let randomNum = Math.floor(Math.random() * Math.floor(this.charArr.length - 1));

      this.result = this.charArr[randomNum];
      this.charArr.splice(randomNum, 1);
    }
  },
  created() {
    for (let i = 0; i < 26; i++) {
      this.charArr.push(String.fromCharCode(65 + i));
    }
  }
};
</script>

<style>
.generator {
  display: grid;
  grid-template-columns: repeat(2, auto);
  margin-top: 25px;
}

.generate-btn {
  grid-column: 2 / 3;
  justify-self: end;
  margin-left: 10px;
  background-color: var(--accent);
  width: 75px;
  height: 75px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.generate-btn:hover {
  background-color: var(--hover);
  cursor: pointer;
}

.generate-btn:active {
  background-color: var(--accent);
  position: relative;
  top: 2px;
}

.generate-btn:focus {
  outline: none;
}

#result {
  color: white;
  font-size: 3em;
  margin: 10px;
  user-select: none;
}

.description {
  grid-column: 1 / 2;
  align-self: center;
  text-align: right;
  margin-right: 10px;
  max-width: 300px;
}
</style>
