
<script lang="ts">
  import LogoHeader from '$lib/components/LogoHeader.svelte';
  import Header from '../components/Header.svelte';
  import TrainingCard from '$lib/components/TrainingCard.svelte';
  import FrameWhite from '$lib/assets/frame_white.svg';
  import FramePurp from '$lib/assets/frame_purp.svg';
  import FrameLightPurp from '$lib/assets/frame_lightpurp.svg';
  import FrameYel from '$lib/assets/frame_yel.svg';




  
  let name = '';
  let telegram = '';
  let education = '';
  let interests: string[] = [];

  // Доступные теги
  const availableTags = [
    'Управление процессами',
    'Управление человеческим ресурсом',
    'Создание собственного проекта',
    'Креатив',
    'Продвижение проектов',
    'Работа со спонсорскими интеграциями',
    'Медиа-поддержка мероприятий',
    'Создание программы мероприятий',
    'Работа с финансами',
    'Работа с техникой'
  ];

  let isSubmitting = false;
  let submitMessage = '';
  let fieldErrors: Record<string, string> = {};

  // Функция добавления тега
  const addTag = (tag: string) => {
    if (!interests.includes(tag)) {
      interests = [...interests, tag];
    }
  };

  // Функция удаления тега
  const removeTag = (tag: string) => {
    interests = interests.filter(t => t !== tag);
  };

  // Функция валидации полей
  const validateFields = (): boolean => {
    fieldErrors = {};
    
    if (!name.trim()) fieldErrors.name = 'Введите ФИО';
    if (!telegram.trim()) fieldErrors.telegram = 'Введите Telegram';
    if (!education.trim()) fieldErrors.education = 'Введите образовательную программу';
    if (interests.length === 0) fieldErrors.interests = 'Выберите хотя бы одно направление';
    
    return Object.keys(fieldErrors).length === 0;
  };

  const handleSubmit = async (e: Event) => {
    e.preventDefault();
    isSubmitting = true;
    submitMessage = '';

    // Валидация полей
    if (!validateFields()) {
      submitMessage = 'Пожалуйста, исправьте ошибки в форме';
      isSubmitting = false;
      return;
    }

    try {
      // Отправка на Google Apps Script
      const response = await fetch('https://script.google.com/macros/s/AKfycbwFhoFtqLELORcfrW2Y4KPAvisrND_auW-uYuXmXOs-8b_wx-r8zjfwomiM662tkwQ9/exec', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          name: name.trim(),
          telegram: telegram.trim(),
          education: education.trim(),
          interests: interests.join(', '),
          timestamp: new Date().toISOString()
        })
      });

      if (response.ok) {
        const result = await response.json();
        
        if (result.success) {
          submitMessage = 'Форма успешно отправлена!';
          // Очищаем форму
          name = '';
          telegram = '';
          education = '';
          interests = [];
        } else {
          submitMessage = 'Ошибка при отправке: ' + (result.error || 'Неизвестная ошибка');
        }
      } else {
        submitMessage = 'Ошибка сети: ' + response.status;
      }
    } catch (error) {
      const errorMessage = error instanceof Error ? error.message : 'Неизвестная ошибка';
      submitMessage = 'Ошибка сети: ' + errorMessage;
    } finally {
      isSubmitting = false;
    }
  };
</script>

