<template>
  <WebGLScene />

  <BufferPage>
    <Preloader>
      <slot />
    </Preloader>
  </BufferPage>
</template>

<script setup lang="ts">
import { BufferPage, useFlowProvider } from '@nam-hai/water-flow';

const { $lenis } = useNuxtApp()

const flowProvider = useFlowProvider()



useRaf((e) => {
  !flowProvider.flowIsHijacked && $lenis.raf(e.elapsed)
}, {firstStack: true})

onMounted(() => {
  $lenis.scrollTo('top')
})

flowProvider.registerScrollInterface({
  resume: ()=> $lenis.start(),
  stop:  ()=> $lenis.stop(),
  scrollToTop: () => { $lenis.scrollTo('top', { immediate: true }) }
})

</script>

<style lang="scss" scoped></style>
