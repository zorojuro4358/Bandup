# Руководство по подключению данных

## 📊 Где подключать статистику

### 1. Главная страница (HomePage.tsx)
**Файл:** `src/pages/HomePage.tsx`
**Секция:** "Statistics Section"

```tsx
// Замените эти значения на реальные данные из API
<div className="text-3xl font-bold text-primary mb-2">0</div> // Активных студентов
<div className="text-3xl font-bold text-primary mb-2">0%</div> // Успешных результатов
<div className="text-3xl font-bold text-primary mb-2">0★</div> // Рейтинг пользователей
```

### 2. Dashboard статистика (Dashboard.tsx)
**Файл:** `src/pages/Dashboard.tsx`
**Секция:** "Quick Stats"

```tsx
// Замените на реальные данные пользователя
<p className="text-2xl font-bold">0 уроков</p> // Сегодня изучено
<p className="text-2xl font-bold">0 часов</p> // Всего времени
<p className="text-2xl font-bold">0%</p> // Прогресс
<p className="text-2xl font-bold">0</p> // Достижения
```

### 3. Профиль пользователя (ProfilePage.tsx)
**Файл:** `src/pages/ProfilePage.tsx`
**Секции:** "Stats Grid" и "Progress Section"

```tsx
// Общий прогресс
<div className="text-3xl font-bold text-primary">0%</div>

// Статистика
<span className="text-2xl font-bold text-blue-500">0</span> // Завершенных уроков
<span className="text-2xl font-bold text-green-500">0</span> // Часов обучения
<span className="text-2xl font-bold text-yellow-500">0</span> // Достижения

// Прогресс по предметам
const [progress] = useState<Progress[]>([
  { subject: "Writing", completed: 0, total: 12, lastActivity: "Нет активности" },
  // ... обновите на реальные данные
]);
```

## 💬 Где подключать отзывы

### Главная страница (HomePage.tsx)
**Файл:** `src/pages/HomePage.tsx`
**Секция:** "Testimonials Section"

```tsx
// Замените placeholder на реальные отзывы
<div className="text-center py-12">
  <div className="text-6xl mb-4">💬</div>
  <h3 className="text-xl font-semibold text-foreground mb-2">
    Отзывы появятся скоро
  </h3>
  <p className="text-muted-foreground max-w-md mx-auto">
    Мы собираем отзывы от наших студентов. Скоро здесь появятся реальные истории успеха!
  </p>
</div>

// Структура отзыва:
<div className="bg-accent rounded-xl p-6">
  <div className="flex items-center mb-4">
    <div className="flex text-yellow-400">
      {[...Array(5)].map((_, i) => <Star key={i} size={16} fill="currentColor" />)}
    </div>
  </div>
  <p className="text-muted-foreground mb-4">
    "Текст отзыва"
  </p>
  <div className="flex items-center">
    <div className="w-10 h-10 bg-primary rounded-full flex items-center justify-center text-white font-semibold mr-3">
      ИМ
    </div>
    <div>
      <p className="font-medium text-foreground">Имя Фамилия</p>
      <p className="text-sm text-muted-foreground">Должность/Статус</p>
    </div>
  </div>
</div>
```

## 🤖 Где подключать данные об ИИ-ассистентах

### Страница информации об ИИ (AIInfoPage.tsx)
**Файл:** `src/pages/AIInfoPage.tsx`
**Секции:** массивы `features`, `benefits`, `subjects`

```tsx
// Особенности ИИ-ассистентов
const features = [
  {
    icon: Brain,
    title: "Название особенности",
    description: "Описание особенности ИИ-ассистента"
  },
  // ... добавьте больше особенностей
];

// Преимущества ИИ-обучения
const benefits = [
  {
    icon: "🎯",
    title: "Название преимущества",
    description: "Описание преимущества"
  },
  // ... добавьте больше преимуществ
];

// Предметы для изучения
const subjects = [
  {
    name: "Название предмета",
    description: "Описание предмета",
    icon: "📚",
    features: ["Особенность 1", "Особенность 2"]
  },
  // ... добавьте больше предметов
];
```

## 🏆 Где подключать достижения

### Профиль пользователя (ProfilePage.tsx)
**Файл:** `src/pages/ProfilePage.tsx`
**Секция:** массив `achievements`

```tsx
const [achievements] = useState([
  { 
    id: 1, 
    title: "Название достижения", 
    description: "Описание", 
    icon: "🎯", 
    earned: false // true если достижение получено
  },
  // ... добавьте больше достижений
]);
```

## 🔧 Подключение к API

### 1. Создайте API клиент
```tsx
// src/lib/api.ts
const API_BASE_URL = 'https://your-api.com/api';

export const api = {
  // Получить статистику
  getStats: async () => {
    const response = await fetch(`${API_BASE_URL}/stats`);
    return response.json();
  },
  
  // Получить отзывы
  getTestimonials: async () => {
    const response = await fetch(`${API_BASE_URL}/testimonials`);
    return response.json();
  },
  
  // Получить информацию об ИИ
  getAIInfo: async () => {
    const response = await fetch(`${API_BASE_URL}/ai-info`);
    return response.json();
  },
  
  // Получить прогресс пользователя
  getUserProgress: async (userId: string) => {
    const response = await fetch(`${API_BASE_URL}/users/${userId}/progress`);
    return response.json();
  }
};
```

### 2. Используйте React Query для кеширования
```tsx
// В компонентах
import { useQuery } from '@tanstack/react-query';
import { api } from '../lib/api';

const { data: stats } = useQuery({
  queryKey: ['stats'],
  queryFn: api.getStats
});
```

## 📝 Примеры реальных данных

### Статистика
```json
{
  "activeStudents": 1250,
  "successRate": 95,
  "userRating": 4.8,
  "availability": "24/7"
}
```

### Отзыв
```json
{
  "id": 1,
  "text": "Отличная платформа! Очень помогла в изучении математики.",
  "rating": 5,
  "author": {
    "name": "Анна Петрова",
    "role": "Студентка",
    "avatar": "АП"
  },
  "date": "2024-01-15"
}
```

### Информация об ИИ
```json
{
  "features": [
    {
      "title": "Искусственный интеллект",
      "description": "Описание особенности ИИ",
      "icon": "Brain"
    }
  ],
  "benefits": [
    {
      "title": "Точные ответы",
      "description": "Описание преимущества",
      "icon": "🎯"
    }
  ],
  "subjects": [
    {
      "name": "Writing",
      "description": "Описание предмета",
      "icon": "✍️",
      "features": ["Грамматика", "Стиль"]
    }
  ]
}
```

## 🚀 Следующие шаги

1. **Создайте API** для получения данных
2. **Замените статические данные** на API вызовы
3. **Добавьте загрузочные состояния** для лучшего UX
4. **Реализуйте кеширование** с помощью React Query
5. **Добавьте обработку ошибок** для надежности

Все данные теперь обнулены и готовы к подключению реальных данных! 🎉 