<template>
  <div class="body">
    <Header
      :pickedColor="pickedColor"
      :headerStyleBackgroundColor="headerStyleBackgroundColor"
    />
    <Navigator
      :isHard="isHard"
      :colorCount="colorCount"
      :init="init"
      :messageDisplay="messageDisplay"
      :restartButton="restartButton"
      @isHard="isHard = $event"
      @colorCount="colorCount = $event"
    />
    <Container 
      :colors="colors" 
      :ClickSquare="ClickSquare" />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Navigator from "./components/Navigator.vue";
import Container from "./components/Container.vue";
export default {
  name: "App",
  components: {
    Header,
    Navigator,
    Container
},
  mounted() {
    this.init();
  },
  data() {
    return {
      colorCount: 6,
      isHard: true,
      colors: [],
      pickedColor: "",
      restartButton: "",
      headerBackgroundColor: "",
      messageDisplay: "",
      msgDisplayStyleColor: "",
      headerStyleBackgroundColor: "",
    };
  },
  methods: {
    pickColor() {
      let quantity;
      if (this.isHard) {
        quantity = 6;
      } else {
        quantity = 3;
      }
      return Math.floor(Math.random() * quantity);
    },
    init() {
      this.colors = this.createNewColors(this.colorCount);
      this.pickedColor = this.colors[this.pickColor()];
      this.restartButton = "New Colors!";
      this.messageDisplay = "";
      this.headerStyleBackgroundColor = "steelblue";
    },
    createNewColors(numbers) {
      let arr = [];
      for (let i = 0; i < numbers; i++) {
        arr.push(this.createRandomStringColor());
      }
      return arr;
    },
    createRandomStringColor() {
      let newColor =
        "rgb(" +
        this.randomInt() +
        ", " +
        this.randomInt() +
        ", " +
        this.randomInt() +
        ")";
      return newColor;
    },
    randomInt() {
      return Math.floor(Math.random() * 256);
    },
    ClickSquare({ target }) {
      let clickedColor = target.style.backgroundColor;
      if (clickedColor === this.pickedColor) {
        this.messageDisplay = "You Picked Right!";
        this.setAllColorsTo(this.pickedColor);
        this.restartButton = "Play Again!";
        this.headerStyleBackgroundColor = this.pickedColor;
      } else {
        target.style.backgroundColor = "#232323";
        this.messageDisplay = "Try Again!";
        this.msgDisplayStyleColor = "#000000";
      }
    },
    setAllColorsTo(selectedColor) {
      this.colors = this.colors.map(() => selectedColor);
    },
  },
};
</script>

<style>
body {
  background: #232323;
  margin: 0;
  font-family: "Montserrat", "Avenir";
}

h1 {
  font-weight: normal;
  line-height: 1.1;
  padding: 20px 0;
}
</style>