<style>
  /* Фоновое изображение */
  .background-image {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
    background-color: #FFFFFE;
    background-image: url('/src/lib/assets/finish.svg');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
  }


  :global(main) {
    position: relative;
    min-height: 100vh;
  }

  .container {
    max-width: 1039px;
    margin: 0 auto;
    padding: 4rem 2rem;
    display: flex;
    flex-direction: column;
    gap: 52px;
    position: relative;
    z-index: 1;
  }

  .info-block {
    background: linear-gradient(45deg, var(--secondary-yellow) 0%, #FDE9A0 50%, #FBD652 100%);
    padding: 30px 39px 35px 39px;
    border-radius: 20px;
    color: var(--primary-purple);
    position: relative;
    overflow: hidden;
  }

  .info-block::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }



  .info-block h2 {
    font-size: 40px;
    font-family: var(--font-raleway);
    font-weight: 600;
  }

  .info-block ul {
    list-style: disc;
    padding-left: 1.5rem;
    margin: 0;
  }

  .info-block li {
    font-size: 28px;
    font-family: var(--font-raleway);
  }

  /* Адаптивность для больших экранов */
  @media (min-width: 1200px) {
    .info-block {
      padding: 35px 45px 40px 45px;
      border-radius: 24px;
    }
    
    .info-block h2 {
      font-size: 44px;
    }
    
    .info-block li {
      font-size: 32px;
    }
  }

  /* Адаптивность для средних экранов */
  @media (max-width: 1199px) and (min-width: 768px) {
    .container {
      gap: 30px;
    }

    .info-block {
      padding: 32px 42px 37px 42px;
      border-radius: 22px;
    }
    
    .info-block h2 {
      font-size: 38px;
    }
    
    .info-block li {
      font-size: 26px;
    }
  }

  /* Адаптивность для планшетов */
  @media (max-width: 767px) and (min-width: 481px) {
    .info-block {
      padding: 28px 35px 32px 35px;
      border-radius: 18px;
    }
    
    .info-block h2 {
      font-size: 32px;
    }
    
    .info-block li {
      font-size: 22px;
    }
  }

  /* Адаптивность для мобильных устройств */
  @media (max-width: 480px) {
    .registration-section {
      padding: 20px 15px;
    }

    .container {
      gap: 16px;
    }

    .info-block {
      padding: 20px 25px 24px 25px;
      border-radius: 16px;
    }
    
    .info-block h2 {
      font-size: 24px;
    }
    
    .info-block li {
      font-size: 16px;
    }
  }

  /* Адаптивность для очень маленьких экранов */
  @media (max-width: 360px) {
    .info-block {
      padding: 16px 20px 20px 20px;
      border-radius: 14px;
    }
    
    .info-block h2 {
      font-size: 20px;
    }
    
    .info-block li {
      font-size: 14px;
    }
  }

  /* Адаптивность для экстремально маленьких экранов */
  @media (max-width: 280px) {
    .info-block {
      padding: 12px 16px 16px 16px;
      border-radius: 12px;
    }
    
    .info-block h2 {
      font-size: 18px;
    }
    
    .info-block li {
      font-size: 12px;
    }
  }

  /* Адаптивность для мобильных устройств с шрифтом 9px */
  @media (max-width: 480px) {
    .info-block li {
      font-size: 9px;
      line-height: 1.4;
    }
    
    .info-block h2 {
      font-size: 18px;
      line-height: 1.3;
    }
  }

  .training-cards {
    display: flex;
    gap: 26px;
    justify-content: space-between;
    flex-wrap: nowrap;
    max-width: 1039px;
    width: 100%;
    --container-width: 100%;
  }

  .frame-image {
    flex: 1;
    width: calc(25% - 19.5px); /* 25% от контейнера минус отступы */
    height: 175px;
    object-fit: contain;
  }

  /* Адаптивность для разных экранов */
  @media (max-width: 1200px) {
    .training-cards {
      --container-width: 90%;
    }
    
    .frame-image {
      height: 160px;
    }
  }

  @media (max-width: 1024px) {
    .training-cards {
      gap: 16px;
      --container-width: 85%;
    }
    
    .frame-image {
      width: calc(25% - 12px);
      height: 145px;
    }
  }

  @media (max-width: 900px) {
    .training-cards {
      --container-width: 80%;
    }
    
    .frame-image {
      height: 130px;
    }
  }

  @media (max-width: 768px) {
    .training-cards {
      gap: 12px;
      flex-wrap: nowrap;
      justify-content: space-between;
      --container-width: 75%;
    }
    
    .frame-image {
      width: calc(25% - 9px);
      height: 120px;
    }
  }

  @media (max-width: 600px) {
    .training-cards {
      gap: 10px;
      --container-width: 70%;
    }
    
    .frame-image {
      width: calc(25% - 7.5px);
      height: 110px;
    }
  }

  @media (max-width: 480px) {
    .training-cards {
      gap: 8px;
      flex-direction: row;
      flex-wrap: nowrap;
      --container-width: 65%;
    }
    
    .frame-image {
      width: calc(25% - 6px);
      height: 100px;
    }
  }

  @media (max-width: 360px) {
    .training-cards {
      gap: 6px;
      --container-width: 60%;
    }
    
    .frame-image {
      width: calc(25% - 4.5px);
      height: 90px;
    }
  }

  .registration-section {
    gap: 18px;
    padding: 2rem;
  }

  .registration-title {
    color: var(--primary-purple);
    font-size: 2rem;
    font-weight: 700;
    text-align: center;
  }

  .form-section {
    gap: 18px;
  }

  .form-label {
    display: block;
    margin-bottom: 0.75rem;
    font-weight: 600;
    color: var(--primary-purple);
    font-size: 24px;
  }

  .form-input {
    display: flex;
    align-items: center;
    width: 100%;
    padding: 12px 25px;
    background: var(--input-bg);
    border-radius: 16px;
    font-size: 18px;
    color: #857E7E;
    box-sizing: border-box;
  }

  .form-input:focus {
    outline: none;
    border-color: var(--primary-purple);
    transform: translateY(-2px);
  }

  .form-input.error {
    border-color: #dc3545;
  }

  .form-input::placeholder {
    color: #857E7E;
    font-style: normal;
    font-family: var(--font-raleway);
    font-size: 18px;
  }

  .submit-section {
    text-align: center;
    margin-top: 3rem;
  }

  .submit-button {
    background: linear-gradient(135deg, var(--primary-purple) 0%, #5a2a7a 100%);
    color: white;
    padding: 1.25rem 4rem;
    border-radius: 16px;
    font-weight: 600;
    cursor: pointer;
    border: none;
    position: relative;
    overflow: hidden;
  }

  .submit-button::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
    transition: left 0.5s;
  }

  .submit-button:hover::before {
    left: 100%;
  }

  .submit-button:hover:not(:disabled) {
    transform: translateY(-2px);
  }

  .submit-button:disabled {
    opacity: 0.6;
    cursor: not-allowed;
    transform: none;
  }

  /* Адаптивность для больших экранов */
  @media (min-width: 1200px) {
    .registration-section {
      padding: 3rem;
      gap: 24px;
    }
    
    .registration-title {
      font-size: 1.75rem;
    }
    
    .form-section {
      gap: 24px;
    }
    
    .form-label {
      font-size: 28px;
      margin-bottom: 1rem;
    }
    
    .form-input {
      padding: 1.5rem 2rem;
      font-size: 22px;
      border-radius: 20px;
    }
    
    .form-input::placeholder {
      font-size: 22px;
    }
    
    .selected-tags {
      padding: 16px 24px;
      border-radius: 20px;
      min-height: 80px;
    }
    
    .available-tags {
      padding: 1.5rem 2rem;
      border-radius: 20px;
      gap: 12px;
    }
    
    .tag {
      padding: 12px 16px;
      font-size: 22px;
      border-radius: 24px;
    }
    
    .placeholder-text {
      font-size: 22px;
    }
    
    .submit-button {
      padding: 1.5rem 5rem;
      font-size: 35px;
      border-radius: 20px;
    }
  }

  /* Адаптивность для средних экранов */
  @media (max-width: 1199px) and (min-width: 768px) {
    .registration-section {
      padding: 2.5rem;
      gap: 20px;
    }
    
    .registration-title {
      font-size: 2.25rem;
    }
    
    .form-section {
      gap: 20px;
    }
    
    .form-label {
      font-size: 26px;
      margin-bottom: 0.875rem;
    }
    
    .form-input {
      padding: 1.25rem 1.75rem;
      font-size: 20px;
      border-radius: 18px;
    }
    
    .form-input::placeholder {
      font-size: 18px;
    }
    
    .selected-tags {
      padding: 16px 24px;
      border-radius: 18px;
      min-height: 70px;
    }
    
    .available-tags {
      padding: 16px 24px;
      border-radius: 18px;
      gap: 10px;
    }
    
    .tag {
      padding: 10px 16px;
      font-size: 18px;
      border-radius: 22px;
    }
    
    .placeholder-text {
      font-size: 18px;
    }
    
    .submit-button {
      padding: 20px 40px;
      font-size: 24px;
      border-radius: 18px;
    }
    .privacy-text {
      font-size: 18px;
    }
    
    .privacy-link {
      font-size: 18px;
    }
  }

  /* Адаптивность для планшетов */
  @media (max-width: 767px) and (min-width: 481px) {
    .registration-section {
      padding: 2rem 1.5rem;
      gap: 18px;
    }
    
    .registration-title {
      font-size: 1.75rem;
    }
    
    .form-section {
      gap: 18px;
    }
    
    .form-label {
      font-size: 24px;
      margin-bottom: 0.75rem;
    }
    
    .form-input {
      padding: 1rem 1.5rem;
      font-size: 18px;
      border-radius: 16px;
    }
    
    .form-input::placeholder {
      font-size: 18px;
    }
    
    .selected-tags {
      padding: 10px 15px;
      border-radius: 16px;
      min-height: 60px;
    }
    
    .available-tags {
      padding: 10px 15px;
      border-radius: 16px;
      gap: 8px;
    }
    
    .tag {
      padding: 8px 16px;
      font-size: 18px;
      border-radius: 20px;
    }
    
    .placeholder-text {
      font-size: 18px;
    }
    
    .submit-button {
      padding: 10px 35px;
      font-size: 18px;
      border-radius: 16px;
    }
    .privacy-text {
      font-size: 14px;
    }
    
    .privacy-link {
      font-size: 14px;
    }
  }

  /* Адаптивность для мобильных устройств */
  @media (max-width: 480px) {
    .registration-section {
      padding: 1.5rem 1rem;
      gap: 16px;
    }
    
    .registration-title {
      font-size: 1.25rem;
    }
    
    .form-section {
      gap: 14px;
    }
    
    .form-label {
      font-size: 16px;
      margin-bottom: 0.5rem;
    }
    
    .form-input {
      padding: 0.75rem 1rem;
      font-size: 12px;
      border-radius: 12px;
    }
    
    .form-input::placeholder {
      font-size: 12px;
    }
    
    .selected-tags {
      padding: 0.75rem 1rem;
      border-radius: 12px;
      min-height: 50px;
    }
    
    .available-tags {
      padding: 0.75rem 1rem;
      border-radius: 12px;
      gap: 6px;
    }
    
    .tag {
      padding: 6px 10px;
      font-size: 12px;
      border-radius: 16px;
    }
    
    .placeholder-text {
      font-size: 12px;
    }
    
    .submit-button {
      padding: 4px 16px;
      font-size: 10px;
      border-radius: 12px;
    }
    .privacy-text {
      font-size: 12px;
    }
    
    .privacy-link {
      font-size: 12px;
    }
  }

  /* Адаптивность для очень маленьких экранов */
  @media (max-width: 360px) {
    .registration-section {
      padding: 1rem 0.75rem;
      gap: 12px;
    }
    
    .registration-title h2{
      font-size: 1rem;
    }
    
    .form-section {
      gap: 12px;
    }
    
    .form-label {
    font-size: 14px;
      margin-bottom: 0.5rem;
    }
    
    .form-input {
      padding: 0.625rem 0.875rem;
      font-size: 10px;
      border-radius: 10px;
    }
    
    .form-input::placeholder {
      font-size: 10px;
    }
    
    .selected-tags {
      padding: 0.625rem 0.875rem;
      border-radius: 10px;
      min-height: 45px;
    }
    
    .available-tags {
      padding: 0.625rem 0.875rem;
      border-radius: 10px;
      gap: 5px;
    }
    
    .tag {
      padding: 5px 8px;
      font-size: 10px;
      border-radius: 14px;
    }
    
    .placeholder-text {
      font-size: 10px;
    }
    
    .submit-button {
      padding: 3px 15px;
      font-size: 14px;
      border-radius: 10px;
    }
    .privacy-text {
      font-size: 10px;
    }
    
    .privacy-link {
      font-size: 10px;
    }
  }

  /* Адаптивность для экстремально маленьких экранов */
  @media (max-width: 280px) {
    .registration-section {
      padding: 0.75rem 0.5rem;
      gap: 10px;
    }
    
    .registration-title {
      font-size: 1rem;
    }
    
    .form-section {
      gap: 10px;
    }
    
    .form-label {
      font-size: 14px;
      margin-bottom: 0.375rem;
    }
    
    .form-input {
      padding: 0.5rem 0.75rem;
      font-size: 10px;
      border-radius: 8px;
    }
    
    .form-input::placeholder {
      font-size: 10px;
    }
    
    .selected-tags {
      padding: 0.5rem 0.75rem;
      border-radius: 8px;
      min-height: 40px;
    }
    
    .available-tags {
      padding: 0.5rem 0.75rem;
      border-radius: 8px;
      gap: 4px;
    }
    
    .tag {
      padding: 4px 6px;
      font-size: 8px;
      border-radius: 12px;
    }
    
    .placeholder-text {
      font-size: 8px;
    }
    
    .submit-button {
      padding: 0.5rem 1.5rem;
      font-size: 0.75rem;
      border-radius: 8px;
    }
  }

  .privacy-text {
    color: var(--primary-purple);
    margin-top: 1rem;
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
  }

  .error-message {
    color: #dc3545;
    font-size: 0.875rem;
    margin-top: 0.5rem;
    display: block;
  }

  /* Стили для тегов */
  .selected-tags {
    min-height: 60px;
    background: rgba(247, 243, 237, 0.9);
    border-radius: 16px;
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    align-items: center;
    transition: all 0.3s ease;
    backdrop-filter: blur(10px);
  }

  .selected-tags.error {
    border-color: #dc3545;
    box-shadow: 0 0 0 3px rgba(220, 53, 69, 0.1);
  }

  .selected-tags:focus-within {
    outline: none;
    border-color: var(--primary-purple);
    box-shadow: 0 0 0 3px rgba(106, 45, 135, 0.1);
  }

  .placeholder-text {
    color: #857E7E;
    font-style: normal;
    font-family: var(--font-raleway);
  }

  .available-tags {
    margin-top: 12px;
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    color: var(--primary-purple);
    background: rgba(247, 243, 237, 0.9);
    border-radius: 16px;
    padding: 12px;
    backdrop-filter: blur(10px);
  }

  .tag {
    display: inline-flex;
    align-items: center;
    padding: 8px 12px;
    border-radius: 20px;
    font-family: var(--font-raleway);
    font-weight: 500;
    cursor: pointer;
    border: none;
    font-family: var(--font-raleway);
  }

  .selected-tag {
    background: var(--primary-purple);
    color: white;
    position: relative;
  }

  .available-tag {
    background: #e8d5ff;
    color: var(--primary-purple);
  }

  .available-tag:hover {
    background: #d4b8ff;
    transform: translateY(-1px);
  }

  .remove-tag {
    background: none;
    border: none;
    color: white;
    font-size: 16px;
    font-weight: bold;
    margin-left: 6px;
    cursor: pointer;
    padding: 0;
    width: 16px;
    height: 16px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    transition: background-color 0.3s ease;
  }

  .remove-tag:hover {
    background: rgba(255, 255, 255, 0.2);
  }

  @media (max-width: 768px) {
    .background-image {
      background-size: cover;
      background-position: center;
    }
    
    .registration-section {
      padding: 2rem 1.5rem;
    }
    
    .registration-title {
      font-size: 2rem;
    }
  }
