# **API для конференций**
[![Build Status](https://travis-ci.org/TIGRAN02/JB-Task-2.svg?branch=master)](https://travis-ci.org/TIGRAN02/JB-Task-2)

## **_QuickStart for MacOS_**

1. Выполните `brew install node` в командной строке
2. Склонируйте себе этот репозиторий: 
    `git clone https://github.com/TIGRAN02/JB-Task-2.git`
3. Перейдите в папку с проектом: `cd JB-Task-2`
4. Выполните `npm run start`
5. Сервер запущен на `localhost:4343/`

#### Сервер поднят и доступен также по адресу `https://jbconfapi.herokuapp.com/`

## **_Документация_**

### Основные URL

Относительный URL | Необходимые параметры QueryString | Результат
------------------|-----------------------------------|----------
`/`|-|Все конференции
`/find_<field_name>/`|`<field_name>`|Поиск по какому-либо параметру. Более подробно в пояснениях к таблице
`/find_participants/`|`id`|Конференции, в которых принимает участие человек с данным `id`
`/find_date/`|`before` или `after`|Конференции, у которых дата начала позже `after`, а дата конца раньше `before`

#### Пояснения к таблице:

1. `/`:
    * По умолчанию для каждой конференции выводятся все поля, кроме `_id`

2. `/find_<field_name>/`:
    * Если `<field_name>` одно из: `'_id', 'title', 'ytLink', 'country', 'city', 'link', 'status'`, то выводятся конференции, 
    у которых значение поля `<field_name>` совпадает со значением в QueryString или содержит его, сначала идут совпадающие
    
    * Если `<field_name>` одно из: `'projects', 'tags'`, то выводятся конференции, у которых в поле `<field_name>` (это массив) есть элемент, **в точности** совпадающий со значением в QueryString
        
3. `/find_date/`:
    * В случае указания только одного из параметров в QueryString, происходит отбор только по нему
        
#### :warning: **В случае не указания необходимого параметра QueryString запрос будет перенаправлен на `/` с тем же суффиксом (см. далее)**

### Суффиксы

Ко всем URLам можно добавить один из суффиксов:

Суффикс | Необходимые параметры QueryString | Результат
--------|-----------------------------------|----------
`/exclude/`|`fields`|Выводит все поля, кроме указанных в поле `fields`
`/only/`|`fields`|Выводит только поля, указанные в поле `fields`

Поле `fields` может содержать как одно поле: `?field=title`, так и несколько: `?field=title&field=country`

Список допустимых `fields`: `'title', 'projects', 'location', 'tags', 'dateStart', 'dateFinish', 'participants', 'ytLink', 'attendance', 'link', 'comments', 'status'`

#### :warning: **В случае не указания `fields` запрос будет перенаправлен на соответствующий ему без суффикса**


