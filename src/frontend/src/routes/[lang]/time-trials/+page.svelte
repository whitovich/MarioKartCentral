<script lang="ts">
  import Section from '$lib/components/common/Section.svelte';
  import Button from '$lib/components/common/buttons/Button.svelte';
  import { page } from '$app/stores';
  import LL from '$i18n/i18n-svelte';
  import MK8DX from '$lib/assets/logo_mk8dx.png';
  import MK8 from '$lib/assets/logo_mk8.png';
  import MK7 from '$lib/assets/logo_mk7.png';
  import MKW from '$lib/assets/logo_mkw.png';
</script>

<Section header={$LL.NAVBAR.TIME_TRIALS()}>
  <div slot="header_content"></div>
  <div>
    <p>
      {$LL.TIME_TRIALS.DESCRIPTION()}
    </p>
  </div>
  
  <div style="display: flex; flex-wrap: wrap; gap: 10px; justify-content: center;">
    <a href="/{$page.params.lang}/time-trials/mk8dx">
      <Button size="xl">
        <img src={MK8DX} alt="Mario Kart 8 Deluxe"/>
      </Button>
    </a>
    <a href="/{$page.params.lang}/time-trials/mk8">
      <Button size="xl">
        <img src={MK8} alt="Mario Kart 8"/>
      </Button>
    </a>
    <a href="/{$page.params.lang}/time-trials/mk7">
      <Button size="xl">
        <img src={MK7} alt="Mario Kart 7"/>
      </Button>
    </a>
    <a href="/{$page.params.lang}/time-trials/mkw">
      <Button size="xl">
        <img src={MKW} alt="Mario Kart Wii"/>
      </Button>
    </a>
  </div>
</Section>

<style>
  img {
    height: 50px;
    object-fit: scale-down;
  }
</style>
