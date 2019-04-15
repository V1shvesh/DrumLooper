<template>
  <div class='beat-matrix'>
    <div
      class="beat-instrument"
      v-for="(instrument, instrumentIndex) in beatMatrix"
      :key="instrumentIndex"
    >
      <div
        class="beat-tab"
        v-for="(tab, tabIndex) in instrument"
        :class="{selected: beatMatrix[instrumentIndex][tabIndex]}"
        :key="tabIndex"
        @click="toggleBeatTabState(instrumentIndex, tabIndex)"
      >
        {{`${instrumentIndex}-${tabIndex}`}}
      </div>
    </div>
  </div>
</template>

<script>
import Tone from 'tone';

const noOfInstruments = 4;
const noOfBeats = 8;


export default {
  name: 'BeatMatrix',
  data() {
    return {
      beatMatrix: Array(noOfInstruments).fill(Array(noOfBeats).fill(false)),
      toneInstance: null,
    };
  },
  created() {
    /**
     * Mounts the Tone Sampler Instance
     */
    this.toneInstance = new Tone.Sampler({
      C3: './sounds/Kick.wav',
      D3: './sounds/Snare.wav',
      E3: './sounds/Snare.wav',
      F3: './sounds/Snare.wav',
    }, () => {
      this.toneInstance.triggerAttack('C3');
    }).toMaster();
    console.log(this.beatMatrix);
  },
  methods: {
    toggleBeatTabState(instrumentIndex, tabIndex) {
      this.$set(
        this.beatMatrix[instrumentIndex],
        tabIndex,
        !this.beatMatrix[instrumentIndex][tabIndex],
      );
    },
  },
  beforeDestroy() {
    /**
     * Disconnects the Tone Sampler Instance from Master Channel.
     * Helps avoid redundant Instances from playing in unison during re-renders
     */
    this.toneInstance.disconnect(Tone.Master);
  },
};
</script>

<style lang="scss">
  .beat-matrix {
    display: flex;
    flex-direction: column;
  }

  .beat-instrument {
    display: flex;
    flex-direction: row;
  }

  .beat-tab {
    width: 3em;
    height: 3em;
    margin: 4px;
  }

  .beat-tab:nth-child(8n+1),
  .beat-tab:nth-child(8n+2),
  .beat-tab:nth-child(8n+3),
  .beat-tab:nth-child(8n+4){
    background-color: #444;
  }

  .beat-tab:nth-child(8n+5),
  .beat-tab:nth-child(8n+6),
  .beat-tab:nth-child(8n+7),
  .beat-tab:nth-child(8n){
    background-color: #999;
  }

  .beat-tab.selected {
    background-color: #808;
  }
</style>
