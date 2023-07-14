# Шпаргалка Laravel

### 1. Artisan
___Конфигурирование приложения___

Описание | Команда |
-------- | -------- |
Генерация секретного ключа приложения. Для того, чтобы генерация и внедрение ключа прошло успешно, ключ 'key' в config/application.php должен быть пустой строкой. После генерации ключа вам может понадобиться очистка куки в броузере. | `php artisan key:generate` 

___Миграции___

Описание | Команда 
-------- | -------- 
Создание таблицы миграции Laravel | `php artisan migrate:install` 
Создание миграции | `php artisan migrate:make create_users_table` 
Создание миграции для бандла | `php artisan migrate:make bundle::tablename` 
Запуск имеющихся миграций | `php artisan migrate` 
Запуск имеющихся миграций в приложении | `php artisan migrate application` 
Запуск всех имеющихся миграций в бандле | `php artisan migrate bundle` 
Откат последней операции миграции | `php artisan migrate:rollback` 
Откат всех ранее запущенных миграций | `php artisan migrate:reset` 

### 2. Migration

__Список типов данных столбца базы данных (migration)__

Доступные типы столбцов
Построитель схем Blueprint предлагает множество методов, соответствующих различным типам столбцов, которые вы можете добавить в таблицы базы данных. Все доступные методы перечислены в таблице ниже:
- bigIncrements
- bigInteger
- binary
- boolean
- char
- date
- dateTime
- dateTimeTz
- decimal
- double
- enum
- float
- foreignId
- foreignIdFor
- foreignUuid
- geometryCollection
- geometry
- id
- increments
- integer
- ipAddress
- json
- jsonb
- lineString
- longText
- macAddress
- mediumIncrements
- mediumInteger
- mediumText
- morphs
- multiLineString
- multiPoint
- multiPolygon
- nullableMorphs
- nullableTimestamps
- nullableUuidMorphs
- point
- polygon
- rememberToken
- set
- smallIncrements
- smallInteger
- softDeletesTz
- softDeletes
- string
- text
- timeTz
- time
- timestampTz
- timestamp
- timestampsTz
- timestamps
- tinyIncrements
- tinyInteger
- tinyText
- unsignedBigInteger
- unsignedDecimal
- unsignedInteger
- unsignedMediumInteger
- unsignedSmallInteger
- unsignedTinyInteger
- uuidMorphs
- uuid
- year

___Пример использование:___

