<script>
  import InaccelLogo from '$lib/assets/inaccel-logo.svg';

  function scrollToRegistration() {
    const registrationSection = document.getElementById('registration');
    if (registrationSection) {
      registrationSection.scrollIntoView({ 
        behavior: 'smooth',
        block: 'start'
      });
    }
  }
</script>

<div class="logo-header">
  <div class="logo-container">
    <img src={InaccelLogo} alt="INACCEL" class="logo-accelerator">
  </div>
  <div class="text-container">
    <p>INACCEL — акселератор по event-менеджменту от Ингруп СтС.</p>
    <button class="registration-button" on:click={scrollToRegistration}>Регистрация</button>
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
    min-width: 107px;
  }

  .text-container {
    width: 450px;
    align-self: stretch;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    gap: 33px;
  }

  .text-container p {
    width: 80%;
    word-wrap: break-word;
    overflow-wrap: break-word;
    font-size: 28px;
    font-family: var(--font-raleway);
    max-width: 339px;
    color: var(--primary-purple);
    line-height: 1.3;
  }

  .registration-button {
    background: linear-gradient(45deg, var(--primary-purple) 0%, #7732AC 100%);
    color: white;
    border: none;
    border-radius: 15px;
    transition: all 0.3s ease;
    cursor: pointer;
    font-family: var(--font-raleway);
    font-weight: 600;
    width: auto;
  }

  .registration-button:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(62, 36, 91, 0.3);
  }

  .registration-button:active {
    transform: translateY(0);
  }

  /* Адаптивность для больших экранов */
  @media (min-width: 1200px) {
    .logo-header {
      width: 85%;
      gap: 20px;
    }
    
    .logo-container {
      width: 350px;
    }
    
    .text-container {
      width: 500px;
      gap: 40px;
    }
    
    .text-container p {
      font-size: 30px;
      max-width: 380px;
    }
    
    .registration-button {
      font-size: 25px;
      border-radius: 18px;
      padding: 10px 60px;
      width: auto;
    }
  }

  /* Адаптивность для средних экранов */
  @media (max-width: 1199px) and (min-width: 768px) {
    .logo-header {
      width: 85%;
    }
    
    .logo-container {
      width: 300px;
    }
    
    .text-container {
      width: 420px;
      gap: 30px;
    }
    
    .text-container p {
      font-size: 26px;
      max-width: 320px;
    }
    
    .registration-button {
      font-size: 40px;
      padding: 24px 102px;
      border-radius: 16px;
    }
  }

  /* Адаптивность для планшетов */
  @media (max-width: 767px) and (min-width: 481px) {
    .logo-header {
      width: 90%;
      flex-direction: row;
      gap: 20px;
      align-items: center;
    }
    
    .logo-container {
      width: 200px;
    }
    
    .text-container {
      width: auto;
      gap: 20px;
      align-items: flex-start;
      text-align: left;
    }
    
    .text-container p {
      font-size: 20px;
      max-width: 280px;
      width: auto;
    }
    
    .registration-button {
      font-size: 18px;
      padding: 6px 35px;
      border-radius: 12px;
      width: auto;
    }
  }

  /* Адаптивность для мобильных устройств */
  @media (max-width: 480px) {
    .logo-header {
      width: 95%;
      flex-direction: row;
      gap: 15px;
      align-items: center;
    }
    
    .logo-container {
      width: 120px;
    }
    
    .text-container {
      width: auto;
      gap: 12px;
      align-items: flex-start;
      text-align: left;
    }
    
    .text-container p {
      font-size: 12px;
      max-width: 180px;
      width: auto;
      line-height: 1.3;
      word-wrap: break-word;
      overflow-wrap: break-word;
    }
    
    .registration-button {
      font-size: 10px;
      padding: 4px 16px;
      border-radius: 8px;
      width: auto;
    }
    
    .registration-button:hover {
      transform: translateY(-1px);
      box-shadow: 0 4px 15px rgba(62, 36, 91, 0.25);
    }
  }

  /* Адаптивность для очень маленьких экранов */
  @media (max-width: 360px) {
    .logo-header {
      width: 98%;
      flex-direction: row;
      gap: 12px;
      align-items: center;
    }
    
    .logo-container {
      width: 80px;
    }
    
    .text-container {
      width: auto;
      gap: 8px;
      align-items: flex-start;
      text-align: left;
      font-size: 10px;
    }
    
    .text-container p {
      font-size: 10px;
      max-width: 160px;
      width: auto;
      line-height: 1.2;
      word-wrap: break-word;
      overflow-wrap: break-word;
    }
    
    .registration-button {
      font-size: 14px;
      padding: 3px 15px;
      border-radius: 6px;
      width: auto;
    }
  }

  /* Адаптивность для экстремально маленьких экранов */
  @media (max-width: 280px) {
    .logo-header {
      width: 100%;
      flex-direction: row;
      gap: 10px;
      align-items: center;
    }
    
    .logo-container {
      width: 60px;
    }
    
    .text-container {
      width: auto;
      gap: 6px;
      align-items: flex-start;
      text-align: left;
    }
    
    .text-container p {
      font-size: 10px;
      max-width: 80px;
      width: auto;
      line-height: 1.1;
      word-wrap: break-word;
      overflow-wrap: break-word;
    }
    
    .registration-button {
      font-size: 12px;
      padding: 2px 10px;
      border-radius: 4px;
      width: auto;
    }
  }

  /* Адаптивность для ландшафтной ориентации на мобильных */
  @media (max-width: 768px) and (orientation: landscape) {
    .logo-header {
      flex-direction: row;
      gap: 20px;
      align-items: center;
    }
    
    .logo-container {
      width: 180px;
    }
    
    .text-container {
      width: auto;
      gap: 15px;
      align-items: flex-start;
      text-align: left;
    }
    
    .text-container p {
      font-size: 16px;
      max-width: 250px;
      width: auto;
    }
    
    .registration-button {
      padding: 6px 35px;
      border-radius: 10px;
      width: auto;
    }
  }
</style>
