<template>
  <div id="app">
    <HeaderBar />
    <div class="main-section columns">
      <main class="column">
        <MachineCard />
      </main>
    </div>
  </div>
</template>

<script>
import HeaderBar from '@/components/header-bar';
import MachineCard from '@/components/MachineCard';

export default {
  name: 'App',
  components: { HeaderBar, MachineCard },
};
</script>

<style lang="scss">
@import '@/design/index.scss';
</style>
