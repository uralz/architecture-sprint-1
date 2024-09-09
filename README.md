# Задание 1

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

# Задание 2

## Описание решения

Фронтенд раздели на микрофронты
- Пользователи
   - аутентификация
   - регистрация
   - ЛК пользователей, администраторов, специалистов поддержки
- Заказы, товары и услуги
  - просмотр, поиск товаров и услуг
  - создание/изменение товаров и услуг
  - создание заказа
- Аукционы
  - создание/редактирование аукциона
  - обработка заявки на аукцион
  - просмотр и участие в аукционах
- Отчетность
  - получение/просмотр отчетов

Монолит разделил на компоненты:

- Пользователи (регистрация, аутентификация, управление профилем, ЛК(админы, поддержка, пользователи))
  - регистрация
  - аутентификация (JWT)
  - редактирование профиля
  - назначение ролей
- Сервис поддержки
  - регистрация заявок
  - обработка и обновление статуса заявок
- Товары и услуги
  - создание/изменение товаров и услуг
- Аукционы
  - создание/редактирование аукциона
  - обработка заявки на аукцион
  - проведение аукционов
- Управление заказами
  - создание/редактирование заказа
- Транзакции
  - проведение платежей через внешние платежные сервисы
- Сервис уведомлений
  - нотификация пользователей
- Отчетность
  - формирование отчетов

