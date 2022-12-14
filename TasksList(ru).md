# Техническое задание приложения "Tasks list"

**Проблема:** У пользователя в течении дня возникает много домашних и рабочих дел. Некоторые забываются, откладываются или выполняются не в том порядке, как хотелось бы пользователю. Трудно оценить всю работу, которую нужно выполнить за день. Непонятно, какие задачи горят, а какие задачи требуют меньшего фокуса.
**Приложение:** Список тасок, который можно изменять: добавлять/удалять/редактировать задачи. Можно помечать задачи как выполненные. Таски можно разделить на важные и второстепенные, рабочие и домашние. 
**Референсы:** https://todolistme.net/
**Стек технологий:** Четкого требования к стеку технологий нет, важно иметь возможность масштабировать приложение. Код должен быть хорошо документирован. Стек должен быть выбран с учетом того, что он будет доработан другими разработчиками (иметь достаточную популярность и комьюнити чтобы считаться стандартом разработки).

**Комментарий разработчика**
После интервью с заказчиком для разделения задач на важные/неважные домашние/рабочие - было принято добавить универсальную сущность - тег. Тег будет иметь настройки оформления которые будут накладываться на таску. Важно проработать функцию ассайна тега, так, чтобы часто используемые теги можно было быстро назначить.

**Комментарий заказчика после интервью**
* Frontend: React, делать на тайпскрипте и на хуках
* Прикрутить бутстрап к приложению (https://react-bootstrap.github.io/getting-started/introduction). Если хотите использовать свои css фреймворки, выбор что использовать оставляем за вами, так же как и основной дизайн.
* Изучить, что такое Кастомные хуки (https://reactjs.org/docs/hooks-custom.html), попробовать написать свои. Для примера можно сделать хук для работы с LocalStorage.
* Добавить возможность хранения списка ToDo в LocalStorage, чтобы не терять их при обновлении страницы.
* Отрефакторить структуру приложения
* Добавить возможность ассайнить теги на таски
* Сделать фильтрацию тасков по тегам
* Использовать context для хранения информации о выбранном теге

* Разделить приложение на страницы:
	* главная страница со списком тасок
	* страница со списком тегов
	* страница с удаленными тасками

* использовать React Router для переходов по страницам

# Сущности

* Таски (tasks) - основная лоигческая единица приложения. 
	* Всегда имеет название
		* Всегда вводится вручную
		* Может быть отредактировано
	* Может иметь связь с тегом
		* Можно удалить тег
		* Можно добавить тег
	* Всегда имеет статус: "завершено / открыто"
		* Может быть изменен. По умолчанию статус "открыто". 
	* Всегда имеет состояние: "удален?" булево значение. Дефолтное состояние - false 
* Теги
	* Всегда имеет название
		* Название вводится вручную
		* Может быть отредактировано
		* Имеет цвет (выбор из предустоновленных)
		* Тег может быть избранным (его цвет будет влиять на цвет строки таски)


# Функционал (описание UI)

Полное описание функционала приложения. (Далее функционал описан совместно с разработчиком, на основе описания выше и интервью с заказчиком).

## 📄 Страница списка тасок

Представляет собой сортируемый список дел. Это основа приложения, поэтому он должен быть хорошо проработан, раскрываться на всю ширину и высоту на мобильном устройстве. Список отсортирован по дате добавления таски.

### Кнопка more

В коце строки таски кнопка с вертикальным троеточием (more). Содержит выпадающее меню.

### Добавление таски

Через input расположенный над списком дел, по нажатию на кнопку клавиатуры enter, или через кнопку "+" рядом с input. Редактирование названия через кнопку "more" -> Переименовать. Таске присваивается статус "открыто"

### Удаление таски

Удаление таски через "more" -> удалить. Таске присваивается булевый статус "удален". Удаление происходит без подтверждения потому что таск можно восстановить.

### Закрытие/открытие таски

Через чекбокс вначале строки.

### Фильтры

Фильтрация списка тасок возможно по тегу, или по открытым/закрытым задачам

### Кнопка "закрыть лист"

Отобразит конфирм: все закрытые таски будут удалены. Вы можете восстановить их позже на странице корзины.
Кнопка так же имеет дропдаун "Удалить все таски, включая незакрытые".

### Ассайн тега

В строке таски выпадающий список с уже сохраненными тегами и крайним пунктом *добавить новый*. При добавлении нового тега нас редиректит на страницу редактирования тегов.

## 📄 Страница добавления тега

Содержит уже имеющиеся теги и позволяет добавлять/редактировать новые. Список отсортирован по дате добавления тега.

###  Добавление тега
Добавление тега происходит через инпут вверху страницы, там же можно выбрать цвет, который будет присвоен тегу. По цветовой схеме тегу присваивается основной контрасный цвет.

### Редактирование тега
Тег в отличае от таски всегда можно редактировать Inline в строке

### Удаление тега
Через кнопку-иконку trash в конце строки

### Избранный тег
Только один тег можно сделать избранным, для этого слева строки будет кнопка-radiobutton

## 📄 Страница удаленных тасок

Список с чекбоксами, выделив несколько тасок и нажав на кнопку "удалить выбранное" можно удалить выбранные. Список отсортирован по дате удаления таска. Список имеет делимитер с обозначением дней.

### Кнопка удалить выбранное

Становится активна, только если какой-то из чекбоксов выделен. Имеет dropdown с функционалом "удалить все окончательно". При нажатии "удалить все окончательно" из системы удаляются все таски со статусом "удаленные".

# User Cases 

Типичные сценарии использования приложения

## 🚶‍♂️ Повседневный

Пользователь создает список дел, в течении дня постепенно помечает дела как выполненные. В конце дня пользователь нажимает на кнопку "закрыть лист"

## 🚶‍♂️ Пришел из отпуска

Пользователь после отпуска возвращается за рабочее место. Видит лист задач которые уже потеряли актуальность. Нажимает на кнопку "закрыть лист" -> Удалить таски включая незакрытые

## 🚶‍♂️ Таймщит

Пользователь хочет вспомнить содержание задач прошедшей недели. Он заходит на страницу корзины и видит все удаленные задачи. Чтобы найти задачу можно использовать делимитер дней.
