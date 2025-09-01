<script lang="ts">
  import FrameWhite from '$lib/assets/frame_white.svg';
  import FramePurp from '$lib/assets/frame_purp.svg';
  import FrameLightPurp from '$lib/assets/frame_lightpurp.svg';
  import FrameYel from '$lib/assets/frame_yel.svg';
  
  export let text = "Обучение с 29 сентября до середины ноября";
  export let number = 1;
  export let textColor = "var(--stsnyj-fioletovyj)";
  export let backgroundColor = "white";
</script>

<div class="training-card" style="background-color: {backgroundColor}">
  <div class="card-content">
    <div class="frames-container">
      <img src={FrameWhite} alt="Frame White" class="frame-image" />
      <img src={FramePurp} alt="Frame Purple" class="frame-image" />
      <img src={FrameLightPurp} alt="Frame Light Purple" class="frame-image" />
      <img src={FrameYel} alt="Frame Yellow" class="frame-image" />
    </div>
  </div>
</div>

<style>
  .training-card {
    border-radius: 0px 11px 22px 22px;
    flex-shrink: 0;
    width: 240px;
    height: 175px;
    position: relative;
    box-shadow: var(--ten-otdelnoj-papki-box-shadow);
    overflow: hidden;
  }

  .card-content {
    border-radius: 0px 0px 22px 22px;
    padding: 16px 13px 16px 13px;
    display: flex;
    flex-direction: column;
    gap: 16px;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
    position: relative;
  }

  .frames-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    gap: 8px;
    width: 100%;
    height: 100%;
    align-items: center;
    justify-items: center;
  }

  .frame-image {
    width: 80px;
    height: 80px;
    object-fit: contain;
    transition: transform 0.3s ease;
  }

  .frame-image:hover {
    transform: scale(1.1);
  }
</style>
