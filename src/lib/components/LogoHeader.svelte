<script>
  import InaccelLogo from '$lib/assets/inaccel-logo.svg';
</script>

<div class="logo-header">
  <div class="logo-container">
    <img src={InaccelLogo} alt="INACCEL" class="logo-accelerator">
  </div>
  <div class="text-container">
    <p>INACCEL — акселератор по event-менеджменту от Ингруп СтС.</p>
    <button class="registration-button">Регистрация</button>
  </div>
</div>

<style>
  .logo-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 80%;
  }

  .logo-container {
    position: relative;
    width: 320px;
  }

  .logo-accelerator {
    width: 100%;
  }

  .text-container {
    width: 450px;
    align-self: stretch;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  .text-container p {
    width: 80%;
    word-wrap: break-word;
    font-size: 28px;
  }

  .registration-button {
    background: var(--primary-purple);
    color: white;
    border: none;
    padding: 1rem 3rem;
    border-radius: 8px;
    font-size: 40px;
    transition: 0.3s;
    cursor: pointer;
    width: 100%;
  }
</style>