</style>

<main>
  <div class="background-image"></div>
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
      <img src={FrameYel} alt="Frame Yellow" class="frame-image" />
      <img src={FrameLightPurp} alt="Frame Light Purple" class="frame-image" />
      <img src={FramePurp} alt="Frame Purple" class="frame-image" />
      <img src={FrameWhite} alt="Frame White" class="frame-image" />
    </div>

    <div id="registration" class="registration-section">
      <h2 class="registration-title">Регистрация</h2>

      <form on:submit={handleSubmit}>
        <div class="form-section">
          <label for="name" class="form-label">Твое ФИО</label>
          <input 
            id="name" 
            type="text"
            bind:value={name} 
            placeholder="ФИО"
            class="form-input {fieldErrors.name ? 'error' : ''}"
            required
          >
          {#if fieldErrors.name}
            <span class="error-message">{fieldErrors.name}</span>
          {/if}
        </div>

        <div class="form-section">
          <label for="telegram" class="form-label">Твой Telegram</label>
          <input 
            id="telegram" 
            type="text"
            bind:value={telegram} 
            placeholder="@"
            class="form-input {fieldErrors.telegram ? 'error' : ''}"
            required
          >
          {#if fieldErrors.telegram}
            <span class="error-message">{fieldErrors.telegram}</span>
          {/if}
        </div>

        <div class="form-section">
          <label for="education" class="form-label">Твоя образовательная программа и учебная группа</label>
          <input 
            id="education" 
            type="text"
            bind:value={education} 
            placeholder="Например, «Медиакоммуникации, БМД251»"
            class="form-input {fieldErrors.education ? 'error' : ''}"
            required
          >
          {#if fieldErrors.education}
            <span class="error-message">{fieldErrors.education}</span>
          {/if}
        </div>

        <div class="form-section">
          <label for="interests" class="form-label">Расскажи, какие направления в ивенте тебя больше всего интересуют?</label>
          
          <!-- Выбранные теги -->
          <div class="selected-tags {fieldErrors.interests ? 'error' : ''}">
            {#each interests as tag}
              <span class="tag selected-tag">
                {tag}
                <button type="button" class="remove-tag" on:click={() => removeTag(tag)}>×</button>
              </span>
            {/each}
            {#if interests.length === 0}
              <span class="placeholder-text">Выберите направления...</span>
            {/if}
          </div>

          <!-- Доступные теги -->
          <div class="available-tags">
            {#each availableTags as tag}
              {#if !interests.includes(tag)}
                <button 
                  type="button" 
                  class="tag available-tag" 
                  on:click={() => addTag(tag)}
                >
                  {tag}
                </button>
              {/if}
            {/each}
          </div>

          {#if fieldErrors.interests}
            <span class="error-message">{fieldErrors.interests}</span>
          {/if}
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
          
          <p class="privacy-text">
            Нажимая кнопку ты соглашаешься с <a href="/privacy" class="privacy-link">политикой конфиденциальности</a>
          </p>
        </div>
      </form>
    </div>
  </div>
</main>
