<script>
  import LogoHeader from '$lib/components/LogoHeader.svelte';
  import Header from '../components/Header.svelte';
  import TrainingCard from '$lib/components/TrainingCard.svelte';
  
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

  .info-block {
    background: var(--secondary-yellow);
    padding: 3rem;
    border-radius: 12px;
    box-shadow: var(--shadow);
  }

  .training-cards {
    display: flex;
    gap: 2rem;
    justify-content: center;
    flex-wrap: wrap;
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
    font-size: 40px;
    transition: 0.3s;
    cursor: pointer;
    margin-top: 2rem;
    display: block;
    margin-left: auto;
    margin-right: auto;
  }

  .submit-section {
    text-align: center;
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
    <LogoHeader />

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

    <div class="training-cards">
      <TrainingCard 
        text="Обучение с 29 сентября до середины ноября"
        number={1}
        backgroundColor="#fff5d9"
        textColor="var(--primary-purple)"
      />
      <TrainingCard 
        text="Разработка собственного ивента"
        number={2}
        backgroundColor="#e8d9ff"
        textColor="var(--primary-purple)"
      />
      <TrainingCard 
        text="Комьюнити будущих ивентщиков"
        number={3}
        backgroundColor="#d9d9ff"
        textColor="var(--primary-purple)"
      />
      <TrainingCard 
        text="Твой старт во внеучебке Вышки"
        number={4}
        backgroundColor="#fff5d9"
        textColor="var(--primary-purple)"
      />
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

      <div class="submit-section">
        <button class="submit-button">Отправить</button>
        <p>Нажимая кнопку ты соглашаешься с <a href="#" class="privacy-link">политикой конфиденциальности</a></p>
      </div>
    </form>
  </div>
</main>
