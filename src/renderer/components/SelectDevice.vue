<template class="task-template">
    <section id="devices-section" class="section js-section u-category-native-ui">
        <header class="section-header">
            <div class="section-wrapper">
                <h1>
                    <svg class="section-icon"><use xlink:href="assets/img/icons.svg#icon-native-ui"></use></svg>녹화 장비 선택
                </h1>
                
                <h3>카메라, 프리렌테이션 스크린 마이크를 선택하는 화면</h3>
                
                <p>강의 녹화 시작 전에 해당 장비들이 선택되어 있어야 정상적인 녹화가 가능합니다. </p>
            </div>
        </header>
        <div class="demo">
            <div class="demo-wrapper">
                <button id="open-file-demo-toggle" class="js-container-target demo-toggle-button" style="display:inline;">Camera
                    <div class="demo-meta u-avoid-clicks">Information: <span class="demo-meta-divider">선택 없음</span> </div>
                </button>
                <select v-model="selectCamera">
                  <option v-for="option in cameras" v-bind:value="option.value" v-bind:key="option.name">
                    {{option.name}}
                  </option>
                </select>
            <span class="demo-controls" style="float: right !important; margin-top: 15px;">
                <button class="demo-button" id="select-camera" v-on:click="clickme">선택</button>
            </span>
            </div>
        </div>
    </section>
</template>

<script>
export default {
  data () {
    return {
      selectCamera: '',
      cameras: []
    }
  },
  methods: {
    clickme () {
      alert(this.selectCamera)
    },
    getDevices () {
      let self = this
      const ffdevices = require('ffdevices')
      ffdevices.getAll(function (error, devices) {
        if (!error) {
          self.addCameralist(devices)
        } else {
          console.log('getFfmpegDevices > error :', error)
        }
      })
    },
    addCameralist (devices) {
      console.log('devices> :', devices)
      this.selectCamera = devices[0].name
      devices.forEach((item) => {
        let flag = false
        if (item.os === 'darwin') {
          (item.type !== 'audio') ? flag = true : flag = false
        }
        if (flag === true) {
          this.cameras.push(item)
        }
      })
    }
  },
  mounted () {
    this.getDevices()
  }
}
</script>

<style>
/* Demo */

.demo:first-of-type {
  margin-top: 2rem;
}
.demo:last-of-type {
  margin-bottom: 2rem;
}
@media (min-width: 940px) {
  .demo:last-of-type {
    margin-bottom: 4rem;
  }
}

.demo-wrapper {
  position: relative;
  max-width: 740px;
  margin: 0 auto;
  padding: 0 2rem;
}


/* Toggle Button ----------------------------- */

.demo-toggle-button {
  position: relative;
  display: block;
  margin: 0;
  padding: .5em 1.5em;
  line-height: 1.5;
  font: inherit;
  font-weight: 600;
  font-size: 1.2em;
  text-align: left;
  border: none;
  color: inherit;
  background-color: transparent;
  transition: border-color .12s;
  outline: none;
}

.demo-toggle-button:before,
.demo-toggle-button:after {
  content: "";
  position: absolute;
  left: 0;
  width: 2px;
  height: 50%;
  background-color: hsl(0,0%,88%);
  transition: transform .2s cubic-bezier(.4,.1,0,1);
}
.demo-toggle-button:before {
  top: 0;
  transform-origin: bottom center;
  transform: translateX(.7em) rotate(-30deg) scale(.75);
}
.demo-toggle-button:after {
  bottom: 0;
  transform-origin: top center;
  transform: translateX(.7em) rotate(30deg) scale(.75);
}
.is-open .demo-toggle-button:before,
.is-open .demo-toggle-button:after {
  transform: rotate(0deg);
}
.demo-toggle-button:focus:before,
.demo-toggle-button:focus:after {
  background-color: currentColor;
}

/* Meta info */

.demo-meta {
  margin-top: .2em;
  font-size: 11px;
  font-weight: 300;
  text-transform: uppercase;
  color: var(--color-subtle);
}
.demo-meta-divider {
  margin: 0 .5em;
}


/* Demo Box ----------------------------- */

