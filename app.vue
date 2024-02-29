<script setup lang="ts">
import { OrbitControls } from '@tresjs/cientos';

const gl = {
  clearColor: '#82DBC5',
  shadows: true,
  alpha: false,

};

const boxRef = shallowRef()
const { onLoop, pause, resume } = useRenderLoop()
onLoop(({ delta, elapsed }) => {
  if (boxRef.value) {
    boxRef.value.rotation.x += delta

  }
})

</script>

<template>
  <TresCanvas v-bind="gl" window-size>
    <TresPerspectiveCamera :position="[9, 9, 9]" />
    <OrbitControls :make-default="true" />
    <!-- <TransformControls :object="boxRef" /> -->
    <!-- <PointerLockControls make-default  />
    <KeyboardControls /> -->
    <TresGroup :position="[2, 0, 0]">

      <TresMesh ref="boxRef" cast-shadow>
        <TresBoxGeometry :args="[1, 1, 1]" />
        <TresMeshToonMaterial color="#4F4F4F" />
      </TresMesh>

    </TresGroup>
    <TresMesh @click="pause()" cast-shadow :position="[15, 0, 0]">
      <TresBoxGeometry :args="[3, 3, 3]" />
      <TresMeshToonMaterial color="#f0f" />
    </TresMesh>

    <TresMesh @click="resume()" cast-shadow :position="[-15, 0, 0]">
      <TresBoxGeometry :args="[3, 3, 3]" />
      <TresMeshToonMaterial color="#f0f" />
    </TresMesh>


    <TresDirectionalLight :position="[0, 2, 4]" :intensity="1.2" cast-shadow />
  </TresCanvas>
</template>

<style>
html,
body {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
}

#app {
  height: 100%;
  width: 100%;
  background-color: #000;
}
</style>