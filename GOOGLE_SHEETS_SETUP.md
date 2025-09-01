# Настройка отправки формы в Google Sheets

## Шаг 1: Создание Google Apps Script

1. Перейдите на [script.google.com](https://script.google.com)
2. Создайте новый проект
3. Назовите проект "Form Handler" или любое другое название

## Шаг 2: Код для Google Apps Script

Замените содержимое файла `Code.gs` на следующий код:

```javascript
function doGet(e) {
  // Проверяем, что параметр e существует
  if (!e) {
    return ContentService
      .createTextOutput('Form handler is working!')
      .setMimeType(ContentService.MimeType.TEXT);
  }
  
  // Получаем параметры из GET запроса
  const params = e.parameter || {};
  
  try {
    // Проверяем, есть ли данные для записи
    if (params.name && params.telegram && params.education && params.interests) {
      // Получаем активную таблицу
      const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
      
      // Добавляем заголовки, если их нет
      if (sheet.getLastRow() === 0) {
        sheet.appendRow([
          'Дата и время',
          'ФИО',
          'Telegram',
          'Образовательная программа',
          'Интересы'
        ]);
      }
      
      // Добавляем новую строку с данными
      sheet.appendRow([
        new Date().toLocaleString('ru-RU'),
        params.name,
        params.telegram,
        params.education,
        params.interests
      ]);
      
      // Возвращаем JSONP ответ
      const callback = params.callback || 'callback';
      const response = { success: true, message: 'Данные успешно сохранены' };
      
      return ContentService
        .createTextOutput(`${callback}(${JSON.stringify(response)})`)
        .setMimeType(ContentService.MimeType.JAVASCRIPT);
        
    } else {
      // Если нет данных, возвращаем приветственное сообщение
      return ContentService
        .createTextOutput('Form handler is working!')
        .setMimeType(ContentService.MimeType.TEXT);
    }
    
  } catch (error) {
    // Возвращаем ошибку в JSONP формате
    const callback = params.callback || 'callback';
    const response = { success: false, error: error.toString() };
    
    return ContentService
      .createTextOutput(`${callback}(${JSON.stringify(response)})`)
      .setMimeType(ContentService.MimeType.JAVASCRIPT);
  }
}

function doPost(e) {
  // Обработка POST запросов (если понадобится в будущем)
  return doGet(e);
}

function doOptions(e) {
  // Обработка preflight OPTIONS запроса
  return ContentService
    .createTextOutput('')
    .setMimeType(ContentService.MimeType.TEXT);
}
```

## Шаг 3: Настройка веб-приложения

1. В Google Apps Script нажмите "Deploy" → "New deployment"
2. Выберите тип "Web app"
3. Настройте:
   - **Execute as**: Me (ваш аккаунт)
   - **Who has access**: Anyone
4. Нажмите "Deploy"
5. Скопируйте URL веб-приложения

## Шаг 4: Обновление кода формы

✅ **URL уже настроен!** 
Форма настроена на отправку данных на ваш Google Apps Script: `https://script.google.com/macros/s/AKfycbx8x5IFc2M_F0uJtBeAZ-SVAWO79VWKAAbBc2HjCcl2qWY4Sx5kE9e2_qWOPfKlhRUD/exec`

## Шаг 5: Создание Google Sheets

1. Создайте новую Google таблицу
2. Назовите её "Регистрации INACCEL" или любое другое название
3. Убедитесь, что она открыта (активна) при первом тестировании

## Структура данных в таблице

Таблица будет автоматически заполняться следующими колонками:
- Дата и время
- ФИО
- Telegram
- Образовательная программа
- Интересы

## Тестирование

1. Отправьте тестовую форму
2. Проверьте, что данные появились в Google Sheets
3. Убедитесь, что заголовки создались автоматически

## Безопасность

- Веб-приложение доступно всем (кто знает URL)
- Данные сохраняются в вашей Google таблице
- Рекомендуется регулярно проверять логи в Google Apps Script

## Решение проблемы CORS

Google Apps Script автоматически обрабатывает CORS для веб-приложений. Если проблемы всё ещё возникают:

1. **Пересоздать deployment** после обновления кода
2. **Очистить кэш браузера**
3. **Проверить, что таблица открыта** в Google Sheets
4. **Убедиться, что скрипт выполняется от вашего имени**
5. **Использовать режим разработки** для тестирования