.demo-box {
  display: none;
  position: relative;
  padding: 2em;
  margin-top: 1em;
  margin-bottom: 2em;
  border-radius: 6px;
  border: 1px solid var(--color-border);
  background-color: var(--color-bg);
}
.demo-box:before {
  content: "";
  position: absolute;
  top: -11px;
  width: 20px;
  height: 20px;
  background-color: inherit;
  border-top: inherit;
  border-right: inherit;
  border-top-right-radius: 3px;
  transform: rotate(-45deg);
}

.is-open .demo-box {
  display: block;
  animation: demo-box-fade-in .2s cubic-bezier(0, .20, .20, .96);
}
@keyframes demo-box-fade-in {
    0% { opacity: 0; transform: translateY(-20px); }
  100% { opacity: 1; transform: translateY(0); }
}

.demo-box > p:first-child {
  margin-top: 0;
}

.demo-box h5 {
  font-size: 1em;
  margin-bottom: .6em;
}


/* Demo Controls ----------------------------- */

.demo-controls {
  display: flex;
  align-items: center;
}
.rec-button {
  align-self: flex-start;
  margin-right: 1em;
  border: 2px solid;
  border-radius: 4px;
  font: inherit;
  font-size: 1.2em;
  padding: .4em 1.2em;
  color: red;
  background-color: transparent;
}
.stop-button {
  align-self: flex-start;
  margin-right: 1em;
  border: 2px solid;
  border-radius: 4px;
  font: inherit;
  font-size: 1.2em;
  padding: .4em 1.2em;
  color: dodgerblue;
  background-color: transparent;
}
.rec-button {
  align-self: flex-start;
  margin-right: 1em;
  border: 2px solid;
  border-radius: 4px;
  font: inherit;
  font-size: 1.2em;
  padding: .4em 1.2em;
  color: red;
  background-color: transparent;
}
.stop-button {
  align-self: flex-start;
  margin-right: 1em;
  border: 2px solid;
  border-radius: 4px;
  font: inherit;
  font-size: 1.2em;
  padding: .4em 1.2em;
  color: dodgerblue;
  background-color: transparent;
}
.play-button {
  align-self: flex-start;
  margin-right: 1em;
  border: 2px solid;
  border-radius: 4px;
  font: inherit;
  font-size: 1.2em;
  padding: .4em 1.2em;
  color: yellowgreen;
  background-color: transparent;
}
.play-button {
  align-self: flex-start;
  margin-right: 1em;
  border: 2px solid;
  border-radius: 4px;
  font: inherit;
  font-size: 1.2em;
  padding: .4em 1.2em;
  color: yellowgreen;
  background-color: transparent;
}
.demo-button {
  align-self: flex-start;
  margin-right: 1em;
  border: 2px solid;
  border-radius: 4px;
  font: inherit;
  font-size: 1.2em;
  padding: .4em 1.2em;
  color: inherit;
  background-color: transparent;
}
.demo-button:focus {
  outline: none;
  background-color: white;
}
.demo-button:active {
  border-color: var(--color-border);
}

.demo-input {
  flex: 1;
  border: 2px solid var(--color-border);
  border-radius: 4px;
  font: inherit;
  font-size: 1.2em;
  padding: .4em .8em;
  color: inherit;
  background-color: transparent;
}
.demo-input:focus {
  outline: none;
  border-color: hsl(0,0%,80%);
  background-color: white;
}

.demo-response {
  flex: 1;
  word-break: break-word;
}

.smooth-appear {
  opacity: 1;
  transition: opacity .5s ease-in-out;
}

.disappear {
  opacity: 0;
}
.demo-button.smooth-disappear:focus {
  outline: inherit;
  border-color: inherit;
  background-color: inherit;
}

/* ProTip ----------------------------- */

.demo-protip {
  margin-top: 2rem;
  padding: 1.5rem 2rem 2rem 2rem;
  border: 1px solid hsla(0,0%,0%,.06);
  border-radius: 6px;
  background: var(--color-accent) linear-gradient(hsla(0,0%,100%,.85), hsla(0,0%,100%,.85));
}
.demo-protip h2 {
  margin: 0 0 .5rem 0;
}
.demo-protip strong {
  font-weight: 600;
}


</style>