<script>
  import InaccelLogo from '$lib/assets/inaccel-logo.svg';
  import IngroupLogo from '$lib/assets/ingroupctc-logo.svg';
  import Header from '../components/Header.svelte';
  
  let name = '';
  let telegram = '';
  let education = '';
  let interests = [];

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log('Submitted:', { name, telegram, education, interests });
  };
</script>

<style>
  :root {
    --primary-purple: #6a2d87;
    --secondary-yellow: #f9c300;
    --background-gradient: linear-gradient(135deg, #f8f0ff 0%, #fcdbfd 100%);
    --shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 4rem 2rem;
    display: flex;
    flex-direction: column;
    gap: 52px;
  }

  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .logo-container {
    position: relative;
    width: 200px;
  }

  .logo-accelerator {
    width: 100%;
  }

  .ingrup-logo {
    position: absolute;
    top: -20px;
    right: -50px;
    width: 150px;
  }

  .registration-button {
    background: var(--primary-purple);
    color: white;
    border: none;
    padding: 1rem 3rem;
    border-radius: 8px;
    font-size: 1.2rem;
    transition: 0.3s;
    cursor: pointer;
  }

  .info-block {
    background: var(--secondary-yellow);
    padding: 3rem;
    border-radius: 12px;
    box-shadow: var(--shadow);
  }

  .steps {
    display: flex;
    gap: 2rem;
  }

  .step {
    background: white;
    padding: 2rem;
    border-radius: 12px;
    box-shadow: var(--shadow);
    text-align: center;
    position: relative;
    width: 250px;
  }

  .step-number {
    position: absolute;
    bottom: -20px;
    left: 50%;
    transform: translateX(-50%);
    font-size: 6rem;
    opacity: 0.2;
    color: var(--primary-purple);
  }

  .form-section {
    margin-bottom: 4rem;
  }

  label {
    display: block;
    margin-bottom: 0.5rem;
    font-weight: 600;
  }

  input, textarea, select {
    width: 100%;
    padding: 1rem;
    border: 1px solid #ddd;
    border-radius: 8px;
    margin-bottom: 2rem;
  }

  .submit-button {
    background: var(--primary-purple);
    color: white;
    border: none;
    padding: 1rem 3rem;
    border-radius: 8px;
    font-size: 1.2rem;
    transition: 0.3s;
    cursor: pointer;
    margin-top: 2rem;
  }

  .privacy-link {
    color: var(--primary-purple);
    text-decoration: underline;
  }
</style>

<main>
  <div class="container">
    <Header />
    <div class="header">
      <div class="logo-container">
        <img src={InaccelLogo} alt="INACCEL" class="logo-accelerator">
      </div>
      <div>
        <p>INACCEL — акселератор по event-менеджменту от Ингруп СтС.</p>
        <button class="registration-button">Регистрация</button>
      </div>
      <img src={IngroupLogo} alt="Ингруп СтС" class="ingrup-logo">
    </div>

    <div class="info-block">
      <h2>INACCEL – это</h2>
      <ul>
        <li>Навык event-менеджмента с нуля всего за 6 недель</li>
        <li>Личное сопровождение от менторов</li>
        <li>Уникальная платформа с авторскими видео-лекциями</li>
        <li>Мастерские от экспертов индустрии</li>
        <li>Выход на новый уровень в креативной сфере</li>
      </ul>
    </div>

    <div class="steps">
      <div class="step" style="background: #fff5d9;">
        <p>Обучение с 29 сентября до середины ноября</p>
        <span class="step-number">1</span>
      </div>
      <div class="step" style="background: #e8d9ff;">
        <p>Разработка собственного ивента</p>
        <span class="step-number">2</span>
      </div>
      <div class="step" style="background: #d9d9ff;">
        <p>Комьюнити будущих ивентщиков</p>
        <span class="step-number">3</span>
      </div>
      <div class="step" style="background: #fff5d9;">
        <p>Твой старт во внеучебке Вышки</p>
        <span class="step-number">4</span>
      </div>
    </div>

    <h2>Регистрация</h2>

    <form on:submit={handleSubmit}>
      <div class="form-section">
        <label for="name">Твое ФИО</label>
        <input id="name" bind:value={name} placeholder="ФИО">
      </div>

      <div class="form-section">
        <label for="telegram">Твой Telegram</label>
        <input id="telegram" bind:value={telegram} placeholder="@">
      </div>

      <div class="form-section">
        <label for="education">Твоя образовательная программа и учебная группа</label>
        <textarea id="education" bind:value={education} placeholder="Например, «Медиакоммуникации, БМД251»"></textarea>
      </div>

      <div class="form-section">
        <label for="interests">Расскажи, какие направления в ивенте тебя больше всего интересуют?</label>
        <select id="interests" multiple bind:value={interests}>
          <option>Маркетинг и продвижение</option>
          <option>Организация мероприятий</option>
          <option>Креативное продюсирование</option>
          <option>PR и медиакоммуникации</option>
          <option>Логистика и управление проектами</option>
        </select>
      </div>

      <button class="submit-button">Отправить</button>
      <p>Нажимая кнопку ты соглашаешься с <a href="#" class="privacy-link">политикой конфиденциальности</a></p>
    </form>
  </div>
</main>
