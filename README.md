# Оглавление
1. [Задание 1](#task_1)
2. [Задание 2](#task_2)

# Задание 1 <a name="task_1"></a>

Для решения необходимо провести анализ приложения и определить бизнес-функции приложения, руководствуясь принципами Domain-Driven-Design.

## Анализ приложения

Проект Mesto - фронтенд-приложение на React с простым функционалом загрузки фотографий, их отображения и возможностью реакций от зарегистрированных пользователей, таким образом мы имеем следующи фукнции приложения:
* профиль пользователя
* галерея фотографий
* авторизация и аутентификация

Так же стоит отдельно отметить, что выделена функция авторизации и аутентификации, чтобы была возможность развивать профиль как самостоятельную функцию.

## Метод реализации

В качестве метода реализации будет выбрана run time с клиентской компновкой, так у нас будет возможность разрабатывать микрофронты отдельно, а так же осуществлять динамическую lazy-загрузку компонентов.

## Инструмент реализации

В качестве инструмента выбран `Webpack Module Federation`, так как есть опыт работы с данным фреймворком и все части у нас написаны на React. `Single SPA` так же отлично подойдет для решения задачи, в случае наличия опыта у команды и наличия компонентов, реализованных не на React.

## Приложение (Уровень 2)

Структура приложения в папке [microfrontend](frontend/microfrontend)

```text
/auth
/gallery
/profile
/src
.babelrc
.gitignore
package.json
webpack.config.js
```

### auth
Модуль авторизации и аутентификации пользователя. Отображает страницы регистрации и авторизации, а так же показывает всплывающее окно об успешной авторизации на сайте. Его структура:
```text
/auth 
├── /src    
│    ├── /blocks     
│    │    └── /auth-form            # стили формы авторизации
│    ├── /components
│    │    ├── InfoTooltip.js        # компонент всплывающего окна об успешной регистрации
│    │    ├── Login.js              # компонент формы авторизации
│    │    ├── ProtectedRoute.js     # компонент роута проверки авторизации
│    │    └── Register.js           # компонент формы регистрации
│    │── /utils 
│    │    └── auth.js               # утилитарный класс для работы с апи авторизации
│    └── index.js                   # точка входа для root приложения
├── package.json                    # описание приложения и его зависимостей
└── webpack.config.js               # настройка webpack module federation
```

### gallery
Модуль работы с фотографиями - позволяет загружать фотографии, удалять их, а так же ставить и учитывать лайки под ними.
```text
/gallery 
├── /src    
│    ├── /blocks     
│    │    ├── /card                 # стили карточек фотографий и лайков
│    │    ├── /places               # стили мест
│    │    └── /popup                # стили всплывающих окон
│    ├── /components
│    │    ├── AddPlacePopup.js      # компонент добавления места с указанием фото
│    │    ├── Card.js               # компонент отображения фото и лайков
│    │    ├── ImagePopup.js         # компонент просмотра отдельного фото 
│    │    ├── Main.js               # компонент отображения плитки с фото
│    │    └── PopupWithForm.js      # компонент всплывающего окна (используется в AddPlacePopup)
│    │── /utils 
│    │    └── api.js                # утилитарный класс для работы с апи фото
│    └── index.js                   # точка входа для root приложения
├── package.json                    # описание приложения и его зависимостей
└── webpack.config.js               # настройка webpack module federation
```

### profile
Модуль отвечает за профиль пользователя.
```text
/gallery 
├── /src    
│    ├── /blocks     
│    │    ├── /popup                # стили всплывающих окон
│    │    └── /profile              # стили профиля
│    ├── /components
│    │    ├── EditAvatarPopup.js    # компонент формы редактирования аватра
│    │    ├── EditProfilePopup.js   # компонент формы редактирования профиля
│    │    └── PopupWithForm.js      # компонент всплывающего окна 
│    │── /utils 
│    │    └── api.js                # утилитарный класс для работы с апи фото
│    └── index.js                   # точка входа для root приложения
├── package.json                    # описание приложения и его зависимостей
└── webpack.config.js               # настройка webpack module federation
```

### root (каталог src)
Корневой модуль хост-приложения, который объединяет все микрофронты в один.
```text
/ 
├── /src    
│    ├── /blocks     
│    │    ├── /content              # основной стиль
│    │    ├── /footer               # стиль подвала страницы
│    │    ├── /header               # стиль шапки страницы
│    │    └── /popup                # стили всплывающих окон
│    ├── /components
│    │    ├── App.js                # компонент основного приложения, собирающего все вместе
│    │    ├── Footer.js             # компонент подвала страницы
│    │    └── Header.js             # компонент шапки страницы
│    └── index.js                   # точка входа при запуске и сборки основного фронта
├── package.json                    # описание хост приложения и его зависимостей
└── webpack.config.js               # настройка сборки всего фронта
```

Уровень 3 (запуск готового кода) не выполнялся

# Задание 2 <a name="task_2"></a>

Итоговая диаграмма в файле [arch_template_task2.drawio](arch_template_task2.drawio), вкладка Solution