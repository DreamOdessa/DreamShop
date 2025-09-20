# Dream E-commerce - Інструкції для деплою

## Швидкий старт для деплою

### 1. Налаштування Environment Variables

Переконайтеся що всі необхідні змінні середовища налаштовані:

```bash
# Обов'язкові
DATABASE_URL=postgresql://...
SESSION_SECRET=your-secret-key

# Email налаштування (Gmail SMTP)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password
FROM_EMAIL=your-email@gmail.com

# Google OAuth
GOOGLE_CLIENT_ID=your-client-id
GOOGLE_CLIENT_SECRET=your-client-secret

# Telegram Bot (для верифікації телефонів)
TWILIO_ACCOUNT_SID=optional
TWILIO_AUTH_TOKEN=optional
TWILIO_PHONE_NUMBER=optional

# Object Storage (автоматично налаштовується Replit)
DEFAULT_OBJECT_STORAGE_BUCKET_ID=...
PRIVATE_OBJECT_DIR=...
PUBLIC_OBJECT_SEARCH_PATHS=...
```

### 2. Запуск деплою

```bash
# Автоматичний deploy script
./scripts/deploy.sh

# Або вручну:
tsx migrate.ts          # Міграції БД
npm run build          # Збірка проекту  
npm start              # Запуск продакшн сервера
```

## Структура бази даних

Після успішної міграції в базі буде створено:

- **users** - користувачі з підтримкою Google OAuth та Telegram
- **categories** - категорії продуктів з перекладами (ua/ru/en) 
- **products** - товари з багатомовною підтримкою
- **orders** - замовлення користувачів
- **cart_items** - кошик покупок
- **product_likes** - уподобання користувачів
- **sessions** - сесії користувачів (PostgreSQL store)
- **telegram_verifications** - верифікація через Telegram bot

## Перевірка успішного деплою

1. Відкрийте додаток в браузері
2. Перевірте що відображаються категорії та продукти
3. Протестуйте реєстрацію/логін через Google OAuth
4. Перевірте роботу Telegram bot (@DREAM_zakbot) для верифікації

## Troubleshooting

### Проблема: База даних не підключається
- Перевірте DATABASE_URL
- Переконайтеся що база доступна з продакшн сервера

### Проблема: Google OAuth не працює  
- Перевірте GOOGLE_CLIENT_ID та GOOGLE_CLIENT_SECRET
- Додайте правильний callback URL в Google Console

### Проблема: Email не відправляються
- Перевірте SMTP налаштування
- Для Gmail потрібен App Password, не основний пароль

### Проблема: Telegram верифікація не працює
- Перевірте що @DREAM_zakbot доступний
- Bot token має бути правильно налаштований на сервері