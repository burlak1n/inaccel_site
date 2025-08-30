<script>
  import IngroupLogo from '$lib/assets/ingroupctc-logo.svg';
</script>

<header class="header-component">
  <a href="https://ingroupsts.ru/" target="_blank" rel="noopener noreferrer" class="header-link">
    <img src={IngroupLogo} alt="Ингруп СтС" class="header-logo">
  </a>
</header>

<style>
  .header-component {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    height: 40px;
  }

  .header-logo {
    height: 100%;
    width: auto;
  }

  .header-link {
    display: flex;
    align-items: center;
    height: 100%;
    text-decoration: none;
    transition: all 0.3s ease;
  }

  .header-link:hover {
    transform: scale(1.1);
    filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.02));
  }
</style>
