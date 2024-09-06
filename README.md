## Уровень 1. Проектирование

Задача:
 - Выберите фреймворк для создания микрофронтендов и опишите решение в удобном вам виде.

Проект Mesto представляет собой одностраничное приложение со следующей функциональностью:
 - Загрузка и удаление фотографий
 - Сбор и учёт лайков под фото
 - Создание профиля и его редактирование

Для разбивки на микрофронты буду выбирать между двумя популярными фреймворками - Webpack Module Federation и Single SPA.
Single-SPA больше подходит, когда фронт пишется на разных фреймворках или библиотеках. Наш фронтенд написано на React, поэтому мы можем использовать общие зависимости. Так же можем использовать общий код утилиты api.js.
Поэтому, решением будет выбрать Webpack Module Federation, который все это позволяет.

## Уровень 2. Планирование изменений

Для проектирования микрофронтендов применю подход "DDD" и стратегию "вертикальная нарезка", разделив приложение на предметные области.

Выделю 3 домена:
 - Регистрация/аутентификация
 - Профиль пользователя
 - Каталог изображений

```
/auth-microfrontend
  /src
    /components
	    Login.js               // Компонент входа пользователя
	    Register.js            // Компонент регистрации пользователя
    /styles                    // Стили
	    login.css
	    /auth-form
    /utils
	    auth.js                // Утилиты для аутентификации
/profile-microfrontend
	/components
		EditAvatarPopup.js     // Компонент редактирования аватара
		EditProfilePopup.js    // Компонент редактирования профиля
	/styles                    // Стили
		__add-button
		__description
		__edit-button
		__image
		__info
		__title
		profile.css
/cards-microfrontend
	/components
		AddPlacePopup.js       // Компонент добавления карточки
		Card.js                // Компонент карточки
	/styles                    // Стили
		__delete-button
		__description
		__image
		__like-button
		__like-count
		__title
		card.css
```