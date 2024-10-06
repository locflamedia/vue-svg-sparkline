<template>
  <main>
    <h2>SVG SparkLine Example</h2>
    <SparkLine
      :data="dataPoints"
      :width="width"
      :height="height"
      :stroke="stroke"
      :strokeColor="strokeColor"
      :fill="fill"
      :backgroundColor="backgroundColor"
      :opacity="opacity"
      :centerOffset="centerOffset"
      :amplitudeFactor="amplitudeFactor"
      :class="animationClass"
      @animationend="animationClass = ''"
    />
    <h3>Press Enter to apply changes for the inputs</h3>
    <div class="form-container">
      <div>
        <label>Width:</label>
        <input
          type="number"
          v-model="tempWidth"
          @keyup.enter="width = tempWidth"
        />
      </div>
      <div>
        <label>Height:</label>
        <input
          type="number"
          v-model="tempHeight"
          @keyup.enter="height = tempHeight"
        />
      </div>
      <div>
        <label>Stroke:</label>
        <input
          type="number"
          v-model="tempStroke"
          @keyup.enter="stroke = tempStroke"
        />
      </div>
      <div>
        <label>Stroke Color</label>
        <input type="color" v-model="strokeColor" />
      </div>
      <div>
        <label>Fill Color</label>
        <input type="color" v-model="fill" />
      </div>
      <div>
        <label>Background Color</label>
        <input type="color" v-model="backgroundColor" />
      </div>
      <div>
        <label>Opacity</label>
        <input
          type="number"
          v-model="tempOpacity"
          @keyup.enter="opacity = tempOpacity"
        />
      </div>
      <div>
        <label>Center Offset</label>
        <input
          type="number"
          v-model="tempCenterOffset"
          @keyup.enter="centerOffset = tempCenterOffset"
        />
      </div>
      <div>
        <label>Amplitude Factor</label>
        <input
          type="number"
          v-model="tempAmplitudeFactor"
          @keyup.enter="amplitudeFactor = tempAmplitudeFactor"
        />
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref, watch } from 'vue'
import SparkLine from './components/SparkLine.vue'

const dataPoints = [
  65605.49316578607, 65495.73327312595, 65483.5766220925, 65572.91228582137,
  65581.60377130368, 65597.09365064261, 65762.89489896805, 65635.49194243642,
  65814.50773734815, 65636.22650367954, 65756.8496125422, 65802.63199782168,
  65834.19396282289, 65810.72918645393, 65955.12768292298, 65828.7934295196,
  65898.99855442859, 65586.45298542893, 65527.11644598126, 65463.51029871186,
  64746.39422306732, 64396.475068537344, 64484.969411959624, 64433.83839159956,
  64537.123463429336, 64349.82336854003, 64587.99699957813, 64318.776746778014,
  63616.34230857029, 63568.17951393721, 63865.76587841092, 64022.25371999935,
  63833.48490125871, 63748.92772707046, 63583.09984434522, 63486.25842123686,
  63666.31684713173, 63449.59115410886, 63503.49356014067, 63791.957559365765,
  63686.79515140152, 63469.3026729772, 63356.22260582781, 63501.74133444947,
  63415.08962787346, 63412.18315733011, 63705.4811336735, 63757.081328592845,
  63800.85417413033, 64004.68196367795, 64080.50178633876, 64004.08662239725,
  63854.36636664453, 63914.18899810702, 63754.2937988693, 63662.60373432032,
  62961.686718729194, 62599.76795365424, 62593.86156482709, 62427.029171520604,
  62125.97948359865, 61956.825722575944, 61289.16593411256, 60773.960601536724,
  60862.73712876756, 60791.99680016752, 60942.07896643237, 61001.31173991391,
  61507.6161244618, 61750.7046005087, 61668.0154604511, 61470.54966687492,
  61501.28335760069, 61614.35553203237, 61675.92913789715, 61729.57748038025,
  61190.35950053192, 61293.74211108704, 61160.627929869916, 60873.64983332725,
  61497.550438711194, 61390.5193746096, 61824.45506572675, 61625.15477143684,
  61628.35209254788, 60821.807369266025, 60403.41735330646, 60896.05073328484,
  60706.71696375759, 60787.27856276344, 60627.058180398446, 61116.952773807825,
  60985.11168581431, 61126.91796468775, 61350.30877307984, 61309.02944358592,
  61195.121773880295, 61333.19084795601, 60798.5663906038, 60255.395066532634,
  60736.394429169755, 61038.40115605509, 60515.27472549693, 60476.171387359704,
  60444.80078445414, 60047.21023056539, 60603.02736816297, 60114.29109780189,
  60590.99061139087, 60578.342636079724, 61007.84632981549, 60603.79332990731,
  60809.95797483321, 60888.677276841765, 60764.622319062924, 60507.363739362074,
  61205.87676874549, 60922.44007317838, 61024.65291321176, 61022.732614198496,
  61127.61876284449, 61124.400852567356, 61438.61955380302, 61452.881049157106,
  61325.55145027494, 61283.407943760176, 61447.97523592585, 61783.04315946566,
  61237.01884317701, 61181.16559921016, 61824.1609830765, 62330.25296863748,
  61987.93935749957, 62335.022588537446, 62394.20409079485, 62365.29263794423,
  62275.09651258334, 62022.47161965773, 62094.41334605943, 62119.13760016322,
  61998.417167833686, 61796.61346195567, 61858.943006821515, 62017.72164133773,
  62139.39575349718, 62218.77511592513, 62102.5384037539, 62156.44108601213,
  62230.07343582251, 62213.386436766035, 62174.76483460754, 62307.202956879584,
  62181.65898585698, 62190.24835476746, 62189.414556279655, 61926.72757293198,
  62017.56963974981, 61868.52669264689, 61792.073086552715, 61764.447436375944,
  61844.53865265087, 61991.285312837215, 61943.32059194136, 61903.8513984402,
  62105.88392398104, 61972.5254215129, 61888.434969301474, 61875.00799886143,
]
const width = ref(800)
const height = ref(400)
const stroke = ref(1)
const strokeColor = ref('#14b8a6')
const fill = ref('#0d9488')
const backgroundColor = ref('#f0f8ff')
const opacity = ref(10)
const centerOffset = ref(2)
const amplitudeFactor = ref(5)