`bigIncrements()`
Метод `bigIncrements` создает эквивалент автоинкрементного столбца `UNSIGNED BIGINT` (первичный ключ):
```
Schema::create('examples', function (Blueprint $table) {
	$table->id();
	$table->bigIncrements('id');
	$table->timestamps();
});
```
Более подробное описание __[тут](https://laravel.su/docs/8.x/migrations)__.

### 3. Faker

__Список типов данных Faker__

___Person:___

Форматтер | Описание | Пример вывода 
--------- | --------- | --------- 
`name` | полное имя, рандомный формат (из списка в классе). | 'Алексей Евгеньевич Константинов', 'Mrs. Alysson Feil PhD'
`firstName` | просто имя в зависимости от локали | 'Витольд', 'Cathrine', 'Добрыня' 
`middleName` | отчество. только для `русской` локали. | 'Александрович', 'Алексеевич' 
`lastName` | фамилия | 'Егоров', 'Матвеев' 

___Address:___

Форматтер | Описание | Пример вывода 
--------- | --------- | --------- 
`cityPrefix` | тип поселения | 'Ville', 'город' 
`streetPrefix` | тип улицы | 'пер.', 'ул.', 'пр.', 'шоссе', 'пл.' 
`region` | область | Московская 
`regionPrefix` | тип региона. отсутствует в английской версии | область 
`buildingNumber` | номер дома, две цифры | 26 
`city` | название поселения | 'Балашиха', 'Видное' 
`street` | название улицы, только в русской локали | 'Ладыгина', 'Ленина' 
`postcode` | 5 цифр (вообще-то в России 6 цифр) | 23545 
`address` | полный адрес.форматы в локалях различаются | EN: streetAddress postcode city 
`country` | страна | 	'Австралия', 'Австрия' 
`latitude` | широта | 77.147489
`longitude` | долгота | 86.211205

___PhoneNumber:___

Форматтер | Описание | Пример вывода 
--------- | --------- | --------- 
`phone` | в локалях различаются только форматы | '+7 (922) ###-####', '8-800-###-####' 

___Company:___

___на русском языке отсутствует, есть только англоязычный вывод___

Форматтер | Описание | Пример вывода 
--------- | --------- | --------- 
`company` | название компаний | Bogan-Treutel

___Lorem:___

___на русском языке отсутствует, есть только англоязычный вывод___

Форматтер | Описание | Пример вывода 
--------- | --------- | --------- 
`word` | название компаний | Bogan-Treutel

### 4. Функции Laravel

Список всех функции для полноценной работы с Laravel можно найти __[тут](https://laravel.ru/docs/v5/helpers)__.

### 5. Route API

__Resource Controllers__

Если вы думаете о каждой модели `Eloquent` в своем приложении как о `Resource`, обычно для каждого ресурса в вашем приложении выполняются одни и те же наборы действий. Например, представьте, что ваше приложение содержит `Photo` model и `Movie` model. Вполне вероятно, что пользователи могут создавать, читать, обновлять или удалять эти ресурсы.

Из-за этого распространенного варианта использования маршрутизация ресурсов __Laravel__ назначает типичные маршруты создания, чтения, обновления и удаления `CRUD` контроллеру с помощью одной строки кода. Для начала мы можем использовать опцию `make:controller` а потом  команду `--resource` в конце, чтобы быстро создать __контроллер для обработки этих действий__:

```
php artisan make:controller NameController --resource
```

Эта команда сгенерирует контроллер в `app/Http/Controllers/PhotoController.php`. Контроллер будет содержать метод для каждой из доступных операций с ресурсами. Затем вы можете зарегистрировать ресурсный маршрут, который указывает на контроллер:


```
use App\Http\Controllers\PhotoController;
 
Route::resource('photos', PhotoController::class);
```

Вы даже можете зарегистрировать сразу несколько контроллеров ресурсов, передав методу массив `resources`

```
Route::resources([
    'photos' => PhotoController::class,
    'posts' => PostController::class,
]);
```

___Действия, выполняемые контроллером ресурсов:___

| Метода запроса | URI | Функиция контроллера | Название route |
| -------------- | --- | -------------------- | -------------- |
| `GET` | `/photos` | _index_ | _photos.index_ |
| `GET` | `/photos/create` | _create_ | _photos.create_ |
| `POST` | `/photos` | _store_ | _photos.store_ |
| `GET` | `/photos/{photo}` | _show_ | _photos.show_ |
| `GET` | `/photos/{photo}/edit` | _edit_ | _photos.edit_ |
| `PUT/PATCH` | `/photos/{photo}` | _update_ | _photos.update_ |
| `DELETE` | `/photos/{photo}` | _destroy_ | _photos.destroy_ |

Помните, что вы всегда можете получить краткий обзор маршрутов вашего приложения, выполнив `route:list` команду Artisan.

```
php artisan route:list
```

___Пример резултата:___

Methods | Routes
------- | ------ |
`GET|HEAD/`   | movies.index › MoviesController@index |
`POST`        | _ignition/execute-solution | ignition.executeSolution › Spatie\LaravelIgnition › ExecuteSolutionController
`GET|HEAD`    | _ignition/health-check | ignition.healthCheck › Spatie\LaravelIgnition › HealthCheckController
`POST`        | _ignition/update-config | ignition.updateConfig › Spatie\LaravelIgnition › UpdateConfigController
`GET|HEAD`    | api/user | generated::fvRQHk9WTpY4i4fX
`GET|HEAD`    | movies/{movie} | movies.show › MoviesController@show
`GET|HEAD`    | sanctum/csrf-cookie | sanctum.csrf-cookie › Laravel\Sanctum › CsrfCookieController@show



