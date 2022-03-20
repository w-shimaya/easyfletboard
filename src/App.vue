<template>
  <div>
    <FletBoard :rootnote="rootnote" :scalename="scalename" />
    <p>
      <select v-model.number="rootnote">
        <option value="0">C</option>
        <option value="1">D♭</option>
        <option value="2">D</option>
        <option value="3">E♭</option>
        <option value="4">E</option>
        <option value="5">F</option>
        <option value="6">F♯/G♭</option>
        <option value="7">G</option>
        <option value="8">A♭</option>
        <option value="9">A</option>
        <option value="10">B♭</option>
        <option value="11">B</option>
      </select>
      <select v-model="scalename">
        <option value="ionian">Ionian/Major</option>
        <option value="dorian">Dorian</option>
        <option value="phrygian">Phrygian</option>
        <option value="lydian">Lydian</option>
        <option value="mixolydian">Mixolydian</option>
        <option value="aeorian">Aeorian/Natural Minor</option>
        <option value="locrian">Locrian</option>
        <option value="majseventh">Δ7 chord tone</option>
        <option value="minseventh">m7 chord tone</option>
        <option value="domseventh">7 chord tone</option>
        <option value="halfdim">φ chord tone</option>
      </select>
    </p>
  </div>
</template>

<script>
import FletBoard from "./components/FletBoard.vue";

export default {
  name: "App",
  components: {
    FletBoard,
  },
  data() {
    return {
      rootnote: 0,
      scalename: "ionian",
    };
  },
};
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
