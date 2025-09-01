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
    padding: 0 1rem;
    width: 100%;
    box-sizing: border-box;
  }

  .header-logo {
    height: 100%;
    width: auto;
    max-width: 200px;
    object-fit: contain;
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

  /* Адаптивность для больших экранов */
  @media (min-width: 1200px) {
    .header-component {
      height: 50px;
      padding: 0 2rem;
    }
    
    .header-logo {
      max-width: 250px;
    }
  }

  /* Адаптивность для средних экранов */
  @media (max-width: 1199px) and (min-width: 768px) {
    .header-component {
      height: 45px;
      padding: 0 1.5rem;
    }
    
    .header-logo {
      max-width: 220px;
    }
  }

  /* Адаптивность для планшетов */
  @media (max-width: 767px) and (min-width: 481px) {
    .header-component {
      height: 40px;
      padding: 0 1rem;
    }
    
    .header-logo {
      max-width: 180px;
    }
  }

  /* Адаптивность для мобильных устройств */
  @media (max-width: 480px) {
    .header-component {
      height: 30px;
      padding: 0 0.5rem;
      justify-content: flex-end;
    }
    
    .header-logo {
      max-width: 100px;
      height: 80%;
    }
    
    .header-link:hover {
      transform: scale(1.05);
    }
  }

  /* Адаптивность для очень маленьких экранов */
  @media (max-width: 360px) {
    .header-component {
      height: 25px;
      padding: 0 0.25rem;
    }
    
    .header-logo {
      max-width: 80px;
      height: 75%;
    }
  }

  /* Адаптивность для экстремально маленьких экранов */
  @media (max-width: 280px) {
    .header-component {
      height: 20px;
      padding: 0 0.25rem;
    }
    
    .header-logo {
      max-width: 60px;
      height: 70%;
    }
  }

  /* Адаптивность для ландшафтной ориентации на мобильных */
  @media (max-width: 768px) and (orientation: landscape) {
    .header-component {
      height: 25px;
      padding: 0 0.5rem;
    }
    
    .header-logo {
      max-width: 90px;
      height: 80%;
    }
  }

  /* Адаптивность с использованием vw для более точного масштабирования */
  @media (max-width: 480px) {
    .header-component {
      height: 8vw;
      min-height: 25px;
      max-height: 35px;
      padding: 0 2vw;
    }
    
    .header-logo {
      max-width: 25vw;
      min-width: 60px;
      max-width: 120px;
      height: 80%;
    }
  }

  /* Адаптивность для очень узких экранов */
  @media (max-width: 320px) {
    .header-component {
      height: 7vw;
      min-height: 20px;
      padding: 0 1.5vw;
    }
    
    .header-logo {
      max-width: 20vw;
      min-width: 50px;
      height: 75%;
    }
  }
</style>
