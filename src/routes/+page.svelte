<script>
  import LogoHeader from '$lib/components/LogoHeader.svelte';
  import Header from '../components/Header.svelte';
  import TrainingCard from '$lib/components/TrainingCard.svelte';
  
  let name = '';
  let telegram = '';
  let education = '';
  let interests = [];

  let isSubmitting = false;
  let submitMessage = '';

  const handleSubmit = async (e) => {
    e.preventDefault();
    isSubmitting = true;
    submitMessage = '';

    try {
      const response = await fetch('YOUR_GOOGLE_APPS_SCRIPT_URL_HERE', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          name,
          telegram,
          education,
          interests
        })
      });

      const result = await response.json();
      
      if (result.success) {
        submitMessage = 'Форма успешно отправлена!';
        // Очищаем форму
        name = '';
        telegram = '';
        education = '';
        interests = [];
      } else {
        submitMessage = 'Ошибка при отправке: ' + result.error;
      }
    } catch (error) {
      submitMessage = 'Ошибка сети: ' + error.message;
    } finally {
      isSubmitting = false;
    }
  };
</script>

<style>
  :root {
    --primary-purple: #6a2d87;
    --secondary-yellow: #f9c300;
    --background-gradient: linear-gradient(135deg, #f8f0ff 0%, #fcdbfd 100%);
    --shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    --form-bg: #1a1a1a;
    --input-bg: #f5f5dc;
    --input-border: #e0e0c8;
    --text-light: #ffffff;
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

  .info-block h2 {
    font-size: 45px;
    margin: 0 0 1rem 0;
  }

  .info-block ul {
    list-style: disc;
    padding-left: 1.5rem;
    margin: 0;
  }

  .info-block li {
    margin-bottom: 0.5rem;
    font-size: 1.1rem;
  }

  .training-cards {
    display: flex;
    gap: 2rem;
    justify-content: center;
    flex-wrap: wrap;
  }

  .registration-section {
    padding: 3rem;
  }

  .registration-title {
    color: var(--primary-purple);
    font-size: 2.5rem;
    font-weight: 700;
    text-align: center;
    margin-bottom: 2.5rem;
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  .form-section {
    margin-bottom: 2rem;
  }

  .form-label {
    display: block;
    margin-bottom: 0.75rem;
    font-weight: 600;
    color: var(--primary-purple);
    font-size: 1.1rem;
  }

  .form-input {
    width: 100%;
    padding: 1.25rem;
    background: var(--input-bg);
    border: 2px solid var(--input-border);
    border-radius: 12px;
    font-size: 1rem;
    color: #333;
    transition: all 0.3s ease;
    box-sizing: border-box;
  }

  .form-input:focus {
    outline: none;
    border-color: var(--primary-purple);
    box-shadow: 0 0 0 3px rgba(106, 45, 135, 0.1);
    transform: translateY(-2px);
  }

  .form-input::placeholder {
    color: #999;
    font-style: italic;
  }

  .select-wrapper {
    position: relative;
  }

  .select-wrapper::after {
    content: '▼';
    position: absolute;
    right: 1.25rem;
    top: 50%;
    transform: translateY(-50%);
    color: var(--primary-purple);
    font-size: 0.8rem;
    pointer-events: none;
  }

  .form-select {
    appearance: none;
    background: var(--input-bg);
    cursor: pointer;
  }

  .submit-section {
    text-align: center;
    margin-top: 3rem;
  }

  .submit-button {
    background: var(--primary-purple);
    color: white;
    border: none;
    padding: 1.25rem 4rem;
    border-radius: 12px;
    font-size: 1.5rem;
    font-weight: 600;
    transition: all 0.3s ease;
    cursor: pointer;
    box-shadow: 0 4px 16px rgba(106, 45, 135, 0.3);
  }

  .submit-button:hover:not(:disabled) {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(106, 45, 135, 0.4);
  }

  .submit-button:disabled {
    opacity: 0.6;
    cursor: not-allowed;
    transform: none;
  }

  .privacy-link {
    color: var(--primary-purple);
    text-decoration: underline;
    font-weight: 500;
  }

  .submit-message {
    margin: 1rem 0;
    padding: 1rem;
    border-radius: 8px;
    font-weight: 600;
  }

  .submit-message.success {
    background: #d4edda;
    color: #155724;
    border: 1px solid #c3e6cb;
  }

  .submit-message.error {
    background: #f8d7da;
    color: #721c24;
    border: 1px solid #f5c6cb;
  }

  @media (max-width: 768px) {
    .registration-section {
      padding: 2rem 1.5rem;
    }
    
    .registration-title {
      font-size: 2rem;
    }
    
    .submit-button {
      padding: 1rem 2rem;
      font-size: 1.25rem;
    }
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

    <div class="registration-section">
      <h2 class="registration-title">Регистрация</h2>

      <form on:submit={handleSubmit}>
        <div class="form-section">
          <label for="name" class="form-label">Твое ФИО</label>
          <input 
            id="name" 
            type="text"
            bind:value={name} 
            placeholder="ФИО"
            class="form-input"
            required
          >
        </div>

        <div class="form-section">
          <label for="telegram" class="form-label">Твой Telegram</label>
          <input 
            id="telegram" 
            type="text"
            bind:value={telegram} 
            placeholder="@"
            class="form-input"
            required
          >
        </div>

        <div class="form-section">
          <label for="education" class="form-label">Твоя образовательная программа и учебная группа</label>
          <input 
            id="education" 
            type="text"
            bind:value={education} 
            placeholder="Например, «Медиакоммуникации, БМД251»"
            class="form-input"
            required
          >
        </div>

        <div class="form-section">
          <label for="interests" class="form-label">Расскажи, какие направления в ивенте тебя больше всего интересуют?</label>
          <div class="select-wrapper">
            <select 
              id="interests" 
              multiple 
              bind:value={interests}
              class="form-input form-select"
              required
            >
              <option value="marketing">Маркетинг и продвижение</option>
              <option value="organization">Организация мероприятий</option>
              <option value="creative">Креативное продюсирование</option>
              <option value="pr">PR и медиакоммуникации</option>
              <option value="logistics">Логистика и управление проектами</option>
            </select>
          </div>
        </div>

        <div class="submit-section">
          <button class="submit-button" disabled={isSubmitting}>
            {isSubmitting ? 'Отправка...' : 'Отправить'}
          </button>
          
          {#if submitMessage}
            <p class="submit-message {submitMessage.includes('успешно') ? 'success' : 'error'}">
              {submitMessage}
            </p>
          {/if}
          
          <p style="color: var(--text-light); margin-top: 1rem;">
            Нажимая кнопку ты соглашаешься с <a href="#" class="privacy-link">политикой конфиденциальности</a>
          </p>
        </div>
      </form>
    </div>
  </div>
</main>
