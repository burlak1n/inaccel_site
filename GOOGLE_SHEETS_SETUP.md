# Настройка отправки формы в Google Sheets

## Шаг 1: Создание Google Apps Script

1. Перейдите на [script.google.com](https://script.google.com)
2. Создайте новый проект
3. Назовите проект "Form Handler" или любое другое название

## Шаг 2: Код для Google Apps Script

Замените содержимое файла `Code.gs` на следующий код:

```javascript
function doPost(e) {
  try {
    // Получаем данные из формы
    const data = JSON.parse(e.postData.contents);
    
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
      data.name,
      data.telegram,
      data.education,
      data.interests
    ]);
    
    // Возвращаем успешный ответ
    return ContentService
      .createTextOutput(JSON.stringify({ success: true }))
      .setMimeType(ContentService.MimeType.JSON);
      
  } catch (error) {
    // Возвращаем ошибку
    return ContentService
      .createTextOutput(JSON.stringify({ 
        success: false, 
        error: error.toString() 
      }))
      .setMimeType(ContentService.MimeType.JSON);
  }
}

function doGet(e) {
  return ContentService
    .createTextOutput('Form handler is working!')
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
Форма настроена на отправку данных на ваш Google Apps Script: `https://script.google.com/macros/s/AKfycbwFhoFtqLELORcfrW2Y4KPAvisrND_auW-uYuXmXOs-8b_wx-r8zjfwomiM662tkwQ9/exec`

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
