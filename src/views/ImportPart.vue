<template>

<a
    href="#/app/andon/importpart"
    class="menu-right"
    style="position: fixed; z-index: 99; right: 0; text-decoration: none"
  >
    <button
      class="fullscreen-btn"
      v-if="!isFullScreen"
      @click="toggleFullScreen"
    >
      <svg
        width="24"
        height="24"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round"
        class="feather feather-maximize"
      >
        <path d="M8 3H5a2 2 0 0 0-2 2v3" />
        <path d="M16 3h3a2 2 0 0 1 2 2v3" />
        <path d="M8 21H5a2 2 0 0 1-2-2v-3" />
        <path d="M16 21h3a2 2 0 0 0 2-2v-3" />
      </svg>
      <span>Fullscreen</span>
    </button>
  </a>  

  <h1 style="text-align: center; background-color: black;position: fixed;color: #ffffff;font-size: 6rem;font-weight: bolder ;z-index: 99;width: 90%;margin: 25% 5%">UNDER CONSTRUCTION</h1>
  <div style="background-color: #e0e0e0; height: 100vh;
  filter: blur(5px);
  ">
    <Head :area="area" />
    <ModuleStock class="mb-2" :moduleTMC="moduleTMC" :moduleSTM="moduleSTM" :moduleUMWT="moduleUMWT" :moduleTMV="moduleTMV" :stdModule="stdModule" :styleTMC="styleTMC"/>
<div class="row d-flex">
  <PalletComplete class="col-12 col-md-6 pe-0 pe-md-1" :pLine="pLine" :counter="counter" :pLineStd="pLineStd"/>
  <NextTruckImport :curTruck="curTruck"  :planeTime="planeTime" class="col-12 col-md-6 ps-0 ps-md-1"/>
</div>
  </div>
</template>

<script>
import NextTruckImport from '@/components/NextTruckImport.vue'
import ModuleStock from '@/components/ModuleStock.vue'
import Head from '@/components/Head.vue';
import PalletComplete from '@/components/PalletComplete.vue';
export default {
  name: 'importPart',
  components: {
    ModuleStock ,
    NextTruckImport,
    Head,
    PalletComplete
  },
  data() {
    return {
      area: 'IMPORT', 
//moduleStock
moduleTMC: 5,
moduleSTM: 10,
moduleUMWT: 8,
moduleTMV: 9,
stdModule:8,
pLine: 12,
counter: 13,
pLineStd: 2,
//nextTruck
curTruck: 'Rz-02-01',
planeTime: 60,
    }
  },
  mounted() {
    // Update the date every minute

    // Event listener to track fullscreen changes
    document.addEventListener('fullscreenchange', this.checkFullScreen)
  },
  methods: {
    toggleFullScreen() {
      const doc = document.documentElement
      if (!document.fullscreenElement) {
        doc.requestFullscreen().catch((err) => {
          alert(
            `Error attempting to enable full-screen mode: ${err.message} (${err.name})`,
          )
        })
      } else {
        document.exitFullscreen()
      }
    },
    checkFullScreen() {
      this.isFullScreen = !document.fullscreenElement
    },
  },
  beforeDestroy() {
    document.removeEventListener('fullscreenchange', this.checkFullScreen)
  },
}
</script>

<style>
.fullscreen-btn {
  right: 0;
  background-color: #910404;
  color: white;
  font-weight: bold;
  border: none;
  cursor: pointer;
  padding: 10px 15px;
  border-radius: 5px;
  display: flex;
  align-items: center;
  font-size: 16px;
}

.fullscreen-btn svg {
  margin-right: 5px;
}

.fullscreen-btn:hover {
  background-color: #0056b3;
}</style>