[Ссылка на диаграмму](https://viewer.diagrams.net/?tags=%7B%7D&lightbox=1&highlight=0000ff&edit=_blank&layers=1&nav=1&title=%D0%97%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5_2.drawio#R%3Cmxfile%3E%3Cdiagram%20name%3D%22%D0%A1%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D0%B0%20%E2%80%94%201%22%20id%3D%22j7TvY-V9f41IpxHdanwK%22%3E7X1Zc%2BM4lvWvccTMgxjYl0fbsrurpqom46vqqe6nDtmWnaqULY8k5zK%2F%2FiNFggJAkCIlLqAEOyLTokiKAi7OuffiLlf49vX739az98%2B%2Frp7myysEnr5f4ekVQkxIEP%2BXHPmRHsGMZkde1oun9Jh24PfF%2F83Tg1Ad%2FVg8zTfZsfTQdrVabhfv5sHH1dvb%2FHFrHJut16tv5mnPq%2BWTceB99jI3HiM58PvjbDkvnPbn4mn7OTsKmdy%2F8ff54uVz9tEC8fSN15k6Obvx5vPsafVNO4TvrvDterXapn%2B9fr%2BdL5PRM8flvuTd%2FMHW87dtnQte8ebHXzcPN%2Fez%2Bd3fJ%2F%2F47evtr3eT7C6b7Q%2F1hedP8ffPXq7W28%2Brl9XbbHm3P3qzXn28Pc2Tu4L41f6cX1ar9%2FggjA%2F%2BNd9uf2STOfvYruJDn7evy%2Bzd%2BffF9p%2FJ5RHNXv1Le2f6Pbvz7sUP9eJtu%2F6RXoSoep1flrzYX7d7pS7cbNerL%2FPb1XK13n1BfH8P4p%2F4neIAKgGbrV%2Fm2aHJz%2B%2F%2FXn%2F8%2B6e35a9L9LdftpMV%2F%2BckfoLdiclYaVdm4%2F63%2Bep1Hj9CfMJ6vpxtF19NWZplIvmSn5df%2Bmm1iJ8FgWz9IEJgBJjMf9IbZGuJcmDeMH3u7B66JFi3nUCIeSQxyH%2BweWMhzRtvVh%2Frx3nhxtfr9eyHdtp7csKm%2FOsknyuMT4KYoAOPyjCtvCT%2BI30O9UqbgP2h3VposC7SjwBfZ8uPbPKuEFvGMnHzvNo9337FsP%2F9WKk3JpudzF%2FHJ0Dx%2Fn0nZOr9%2BK%2BX3f%2BxWN7cX8WCK8Du73hIwO4l3L282%2F3Ld%2F%2BS3b%2FpadPs5OwSNnuNV9vN28PmPb35Mv2Q%2B%2FQBs8%2FKDj8tvtqH2vkeU%2B2RkfY3zv5GQH3d%2FK2b3Xe91b6lfnk6EunfVDv%2FPrlV9ugPa%2BMZ7rRL9HEF2m3VTbLbpuenQ65unvyBtUuoNgPpE96qW%2BXv6nNCfZkToD34rfaA%2BcPm3xuZo5WP4p06vhuS6q8RH3Z8E%2Fuog2R%2BmT3EyoJBDLPl4uUt%2FvsxRuR5DNc3X%2Bfr7SIm4%2BvsjdfF01PKQfN4NGYPu%2FslWJ5BT3xzenNFp%2FGRZXL7mJ2e5msN%2FDMYdYF%2FFT8mzzH%2F7lI4smcwON2gAAVkIJIIMAPKJiR9eSJLTDg0bosAN2%2Bxen7ezLcWaDaFSScRQu7ASWuu9%2BpCMsXfPi%2B289%2FfZ4%2FJu99ipdGUgHK2TmRPHX%2BaP88%2BllvnNJbNWPnMwJhTzAEkGUt922t8GNMoO%2FpZU%2FcwluXTZYx206HF1MVBYxtbrh66%2BdASzLoaWkHGP7QQWbpULMURlLVHl1XgzImCC5qMLjg8uk%2Bzzed8JgpDXQHpzeU116lziJakMKQIAOoYUQg6GlEmDg%2FoSzyi75a87eQw%2BWk0OM2pDSLLgMAMFOUQSAd8doWeyjxvd8iqZ%2Bf4gRxsmHijpVoDCF%2FWs6fFfD%2Beb6u3RF17XiyX2hDDW8pvp4XFnJ38uvqajRi0NL3d69V2ttVeP82Xc%2F31%2FGmhv1yuHr%2FkOGPOB2xh7mXJ3Ps0x%2FDwHG%2B%2BzLePn7NRWn1sl4u3eFaURw3oGAw0tXynwn9abRbbxSpRzx9W2%2B3q1aG3bxPPUFG91wQnmYjMYQSRep09YPKRs817%2BjDPi%2B%2FJc6Qa%2F3x993WeKv47bvg8e08ueP3%2Bkrgjo9m3DYle5rO14bUqsohDSvdc3Z%2BIKK%2BPMDkIwgKYKr1bFyDIuxIghyIaz8k10AxhXMO2ZNo59616Bixpjsd5e6xh6cI3U3R0ScUV8jE4tnUmoCbZk4g65BM5EK4r%2FagGwPmuzU8IIREkAlMBsOBMEGLqoSjx2BZV0Z12n15BkQScEgcwIBRRFp%2BT%2F3Y0D2dgsEIRJaMICaIYxpMxxmnA458GSWgEoERUCMwkwSOchTNwMRABI8kwFowSCrC1%2FTSKWaCOWWjma4%2FHsNzXLk9UX7KtHLd%2FvTetRglRptWgjpkO4ghBCSimEnIJoCVVkEUofotnv0V%2FIeI4ljuKGJdUSOoypriMIKUCq9%2BuVGPWrXhdoxIxSv%2B9UUp0voOItX3EG21HC1%2BkqBEZxfQhoOAAQIjZmCXNtdHSJpDp%2B5%2FXprmWS%2BBUSd1FSRGFKBISMQmkTLZe8TikyL2dOXC8Dzoq4CfWAK%2F0iJ8IAHR1bNTP7rxP8%2FUiHtFEBqeVoUBp5EuVzZMZtUPFDDWNwcFKD83kl0GhS9XB82MY5ZUXTGIrllVe0k3EDnRZn62FVZwSG2IFmMT%2Fco3KoaYX6uEk11osx60j8sUONtnf8SCI7860%2FW%2B63pBFs9T5SD3g5q5khCrGw4o30SKH0lvVpJrxxJO0GVAiiBX4kb46NZxEWtY2JNZGfIfxJDV2On23mifIchrFGkRBJyjZlWegMx9pjQ1R30cWcmQyC4IkkhAU4lhrhD%2BQ2AjtzA%2Fa9q7qAGONbGwhPJLaD%2Bd1hxpzEIGuQnnyLxYcPL7YSzHHCRQBDpiklGKAoBWnxEQsSQwD9VuUJI%2FsbrV0g4vHT2FLot4AJyI2VBiEkNvcy1EUS2IubJB5LWyurZvg5elDkJI5phgCIhNEEoxQS46oAVpFjc4nMXLtPbWMWVaWxVQjRVAiXpeGTZBTFiWOwxijYtaTykOhx%2BsKTaSQ1zLl2kkbmU47gVyZQblW6whULVNjeSsWw7%2BfX%2FHi99mXb3f%2F8%2FZfv%2F30M316m6st%2B57dsnsPa6sZlZaH87gUyzSa7VTvaMG5IaAZW0eZNaUtpToWP4fqtzt4PsSZyVTuZgXETow0LznZzeqU1NM31CuT16ROIZZvcaf2Ij27TecepbYk%2F7qclzYzIY2ZdO%2FrXcErKwq%2B0qNtwfRvOTa3Zm1vpbnWy6HugFfTNBhVXNnJfk1u3NYOuG7Fq%2Bn8yuzS0P3wrhmvSwOyDRpoit4Sm2oCBLR60wsKy2luX9ENGLu85f6CcVUe9ClP2nZiPlCJ68Uo9jqWTp5nfnvgi48kR7pN8GcHwR8q4%2FVEtLfc15Bad%2BgO7eXAaN9ueZR%2B4T7LzO0d74WpSgtQra1DOyrCuqAbtIeubaUA963BfRHW87%2F14wHW3ZBXCusgAtAqfEFbwXhInHftHuIHCqM7D41eDIHwgpvGX6xmVEP8hLPKCzqC%2BNN3G32B%2BH6U87Kt04DWh9CrSgsnmMpWENqK15n0FkiGzqAwEbcSFpqUJeosGRyd7nOo3luEylGaL%2BTcU5sj1ImV2mr7X89kI3ICmRAR4AxDJoXk2CLDXZAE1nYii2F0Pu1EuiIZ2wySuNM8P1yTxopdgt1WwGUJVSwIkcxDvBizIjM5iQTRRKpYI8AjkVLhHJUlUrLaIo8%2Flot4vNf4MGc8pDPzy0N%2BYPb45WU3X%2F%2Bd1lhR5JKVk6DDEM0kCaGNIN%2FH0ZrEE09BxIuJvvGkRwoqjNhagCPUWe22GtntZzxVBERSaAHPwDSBBYpx3lEupmSmEE9CMbuaqQ6jkKZJmZTZZn5hmAtlRAEhAkJBBQOSmrmIAiRVEyCR6a8DciGKgGCMSsCIlMQhEpxFDCCS%2F9KupKNGPNEZr2MKeBIaRoBAIF7QDJkOaAZghGnFTKYrmlAiGQAS5jHWRpEFhiMSSwrIfjsr%2BNhhFvyFLvRd5Q3JECSYccgAN8WDch7FJD2OhV7DEj%2FjhQ4lkvFKj00sCqWkhJgbR4ygJOx4JAu9Q9v%2FQhc6jBdoJCRjHBDGKVDG7T47O4JiLx6OsHOPVnqNFMMzXukTSIiMMInVMi4g4FCYS53GBrPQOB15vdbJ6ZvNYa0XBISjCMd2NkSUIE6tmDHKQRSz%2FShYnVy2xwTGZlYk4%2FUOM2vMWuqERLQStr1a6igs9bbrFwoRSSYElXwnIyarU4QjQEbC6ryGoT5k8XmCQRQP8v7HCgrB3FEUoN8C3C77%2BOQRrJ6sMdaib3vLtlHR%2BVMHnpUMvE8DXKO4yuFC8GUDVa%2Fyf3V17DMrMt%2B%2B7KiwCt8qxDssPyPaKN%2FLr1MtXpSUlALGbuv%2B2ryWvLO0ld4jTmqBQUQL8qQ96iFNSsh3JkCmPuKq4O7USDur4C5qVMzxWslAQysZooZB1pKSkU%2FWCJUM5ZMZpZIh6tshww1wnf35oGT0rmQ0kB1PlQxX076p1YZGj1u20rxrqBR7vcGKiyZa8KBK%2FB61xtBcGsyUbGfPF%2BYo9N%2BdxuC3WwInjl5LR%2BDFMesZm%2FtzRIgROyLEmB0RYgSOCBEcEX7qCKN3RAi3I%2BJazwjiWoYAdRR7cWgE5Wmh49YCGs%2B3lXFZNHqha7o7UwKk324DlxIwuKNA9ucokCN2FMgxOwrkCBwFMjgKvFQCGsiOp0qArHQUHKcEVBde3v09alWg%2Bayb%2BV5OhwBGfeoCfjsEiKQRNtMuJ1h1yR0OhGt4BPxluTIfg08sVyf6PbBc%2FyxXX3Z8ZTmHE2WfP3%2BnsRwpd3XXqwc%2FbmZrPNNWKV4ntalz%2BqG2GoH1vlGbesTBkBeCTpwD1RM0QkMXghoOAW91gP0se6wEQFDDmRC0gP61gCbS46kaAIHDjzK1GldVaAB6iN69tjN%2BraxaZ2jdBegNR8hGHcWB9ekfh8BVg8EfzUFSEVGmhdVZSsTgofsQtN32pB456klM6Tt%2FZkOA2pBsUjKBXnFmDddE4MwhOLO%2B9HjLmQ6vjFH5KycxWCgoycs9xLoLGRTcyZaDWefYcfNkY3mow5O8TwMbghoRKYonT8Hj3phz8G1mqD6tB%2FN7P31jtL%2BdZd1Hr2KUeUS8Gvk6SexBxRhAxagvPb6qGK5K3nv3PC5UptUL3jaKVi%2BvVjpytaKxDHhnfiOlGvXcJ%2BD7YvvP7PLk76RHQNYyIH61bxKQvFA9AtyVEMoZ4%2FFj%2FTWf%2BhylqroU7PsSuLsUlCpLB1sPQBWVWLOpJLI7HhQl6tRWcxBSKz4CWvUZ0mct9Jlsq%2F45cWbTpzU4PpaGSB7bgGW5cN6m%2FIKyzi8JLk0yKEo%2BeTl%2FLrmRnZ2Td2ZEWV8C2%2BVJr4xc4KNbNx7MMr7Terbn99ldazzhTSFLiWrwvU9n%2FvnPP5RRqVuj19pTTcs6GLQ52MQ1APoXQua3z01b3a1s9YB2juJtwSw2%2B1LYFGkZ1vln0epRiY8mYltLkBuL5YkCdmuORXoJMxm9mEp%2FesZbPoK6pOXzVNEJJF1fhUarnQ%2B1%2FmC63Ey1L16sKgAc8lprwAuYY4%2BYLvcVg6zPxY05yG2gU%2FpFmk1HfDAhA897nxzUFVGpC6qxXwVEgDErySFTRE%2FWCaTVUaiLdlXuwoygmKgyYL%2BqQ5pgrr9GKH5wXYeVnFRqscmLT%2FP1Ih6wRDKn1d2vynXYXnRR0bYuWtdWecWbH3%2FdPNzcz%2BZ3f5%2F847evt7%2FeTVzeujYbT7XIj3qjF6ghMCrgYQ7j9wXV5Fa7%2F7TkknyLWydB5%2F0dqDt7TWzkt4fN%2B24IqttV7QgV6UptdcB5etq4mogfhPEcploo2BJjh1A7KycCt4Xaoj%2FUFkN6D%2BBVfe%2FBsUhfE5ufl6tv12%2BL11nm8Nxd%2BjZ7%2F2OVTlV6pHcEx6oiRdfuBIJ4pG31SGG2fZDWDdOvWHAtFLveQhipVZr8mCGclFi%2B0fY8Fk4Cgq58sC6aB57KQDkmO2OsixTSyFrLQd6yQCoykM%2BOBU7fzNuzAORWZ412OEGY5VCEdYMOSWGg1rO5Ss45vWqkkndLDabr2aH%2B90EEqHW38mn1nJ0FZwfoIlv0lDrh0OqlV9TngauJY%2B7aPaJd33mqz7C16BIQAURN3MzbLp7asxtYt%2B0POukwXhDnbhyvVqjPbeMNq05lne%2B8MVWLVtlrKob4gBrbtKH4hArzg7KAtdJ%2B4vb5KCv73lY%2FcadSXd6Cr9tNwEYO%2FdZ8Q%2FU185q5D433NjrYg8siRnSHk76hljulClsfjr0Fov2r76Yxza7INyUOesg63n4sC6jVPGOH59Fi%2BrpbgmeyMZJTXhsqAeHURDBV2%2BjkjRFkqgS4N5WADOtii8cUKOspYWoYq12oDb3AZQiNRldAoB9VAXMamWY8YywCAOc%2FpJbmULhxEnoGIINUOdZMD%2FIEoQhTrYkvMj%2BmxH3Xmp%2BtvLFXizrBufjdaiY61lML9s%2FQYvBCWZ4KNC%2FMQzaQa8R6yAXtLzAh0ykGZ1%2FSqicTcGE66FFL7ItNVp9YqNcd%2B%2BaU0FrmwxBdHwmxIs8dRTE5kJGrGJZy1HUQfu7KW22pp9v1p5%2Fit%2F82286%2FJSazL43dumn0R2VkGe6q3bU2wdSZt9JZthqsUVRKpVYVRnmI9ikwlqbIjKoiYOhq6BDWSPrrrvDJCRNzQCq8TrmqkRXYacpVWXLDZSdcNZAdXxOukMOuSZyLeiyVblpMC2aA3uXjWlNtmXbOfY%2FE1iSryinMHc6%2BieXOCml9dgOBOVmNmRIpGJoS1aidCSU20PcGHPOhC2EHSjxRdrylRHchbFmdznJXGXDhTGRJT5bnyI3NxcAMznQwo1rfPTFjg7rYvjCjOYRERaYOiNGD1slunxdHUDkbohpejsCL%2FfPi6CtnQ%2BQunS3NxO0985FyY%2FBQjraxUwK1t%2FTdr3vt%2FlC70Bm1eIYU21iiLH5wta%2Fu1yOLari1huxfDTnAEQCFPWc1gkxEalEMB%2FjYtTPdG8mezKljqHiFa7hJAqf2z6njr3eltjdtTtWZ7AhnKzDp0DJScfZ3m0VezpBfG0tXDX5FvdaxJuVBSydvZ%2B%2FE9IgkkjQwyZfd70yKUKe74ZLTSFLEJJAyCQQztYgJgixCmEqe%2FRY1CsRxJEl8By6pkM5tcy4jSKnA6rczxCKdNMJsT2dDyIR4Igav6UocID8eDY2MYTeAhN0AHzW0BrKTa2gmOg6uoZGStpjOEie5Dta0CWbQxFqVosOaGBS9ejqI3202C6xJMXAMWt%2BgPuY2m%2Fsp95o3w26Bl7x5xG6Bb7xZ0mizEW%2BW1%2F4KjNmy%2FNRgTNErY%2Fq9NwCRldaJBI1UmO5weE5HvRmQz7nPlEnDZoCXlHnEZoBnlEkdfqJpdW9qZ7AZqCp8lm2tnyHnNRYAs1TP8A2rIa3hxfKJ8zDGPnBe2%2FmQvXJePudec14N90XgvN45r4HseMt5Dh9PwnknNmsIvHiCkNTwntJe05Rog8xdL3hRQB94cdBE3ZN5cQx5uWreAy%2F6xYtH5OV6xovMnZe7twXhrnGXVb1mqrFm4L9jhcHKLy1Kgspr6Yf9mN8RNwX2Ixh4wH7M4UwZD%2Fux%2BlveAw5xCLrxkf0ayE7OfjAynWHD8195Em5u7RHNFsw39qzqrCQwYgsCYjGi0yJEvXKi3%2FE0RU7kwgdOHHVADRtDQA0LATVecuIRATX%2BcWJJSA0o0NatxoYyMGAL4lDDJ7oPmeyJA0cWIUMF94AD%2BagjZPI595kDeYiQ8ZIDj4iQ8Y4DucOtM9UzEXPrsFjbm5cEmqbmY56gUYcY086zZ0iMHSS99mwacu%2BDaKyOocmgFZ3MfWP2qINo%2BBiCaHgIovGRFhvIjq%2Bbha7OlS2Qot7xylXk6XLtx%2BYyY6pRDpJkLizqjiT9jqg5WHkJEg8qL%2FFRB9jwMQTYqLaUgTP94szxB9gId4BNO5WXFNkioF1luWYrwnVSatU7d1kFDe%2B0ZlNT1wNcIic3lkmzwZyzXhNxyGR3rCw8j%2FThmEdWo2DKfUgBUeAyTiYW9ffjBxzioYN9DgLFhXJxA%2BnJudhEvuG5uCTYJ6%2Fz6%2BxLmWfxO%2B3XnD3vTQ4tsrNeTTjvNqm1fzxDrmwuM6bP0unmVUZxT1zpdwRQoaIOxsOz5KjDf8QYwn%2FE0OE%2FgSVPlh5vWbKk%2Fj4x%2Fbu5rYfKmfFgXR10tS%2Bwo%2BdYWobwjekwDtV4WpI9s8F6cXMQqeyGnrjW70ijIteKYrPZnolAjjrMKJ9wn7lWDh1mFLj2ZOkp49piS8d%2BuVY6HEpHcm3N2q%2BBcdtk3OYSaMifwxPcr3Ur%2FQ5iKlZZx4NXi5WjjmCSY4hgkkNHMAXGPVl6fLVuZUkMU%2FXeaaga2yJrNpci0ytcbLSRI0ZPrOl5VJMdLU0FiUBx4fWN6qMOY5JjCGOSQ4cxBeI8WXo8JU4ESgKZjiDO0KbkJPo8tdCQa1O1VwJFoAYVpATaHUva%2BTGYikhqP0OH%2FeY9cofhy5rSuJ9Kj3kx9%2FO1yovx733yEIEXj%2BbFJtLjKy9Cx%2FbAtLqaejEFBmgseG3G%2B%2BY3mZ4hmR0hADUSQWGfPlQEHT78ocmMABYRn8gM1nA0D09m%2BVR6TWY1HNCBzAYgswbS4y2ZOTzv09PLpAfCO0FIahCequLbE%2BHViO%2FsnfAo9st6gzV8xB4QHiuZEK8Ir4a3IBDeEIRXX3q8JTyHk2Wap4QUyxjomZIV9DY1WTD3ed5d2YmTeX4l0rgQm%2FfJNxQvlzUbS9ph1kSq33M%2FrIlq%2BKD6Zk0KoF%2BsiRzOFP9YM59Kn1lTjVxgTc9Ys4H0%2BMqayOHNMVizSIFAJT2WVYi1Sg%2Fo8a53GeE1YsGMOM%2BPC5vLT439P%2BHCpu64sIYLq2suPFT7BzMcoaFzKfMQYc8JkZTMileEWMNtEQhxCEKsLz3eEqLD2zNtpcpPbjrqFqNOlFPHrQJRHidXNYxG5YzqiSg9CJQphJMyjIYPJ0WKmz1nxjGEx%2BAQHuMpM44%2FPAa7w2OMBltCiwe9vjqYXaEfP0fa6iAkRvZq3uEarqf%2BWUtAD1gLjyIOJp9Ar1krxMH4yVoNpMdb1nLHwRxmrfLUhjNkquYTfajlseh1Sw57EMhS4CmOpA88NYrwFTyG8BUcwlc85anxh69ghxMkidd0lXLZh6mASo8jKCkMDgpezGKsp%2B6AtIqpco0NrUeyMvjO2LZrLnJmQw93HEuvLkniQRwL5zySfL9zZxnAZOg2V3lokd%2F0ScYQx0JqOBMCfQ5Anw2kx1f6JO44lix3DxfiVajGao3SHe60gzsilGoLz8p1dxdns7IumPb37TnSZHPRqtFjQ53TE016EOJygCZVzM%2BA2D6K6BYyhugWEqJbPKXJ8Ue3kJLollP6PhbDPS3jEppHirkR1b2nztiIbC5RLKphRqr4x5740YPIFsgxiqQxMjQeK1efKehSHroD81HEtpDGG9V8aIWDhkgXT1nyiEgXM5dpcJakJZEueSaD1Vax2LOxwiNb0jZKQs0g1DMupGZ55pdTk52teFBxllxZX64qXay9VpShNVxePXCjtLiRCDR8D0ZERxFBk0%2BhzzYjDRE0frJhA%2BnJ2dAslD88G5ZUksGHfKCB4zrEmtqbiv12WUTUg0gcyAmOrAAlzH1gvFHE4tDGW9sT7BC8vsc2BOd4SoFHBOf4RoHu4JysYrZeH9ukqAb7ijUps1h%2FpiZlppecIWXWly5%2FzELmReQNrdhSxMNXkGGjiLxhY4i8Uc0%2FAzd6xo0NpMdXbmQlFWT0wBe93OhdZYGYsu3FnOL0XA2rmowe6%2Bos6qZSOhobm%2FIcmbOB7FUxJ%2BuXOT0IxnE4VLGEHpiXbBRBOGwMQTgsBOF4yphHBOH4xpglQTjtMma7DHiW7tYGslQZbuOQng4Z0I9wmwIDEi8YcBThNmwMpWR4CLDxlAGPCLDxjAF5SYCNHgha7GoPA9%2F1hjvOejTMITYuTOqM%2B3gNP9YA3Ick9YD7%2BCjCafIp9Jr7QjiNn9zXQHq85b6SgjQt7iXq2RxWI9887aJYQiD%2FdCsd4xKY8Qi5MqSqmKaec2dPzFi7kX13zDjh0FxrdPi8RD5oq%2Fra4jeClvRIqXqBFH0jxSNa0ntGisLhbJgebENxiilY0bYp30oErrZNugGZR%2ByoJvUXEXLTXN5qVONW%2BVz90KVwOCCGp8vhq92IGgb28HQpyubAJ7oUNczxQJcD0GUD6fGWLh3%2BianV3Beb4TL1S8YFZuwDmEzqqKx20%2Bv2oqgRQ9I7MxI5eL65qBEQ4gEz0pI58IoZa%2FgqAjMOwYz1pcdbZnT4e6Z5Hbg7jeCIRnOW%2F%2FTolr5NGZDNXhNReXvYvOfTdGaM2FikDrc47Lm%2Bjajh9%2BqBES2Hs7KXh4NxWSNAxANGlCVz4BMjyhruiMCIQzBifenxlRGlw6Vz2LXatMNvwc1qUONBk%2FIMia%2Bx5AgT4B1i02vZU1nDf9U%2F7YHB88xljdiQ4Wkvnz2vaa%2BGryHQ3gC010B6vKU9h79mSBdpTpZp3CnVjEW9LDgpxKYy0%2FQ8P6ZsLmw1TETiArLuuNKP6BuTK7GqWjEgwI8i%2BkaOIfpG9f0MXOkbV44%2B%2BgYDd%2FRN507TwIktCFUVCyrG64UFMfDAYuScVFW1USVHB8NxDMZgPu6n0mNKxCCYj15SYhPp8ZYSS8zH%2FvtJ6XkYeg8NZHpuod1nw2pHtd%2BJvNXo2vl41v5l%2Brc8Q5o9QlDNeqvFhEgEaZ%2BUC2tYBZ0nRDJhsuyE02K4DsWOgclu3cXIoLZ3J2frx0weaZEGnp%2Bf0eNjQRzjd57YA6OsgUzmU1o%2Fhswx2tDRSbTL0S5uYP7xsX5YfZr96Bk3YjZ7Wn3TuD2bNIQtfoQdTIhBVw6%2BIp3pQkq6B86MtoCAOeL2SkSTdDYybadF9wUE%2BZQ2krveh7doz9zPNttfYyIe%2F9JvMAVmWqgOBKqDcE9A4EH8LuTMBgLsAgLikFTSnaS2HcHbGxAcFdTb%2B%2FC6q5pd32t2CtEMitSigdE5qAjHzRB05bx1hwy4hkacCuuf2TMicw5sR8HzcvXt8fNsvY2eZjE2zDb1hv919TUDkuTVer5Z%2FJ%2F%2BerWdbbXXT%2FPlXH89f1roL5erxy%2B5h8WEKbfHonnyDyAWmFFeBLNctzbdE7CzyXRFDLJlsmrejSll%2F%2FuxSo6%2BztYvi3ihJNVywft361%2BI4%2F%2BS4QLJ0pss4ulKBiw5ebJ%2FL1kbk6%2Bz9WIW%2F%2F%2F28TpfLx7Tk95W69fZ0nHWPNYFJrNN%2FPeBE2fLeF2%2FzbbzTcmJX%2BK3F28v6buzj%2B1Ke2%2F1vsOCSSxKZac8z2fbj%2FV8splvt%2FE5ZZ%2Bye5zEMVfrxPj%2F99yR5zwtXlCpA9L97g54krcgUYOceCgnSorsq3azk2Hh9W6e4%2BW3e0vNc8LWy9lmY0z%2BO9RPYC%2FZ%2Fztx2bzHc%2BOSGPsJkSEi2kPkmOwSH5BdVfh4uvMuXR9RhCTZYIqUN64yCJFO1beMV1n6Rc0v%2F7C2j8Qnvu%2BPteiYvxHJr0shuL%2BfSuZWCI5AK2mhFRFFtILKpjV0g%2B7AymWcBrAKYHUpYPXTNEBRAkUOv3DfUOTBHjXk1NYoHRid1%2BfvZzMVd7wv%2Ffw8ZyX2MJcPADSwh3HjXRuVTnyw4Eh3w%2BvBXvXu9NLQgAvdq24uTPl2ni971di9V91nd7J%2BHTj23nAHc13ZULPXqCrsQWyxg7EcDt2%2BGavj4OI2GatxjKgHjOVBwHFgrFaEyTvGIiXl%2FqzY39y3o0cJA20noVgA8Hy4qpUI4J65iri80r1zlb356PKA9QymxOUB85OrSH1Df8Dx9KC4XiCn06RHkRPyjZzcxfUGaM%2FlZLL805nKpBkFnzUQjMrSP%2F3ymRfBNLbtRYa3vUjH1fDa5LPGFaiGt72IBxXyAr21Ikz%2B2V7uCnnt2F51Oo%2BcG7HVF4kqYoO9EhstDx9KxsEY97ItVlHYLI2pTcHH%2FiCWux%2FHpmqyo0oKXuhpQR5U7OB%2BWzR9xpKd0VPERI9GAwpVdqNPb5It3PheH9vVJhOTMnDUkbQ0I6mxojyh1Cx8kRi2LpvfqSN1FvdJXaZYM1FCpfvu0zzlTgcgXbO2lOWaeeNphlz38lQNO3b8qU3aT%2FPn2cdy25L4MEkiwgGTlFIMEGSGMMUaTiQlwyD7VcVEdIziOJKEIsYlFZK6kn25jCClAqvfzliM1unQltH%2F449lEuSxxofV0Id0bn55yA%2FMHr%2B87Gbsv1MVS637DAKoS0e9v09SzzudTCJBBJnc%2F5izyaiMVMUQHRoYi6CjLxWCJAKdxVxQlxXVEkJMVeTxhS1mCkQEJMQSQsAAwSYzMMyiJExLpr%2B0qHMiiCIgWCwngBEpiUMoOIsYQCT%2FpZ3Jh2unKYQHnnt4YKYsJofXLw%2F%2FkaSr3O6uVv%2F%2FpzaL7YYRZrDznC7l%2FXl%2FLF7jOUPgt%2Fm3%2BN%2F%2Ft3rdhek5lBJZXQEuL3xaLBGeevmKcYJ7%2FTeJFixDs44DAx%2Fg09MzcFEaBBzLlhRZureAMrziEEZEIzNRZC6FYf2ECTLHBmWApBFBkufIc9i6JkXrul%2B4svY6mtbKvDtvDJtIVVdbqVwARo7ixM4cvw5xK6SFBdzyT2Nqmr1RBL%2F0Rj%2F%2F%2BceBLIpzRRtVTl6hDeIRLaKNq%2Bpth2CDAtiMGmwu0G47sRxacn6aegocN7owDKLcrfH0a6mVbz8EEAogdLYgdO5OoiLcCOoD3Lj2nQLcBLg5c7jREgpvVS%2BUi4IfznDEueajLiJRv5nsrHxXNSBRQKKzRqLrvA9FHmcotJBCcZkIlWzpE5820VxB4gGhAkJdAELJPFRa30dL4xUvC5Uwj2g1Krm61HSISq7cioBKAZUuAZVI4aTTN%2FsrY6nPE9QEcjiiZL%2Fmn6v6SYCxAGMXAGMH675eGBoJGHGXXuXoF98hIIUo7gBIlwpIU837pLc30NWmPL1RC7Sc6l3F86dRreD2KtpF4RmXrsIPvWpXPMR%2FBzC7UDCTU%2B2CPIl%2FB2N202Yd8%2BLjpIBz5w9dZt6loMhhGPbq31I9RwJ0BegaCXRdI03zAZoHqghalrJ0o10otT1BonSw5MjZx0pRhCNuZQAT7rQJSZ561xMahRjxgEYBjXQ00nSsvF84KJRLKn4e0Gq57848a0wjVvMQxqUL0JCzy2F3cBaizQOcjQvO2g5puNZOEtrFCrnOGpUmUgKrdoEE0lWEiziK%2BnWISyEsPeDSuHDpWm3W7XEGa8rW%2BVttXBjhmioySsFKou%2FgAq6IfmElxJgHWDkzWCmYX%2FySzSwWgxAF%2BQ80MAgCIFwgBF3FajtEoRBHHlDo3FAodRzJO819JLRrLg%2BIeAUQSQojACqDyFW92p4gKQSRB0gaGSTlbm3L33MZllYptgiGD2CLcjv3BC0hsDtAy9lAS7C2DCDCVUoOOqzk9Jq%2Fy0NEd0Ci80KiYG4pJKoyt4SQh5AI9OqHFiEce9xIVAk4HQBJaaVZ%2B7Pyrh8uYShtSzRcMW%2Baw5yejptjF9eOWA0GknClxNKjNYw9V2Xdh3VvEHgjkl8XBN7fTyVj7UAglAzkTXLyKCMWSVTARQP5eg04EiGaOyBfQL7TkW938aG84YCNOTZSEBErLQ8cxEbUa2y56LCvmNrESa0FS%2BKQFu1LXZYDcImk5QIxi5ddVvsymOw7y9igIRJgwIWqqqp6ESIaQTGaXoSiRjPsM%2B5FCGM7MpKcESAQkAIwK3CbwPjdfS86RzjBrishoSRWyICECDr87ZDhiEBBQfbbHaiU7%2BydDCoX2qwQEmHGtjEkIlxdS1Um7QmLYkBFpDKKOpj6ENw%2Fbl378vydslTH8HJTNyej9J0%2FswWP2iIiaFnzkkSA7TXWohrR69YugeUbKoFbjpvzCQSIR4CUdcKlmEfxW7n24dAk%2FemEm99Zm6f508v89%2Bzlar39vHpZvc2Wd%2Fuj1sjvz%2FlltXrPpvavGHd%2FZPORYbg28U%2Bzzed8qT9%2BrL%2FmL0onaLP6WGeYVfZVMpd9DJIv823Fmdkdk%2B9ZOeHr%2BTImka9z4zk6mALHVsNUr%2BcKzIrTU83LUFYq0UwoLTMNPl6X14%2Fblb7yfpk9zJefcjacPqy229WrY2luVxYkr1IL4Xb19jZ%2F3GayYYJ6G6sPIxZJMx9qwkQxHYo5HAOQdDeJbIh1FI%2Fj%2Bsc%2Fk%2BsjTtXrf2X3272Yfjde%2FchedbMA4UgXoMPjnfnu8q1bWqhACjSXjLkY7eJa%2BSom2q3Sc5imRomzWqcIYC%2FXKfGL77QVjBqt4FPWKRpqne4uvV6vZz%2B0E95Xi7ftpjC1%2Bf1PmW3kptZrc%2B3qTtV0BZ%2FRQiSYRbBYDt2nNRniT4MXZFxekGyjRq9DoJeiu63errlAT8kEEgIi5Q%2FJ%2B3mSyLWpR3ivJaMICmGnAYAuCoC0yFWRGSsBkJLcZBRRVrlN1Dc24RCIGrDp8rBpdP0WBkArDqEX6hMOEaMBosYFUVIvn1ksQsc0b1B6TqwJAC17R%2Ffh5mpU8u4FmnZQEguXEo%2BTD6qTw%2FsXcCng0kXi0u7unrdT7xqnsIyseB3OkBdQRUMgYICqkUFVeSCg5l1y5EVfHO7YQYIcyojByrQWEsMS6hWAamQUzN%2Bertfr1bf41U7WErS42Yli8bA2Debu%2Bfz7Ypvud9Ps1b%2B0d%2Fab3ckLtdetbZIbe%2BT5BnrJHrmx016Y9XTwq%2Bb44Fa6iiY4uJOOVXzQwb10TQqoo%2BahOtZsy%2F31%2B6dkk12TSSzNBHyqCiyqe6TfPbtsL13FOxFi3okw607p4BTu1Nomf0WF%2FKfFVyd72mgtDiQffiydtym%2FYLloeEFpEmWlnnhn1vzTU8GsE3QHGjC7R9TMJ9OT0vTPBerkqfnSOt%2FpEKz46DqKcP5Zd1rk1WFd2Ly2OmdOPfmOj9VkacmX%2ByfXwzLNTtXZY%2BSDT7XpgOVdPSrU%2F%2Fzde20EgBmr5uycben9tTNLE3nuV8KvD03ivjNc0%2Bzc3GwChSC9fMBR4dOZJrfAmMeac4dU7xWkJ2LeaTe3bli2%2BtKbC%2B3rFP3kt9paqHakN1puY5AciTQxoNpY6TgjG664xga3CwatvZDi7AAt03e3VG2paH1CLZk8bjmUwLgbLe%2B021odiHaDfMzz64MsNGSwgF3tPxkjyQpfARh3y%2B7ZhuTHBxNNonBwp6aUWDyJwriLMbxyps4s58%2FJZaWJM%2Bt5rObMHnZ3S3TdLNgyvjW9SYoPxMsxufnNav00X2vKcbb97VKODxgQtl2UWLm7CMfsKeJjoNJeArFxxM3IYdSK0jvBajNd3VZaqurq%2BXkz70ZLpSHIMXh4xurhybkIaWjqZxXfjvfhCaORae8yKSLi6ljAevXfhBDGAC9nBi87M%2FCygxSLcMMRHxprWAhJDFhzhljTRt%2FKgFCIK1NQRyiM1Vk9YVSISQwYdYYYda1jzrWZdn6JyGNBjyCult1960ch7jBgzzliT0jKOKT7CEgGR58QShjQZ1zoc6iHSrDLGmMTg5HUf5gBUxAQ4IGNRgJSBaQaF1LV6vUd8Kp1vOKOIOne8aq8%2Bn%2FAq4BXPuLVgSSNg%2BlmF4ZCxVQNQiLpWaoGKxaK7KPUqDNvQ73jztswyh6WT6We3gHznI5dWkgEkumqTPLYvfoUw2I8vEkR6elpKR1YZVgcro6obP2W6yMW4tYINvtbIGzeoesEC%2BaKLbEkMOkS8n5llt3ezXHy09lCbhxbOIEcJD1vCxXa8zQYEaGiAxm7ur1g2dUK564N9hbhFd5SfjstzMrbKmnwUjqFxWk5IC6HYXfAIXbtD1pDvPmSqhEpZLqqdZYN1ct69rSY799TI6tNw74mvXMScuhMPubIWqOF8vq6RKzycvkQqdfZV08%2BcrZ5T7%2Fm8%2BJ78hxp4PB8ffd1nsYP7yA9K4v6%2Bj3%2Bwu%2Bfo9m3DYle5rP11eFCpifLTvYuEuYKhg6KdnSOhV31ZiKqW4xdc3ZaiH5PMwWIFuB0rSliVs6OnuaTB%2FkLzay0YumdYfl5bPwhT74dXV8nFN9aPd21e7DlF9fmnWxxdSeNptlKomJtXUQc0ojB6dL4ijc%2F%2Frp5uLmfze%2F%2BPvnHb19vf72bDFOVPlcVUX1dsZZ6mLgMDfVQyjwhuC%2F1ENVUD1Vnja61wwmkyiJQEcnKHjmgIJYX4i75JIbND4I4U4HLkoOTZ8OVl8R%2FpI9xrMrqFPvyXIvMoj4hJXjv8zuywN2VI9fqOC%2FhoXhYI6%2Bore%2BP2Ow1weO3h8175mUYhpaqt6zLG1y2kXZ1mMI6SLyqQvgWTCMQCWERmOoAcHK1AROfhHmDVrKunIOjLPTBurKgRvUqyjnwBMISdWtUKNdXb%2B0eygpKUG6Ii8xYp7QChYCg6oJuKAa6Cqa0xjGgUMABlFd4ACfk6urGxaHuwTby1yCfFmpvtDOaut1V0V65kHS9ZyXnMLmKYjQbJpuHfBy8QSp7XAR7K4JqI2s6b1GsrM%2FTuLtVdv738yte%2FD778u3uf97%2B67effqZPb%2FOJywUXtlPDdqo2i75tp95ptMB1ohhnLrQDdgo6ZvlmKaAsrz%2Bu9k8Ej6Acov%2BtE2EcrtiAMAFhxokwyYvRp0O3jjgMigiKHhAnfrleJfO1V4GSTa9fV0%2BJmnn3%2FwE%3D%3C%2Fdiagram%3E%3C%2Fmxfile%3E)