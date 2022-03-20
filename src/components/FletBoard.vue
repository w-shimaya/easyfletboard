<template>
  <canvas width="800" height="200" class="canvas"></canvas>
</template>

<script>
const SCALES = {
  ionian: [0, 2, 4, 5, 7, 9, 11],
  dorian: [0, 2, 3, 5, 7, 9, 10],
  phrygian: [0, 1, 3, 5, 7, 8, 10],
  lydian: [0, 2, 4, 6, 7, 9, 11],
  mixolydian: [0, 2, 4, 5, 7, 9, 10],
  aeorian: [0, 2, 3, 5, 7, 8, 10],
  locrian: [0, 1, 3, 5, 6, 8, 10],
};

const INT_NAME = [
  "R",
  "♭9",
  "9",
  "m3",
  "Δ3",
  "11",
  "♯11",
  "P5",
  "♭13",
  "13",
  "m7",
  "Δ7",
];

const INT_COLOR = [
  "#3cba1c", // r
  "#401a82", // -9
  "#8b5bde", // 9
  "#253878", // -3
  "#476ce6", // M3
  "#edcf21", // P4/11
  "#877614", // +11/-5
  "#c24023", // P5
  "#6e1b42", // -13
  "#de689f", // 13
  "#14854a", // -7
  "#2ae886", // M7
];

export default {
  props: {
    rootnote: {
      type: Number,
      default: 0,
    },
    opennote: {
      type: Array,
      default: () => [4, 9, 2, 7, 11, 4],
    },
    scalename: {
      type: String,
      default: "ionian",
    },
  },
  watch: {
    rootnote() {
      this.draw();
    },
    scalename() {
      this.draw();
    },
  },
  methods: {
    draw() {
      // clear
      this.ctx.beginPath();
      this.ctx.clearRect(0, 0, 800, 200);
      // draw strings
      for (let i = 0; i < 6; i++) {
        this.ctx.beginPath();
        this.ctx.moveTo(800 / 12, 25 + ((200 - 2 * 25) / 5) * i);
        this.ctx.lineTo(800, 25 + ((200 - 2 * 25) / 5) * i);
        this.ctx.closePath();
        this.ctx.stroke();
      }
      // draw flets
      this.ctx.textAlign = "center";
      this.ctx.font = "15pt Tahoma";
      this.ctx.textBaseline = "bottom";
      this.ctx.fillStyle = "black";
      for (let i = 0; i < 11; i++) {
        this.ctx.beginPath();
        let x = (800 / 12) * (i + 1);
        this.ctx.moveTo(x, 25);
        this.ctx.lineTo(x, 200 - 25);
        this.ctx.closePath();
        this.ctx.stroke();
        if (i == 5 || i == 7 || i == 9 || i == 12) {
          this.ctx.fillText(i.toString(), x, 200);
        }
      }
      // draw notes
      // root
      this.ctx.textAlign = "center";
      this.ctx.font = "13pt Tahoma";
      this.ctx.textBaseline = "middle";
      for (let s = 0; s < 6; s++) {
        for (let f = 0; f < 11; f++) {
          let interval = (this.opennote[s] + f + 12 - this.rootnote) % 12;
          let x = 800 / 24 + (800 / 12) * f;
          let y = 25 + ((200 - 2 * 25) / 5) * (5 - s);
          if (SCALES[this.scalename].includes(interval)) {
            this.ctx.fillStyle = INT_COLOR[interval];
            this.ctx.beginPath();
            this.ctx.arc(x, y, 14, 0, Math.PI * 2);
            this.ctx.fill();
            this.ctx.fillStyle = "white";
            this.ctx.fillText(INT_NAME[interval], x, y);
          }
        }
      }
    },
  },
  mounted() {
    this.ctx = this.$el.getContext("2d");
    this.draw();
  },
};
</script>

<style scoped>
</style>