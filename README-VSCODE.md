# Запуск проекта в Visual Studio Code

Данный проект адаптирован для работы в Visual Studio Code с внешней базой данных PostgreSQL и без зависимости от сервисов Replit.

## Требования

- Node.js 18+ и npm
- PostgreSQL база данных
- Visual Studio Code (рекомендуется)

## Установка и настройка

### 1. Клонирование и установка зависимостей

```bash
git clone <repository-url>
cd <project-name>
npm install
```

### 2. Настройка базы данных

Создайте PostgreSQL базу данных и настройте переменные окружения:

```bash
# Скопируйте .env.example в .env
cp .env.example .env
```

Отредактируйте `.env` файл и укажите:

```env
# Обязательные переменные
DATABASE_URL=postgresql://username:password@localhost:5432/database_name
SESSION_SECRET=your-very-long-and-secure-session-secret-here

# Опциональные (для Google Auth)
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
```

### 3. Миграция базы данных

```bash
npm run db:push
```

### 4. Запуск проекта

Для разработки:
```bash
npm run dev
```

Приложение будет доступно по адресу: `http://localhost:3000`

Для production:
```bash
npm run build
npm start
```

## Аутентификация

Проект поддерживает следующие виды аутентификации:

1. **Локальная аутентификация** - регистрация/вход по телефону и паролю
2. **Google OAuth** - вход через Google аккаунт (требует настройки GOOGLE_CLIENT_ID)

Replit Auth был удален для обеспечения независимости от платформы.

## Конфигурация портов

- **Для локальной разработки**: используйте PORT=3000 в .env
- **Для совместимости с Replit**: используйте PORT=5000 в .env

## Дополнительные настройки

### Email уведомления (опционально)
```env
EMAIL_HOST=smtp.ethereal.email
EMAIL_PORT=587
EMAIL_USER=your-email-user
EMAIL_PASS=your-email-password
```

### Telegram Bot (опционально)
```env
TELEGRAM_BOT_TOKEN=your-telegram-bot-token
TELEGRAM_CHAT_ID=your-telegram-chat-id
```

### Object Storage (опционально)
```env
GOOGLE_CLOUD_PROJECT_ID=your-project-id
GOOGLE_CLOUD_BUCKET_NAME=your-bucket-name
GOOGLE_CLOUD_KEY_FILE=path/to/service-account-key.json
```

## Структура проекта

- `client/` - React frontend
- `server/` - Express.js backend  
- `shared/` - Общие типы и схемы
- `migrations/` - Drizzle ORM миграции базы данных

## Разработка

### Команды

- `npm run dev` - запуск в режиме разработки
- `npm run build` - сборка для production
- `npm start` - запуск production версии  
- `npm run db:push` - применение миграций базы данных
- `npm run check` - проверка TypeScript

### VS Code расширения (рекомендуется)

- **ES7+ React/Redux/React-Native snippets**
- **TypeScript Importer**
- **Prettier - Code formatter**
- **ESLint**
- **Auto Rename Tag**

## Деплой

Для деплоя на внешний сервер:

1. Настройте производственную базу данных
2. Установите переменные окружения
3. Выполните сборку: `npm run build`  
4. Запустите: `npm start`

Убедитесь что:
- `NODE_ENV=production`
- `DATABASE_URL` указывает на production базу
- `SESSION_SECRET` является случайной строкой
- Google OAuth настроен с правильными callback URL