const animationClass = ref('')

const tempWidth = ref(width.value)
const tempHeight = ref(height.value)
const tempStroke = ref(stroke.value)
const tempOpacity = ref(opacity.value)
const tempCenterOffset = ref(centerOffset.value)
const tempAmplitudeFactor = ref(amplitudeFactor.value)

watch([width, height, stroke, opacity, centerOffset, amplitudeFactor], () => {
  animationClass.value = 'sparkline-changed'
})
</script>

<style>
@keyframes highlight {
  0% {
    transform: scale(1);
    box-shadow: 0 0 0 rgba(0, 0, 0, 0);
  }
  50% {
    transform: scale(1.05);
    box-shadow: 0 4px 15px rgba(20, 184, 166, 0.3);
  }
  100% {
    transform: scale(1);
    box-shadow: 0 0 0 rgba(0, 0, 0, 0);
  }
}

/* Định nghĩa lớp animation */
.sparkline-changed {
  animation: highlight 0.5s ease-in-out;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

main {
  background: #f0f8ff;
  border-radius: 15px;
  padding: 30px;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
  max-width: 900px;
  margin: 20px auto;
}

h2 {
  font-size: 28px;
  color: #14b8a6;
  margin-bottom: 30px;
  letter-spacing: 1.5px;
}
h3 {
  color: #14b8a6;
}

.form-container {
  margin-top: 15px;
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  justify-content: space-between;
}

.form-container > div {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: calc(33.33% - 20px);
  transition: transform 0.2s ease-in-out;
}

.form-container > div:hover {
  transform: translateY(-5px);
}

label {
  font-weight: 600;
  margin-bottom: 5px;
  color: #0d9488;
}

input[type='number'],
input[type='color'] {
  box-sizing: border-box;
  text-align: center;
  border-radius: 5px;
  border: 1px solid #14b8a6;
  margin-top: 5px;
  width: 100%;
}

input[type='number'] {
  padding: 8px;
}

input[type='color'] {
  height: 34px;
}

input:focus {
  outline: none;
  border-color: #0d9488;
}

@media (max-width: 768px) {
  main {
    padding: 20px;
  }

  .form-container > div {
    width: 100%;
  }
}
</style>
