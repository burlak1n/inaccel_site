<script lang="ts">
  export let text = "Обучение с 29 сентября до середины ноября";
  export let number = 1;
  export let textColor = "var(--stsnyj-fioletovyj)";
  export let backgroundColor = "white";
</script>

<div class="training-card" style="background-color: {backgroundColor}">
  <div class="card-content">
          <div class="text-content">
        <div class="training-text" style="color: {textColor}">
          {text}
        </div>
        <div class="number-display" style="color: {textColor}">
          {number}
        </div>
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



  .text-content {
    padding: 7px 21px 0px 5px;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    justify-content: flex-end;
    flex-shrink: 0;
    width: 213px;
    position: relative;
  }

  .training-text {
    text-align: left;
    font-family: 'Raleway-Medium', sans-serif;
    font-size: 21px;
    font-weight: 500;
    position: relative;
    align-self: stretch;
    line-height: 1.3;
    word-wrap: break-word;
    overflow-wrap: break-word;
  }

  .number-display {
    margin: 0;
    color: var(--stsnyj-fioletovyj);
    text-align: left;
    font-family: 'Mont-Bold', sans-serif;
    font-size: 80px;
    font-weight: 700;
    position: relative;
  }
</style>
