# @application/average-price

# REST API

Зі всіма айді можна ознайомитись тут (тип транспорту, марка, модель, кузов і тд) за посиланням нижче
https://api-docs-v2.readthedocs.io/ru/latest/auto_ria/used_cars/options/index.html

Документація для роботи з сервісом розрахунку ціни автомобіля

## Отримати середню ціну по унікальному ідентифікатору (omniId)

### omniId - VIN або держномер або айді оголошення

### onlyValue - лише значення, без данних для побудови графіка

### Request

`GET /average/omniId/`

    curl -i -H 'Accept: application/json' 'https://auto.ria.com/rest/average-price/public/average/omniId?omniId=34746079'

### Response

    HTTP/2 200
    server: openresty
    date: Fri, 11 Aug 2023 11:17:41 GMT
    content-type: application/json; charset=utf-8
    content-length: 123
    x-ria-service-version: 1.0.0
    x-ria-service-name: @application/average-price
    x-content-type-options: nosniff

    {
        "value":9597,
        "points":[
                    {"median_price":9197,"active_date":"2021-12-31"},
                    {"median_price":9250,"active_date":"2022-01-01"}
                 ]
    }

## onlyValue

    curl -i -H 'Accept: application/json' 'https://auto.ria.com/rest/average-price/public/average/omniId?omniId=34746079&onlyValue=1'

### Response

    HTTP/2 200
    server: openresty
    date: Fri, 11 Aug 2023 11:17:41 GMT
    content-type: application/json; charset=utf-8
    content-length: 15
    x-ria-service-version: 1.0.0
    x-ria-service-name: @application/average-price
    x-content-type-options: nosniff

    {
        "value": 9597
    }

### Request

`GET /average/params/`

    curl -i -H 'Accept: application/json' 'https://auto.ria.com/rest/average-price/public/average/params?categoryId=1'

### queryParams

| paramName       | Value  |           comment |
|:----------------|:------:|------------------:|
| categoryId      | number |    Тип транспорту |
| brandId         | number |             Марка |
| modelId         | number |            Модель |
| bodyId          | number |             Кузов |
| gearBoxId       | number |           Коробка |
| fuelId          | number |        Тип палива |
| driveId         | number |            Привід |
| colorId         | number |             Колір |
| stateId         | number |           Область |
| generationId    | number |         Покоління |
| modificationId  | number |       Модифікація |
| engineVolumeGTE | number | Об'єм двигуна від |
| engineVolumeLTE | number |  Об'єм двигуна до |
| yearGTE         | number |           Рік від |
| yearLTE         | number |            Рік до |
| mileageGTE      | number |        Пробіг від |
| mileageLTE      | number |         Пробіг до |

### Response

    HTTP/2 200
    server: openresty
    date: Fri, 11 Aug 2023 11:17:41 GMT
    content-type: application/json; charset=utf-8
    content-length: 123
    x-ria-service-version: 1.0.0
    x-ria-service-name: @application/average-price
    x-content-type-options: nosniff

    {
        "value":9597,
        "points":[
                    {"median_price":9197,"active_date":"2021-12-31"},
                    {"median_price":9250,"active_date":"2022-01-01"}
                 ]
    }

### Request

`POST /average/omniId`

    curl -i -H 'Accept: application/json' POST 'https://auto.ria.com/rest/average-price/public/average/omniId' -d 'omniId=ab9999it'

### Response

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8
    X-Ria-Service-Version: 1.0.0
    X-Ria-Service-Name: @application/average-price
    Content-Length: 123
    Date: Fri, 11 Aug 2023 13:56:12 GMT
    Connection: keep-alive
    Keep-Alive: timeout=5

    {"value":27625,"points":[{"median_price":26862,"active_date":"2021-12-31"},{"median_price":24544,"active_date":"2022-01-01"}]}

### Request

`POST /average/params`

    curl -i -H 'Accept: application/json' POST 'https://auto.ria.com/rest/average-price/public/average/params' -d 'categoryId=1'

### Params

| paramName      | Value  |        comment |
|:---------------|:------:|---------------:|
| categoryId     | number | Тип транспорту |
| brandId        | number |          Марка |
| modelId        | number |         Модель |
| bodyId         | number |          Кузов |
| gearBoxId      | number |        Коробка |
| fuelId         | number |     Тип палива |
| driveId        | number |         Привід |
| colorId        | number |          Колір |
| stateId        | number |        Область |
| generationId   | number |      Покоління |
| modificationId | number |    Модифікація |
| engineVolume   | Object |  Об'єм двигуна |
| year           | Object |            Рік |
| mileage        | Object |         Пробіг |

    engineVolume, year, mileage Потрібно передавати у форматі об'єкта з полями gte, lte

### Приклад

```json
{
  "categoryId": "1",
  "brandId": "6",
  "modelId": "1943",
  "year": {
    "gte": "2010",
    "lte": "2020"
  },
  "bodyId": "5",
  "mileage": {
    "gte": "100",
    "lte": "200"
  },
  "fuelId": "1",
  "engineVolume": {
    "gte": "1",
    "lte": "2"
  },
  "gearBoxId": "2",
  "driveId": "1",
  "colorId": "2"
}
```

### Response

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8
    X-Ria-Service-Version: 1.0.0
    X-Ria-Service-Name: @application/average-price
    Content-Length: 123
    Date: Fri, 11 Aug 2023 13:56:12 GMT
    Connection: keep-alive
    Keep-Alive: timeout=5

    {
        "value":9597,
        "points":[
                    {"median_price":9197,"active_date":"2021-12-31"},
                    {"median_price":9250,"active_date":"2022-01-01"}
                 ]
    }

# Підрахунок середньої ціни автомобіля за параметрами, які присутні на формі додавання оголошення

### Request

`POST /average/params/addForm`

        curl --location --request POST 'https://auto.ria.com/rest/average-price/public/average/params/addForm?onlyValue=1' \
--header 'Content-Type: application/json' \
--data-raw '{
    "params": {
        "main_category": 1,
        "marka_id": 9,
        "model_id": 96,
        "body_id": 5,
        "fuel_id": 1,
        "engineVolume": 3,
        "gear_id": 2,
        "drive_id": 1,
        "color_id": 3,
        "state_id": 18,
        "generation_id": 5836,
        "modification_id": 134539,
        "year": 2022,
        "raceInt": 12,
        "power": 340,
        "fuel_consumption_city": 5,
        "fuel_consumption_combine": 7,
        "fuel_consumption_route": 6,
        "seats": 5,
        "door": 5,
        "metallic": 1,
        "equip_id": 212140,
        "city_id": 50,
        "paintConditionId": 1,
        "technicalConditionId": 1,
        "headlightId": 3,
        "interiorMaterialId": 2,
        "interiorColorId": 1,
        "seatAdjustmentId": 2,
        "seatVentilationId": 2,
        "seatHeatedId": 1,
        "memorySeatModuleId": 1,
        "windowLifterId": 1,
        "conditionerTypeId": 2,
        "powerSteeringId": 2,
        "steeringWheelAdjustmentId": 1,
        "spareWheelId": 1,
        "matched_country": 756
    },
    "options": [
        {
            "optionId": 188
        },
        {
            "optionId": 610
        },
        {
            "optionId": 255
        },
        {
            "optionId": 629
        },
        {
            "optionId": 525
        },
        {
            "optionId": 605
        },
        {
            "optionId": 132
        },
        {
            "optionId": 555
        },
        {
            "optionId": 575
        },
        {
            "optionId": 574
        },
        {
            "optionId": 486
        },
        {
            "optionId": 437
        },
        {
            "optionId": 441
        },
        {
            "optionId": 602
        },
        {
            "optionId": 217
        },
        {
            "optionId": 608
        },
        {
            "optionId": 626
        }
    ]
}'

### Response

        {
            "value": 83252,
            "points": [
                {
                    "median_price": 73713.18616101811,
                    "active_date": "2022-04-26"
                },
                {
                    "median_price": 73713.18616101811,
                    "active_date": "2022-04-27"
                }
                ...
            ]
        }

### Add form params

| paramName                 | Value  |                                        comment |
|:--------------------------|:------:|-----------------------------------------------:|
| main_category             | number |                                 Тип транспорту |
| marka_id                  | number |                                          Марка |
| model_id                  | number |                                         Модель |
| body_id                   | number |                                          Кузов |
| gear_id                   | number |                                        Коробка |
| fuel_id                   | number |                                     Тип палива |
| drive_id                  | number |                                         Привід |
| color_id                  | number |                                          Колір |
| state_id                  | number |                                        Область |
| generation_id             | number |                                      Покоління |
| modification_id           | number |                                    Модифікація |
| engineVolume              | number |                                  Об'єм двигуна |
| year                      | number |                                            Рік |
| raceInt                   | number |                                         Пробіг |
| power                     | number |                             Потужність двигуна |
| power_name                | number |                            Величина потужності |
| wheel_formula             | number |                                Колісна формула |
| accumulatorCapacity       | number |                            Ємність акумулятора |
| fuel_consumption_city     | number |                       Витрата пального - місто |
| fuel_consumption_combine  | number |                    Витрата пального - змішаний |
| fuel_consumption_route    | number |                        Витрата пального - шосе |
| axle                      | number |                                 Кількість осей |
| seats                     | number |                                Кількість місць |
| door                      | number |                               Кількість дверей |
| metallic                  | number |                  Модифікація кольору - металік |
| equip_id                  | number |                     Ідентифікатор комплектації |
| city_id                   | number |              	Ідентифікатор міста продажу авто |
| damage                    | number |                                   Участь в ДТП |
| VIN                       | number |                       чи вказаний VIN-код авто |
| plateNumber               | number |                    чи вказаний Держ.номер авто |
| paintConditionId          | number |                           Лакофарбове покриття |
| technicalConditionId      | number |                                 Технічний стан |
| headlightId               | number |                                           Фари |
| interiorMaterialId        | number |                               Матеріали салону |
| interiorColorId           | number |                                   Колір салону |
| seatAdjustmentId          | number |            Регулювання сидінь салону по висоті |
| seatVentilationId         | number |                              Вентиляція сидінь |
| seatHeatedId              | number |                                Підігрів сидінь |
| memorySeatModuleId        | number |                      Пам'ять положення сидіння |
| windowLifterId            | number |                          Електросклопідйомники |
| conditionerTypeId         | number |                                    Кондиціонер |
| powerSteeringId           | number |                               Підсилювач керма |
| steeringWheelAdjustmentId | number |                              Регулювання керма |
| spareWheelId              | number |                                 Запасне колесо |
| custom                    | number |                                  Нерозмитнений |
| onRepairParts             | number |                         Повністю на запчастини |
| is_new                    | number |                                Нове оголошення |
| abroad                    | number |                              Чи авто в Україні |
| is_exchange               | number |                                 Можливий обмін |
| exchangeTypeId            | number |                      Ідентифікатор типу обміну |
| confiscated_car           | number |                      Чи авто було конфісковане |
| matched_country           | number |           Ідентифікатор країни з якої пригнана |
| zsu                       | number |                                Для ЗСУ дешевше |
| notInterested             | number | Не зацікавлений в дзвінках від автобізнесменів |
| installment               | number |                       Можлива оплата частинами |
| carrying                  | number |                             Вантажопідйомність |
| auctionPossible           | number |                                  Можливий торг |

### Add form options

| optionId                                    | comment |
|:--------------------------------------------|:-------:|
| Шкіряний салон  	                           |   125   |
| Люк	                                        |   132   |	
| Центральний замок	                          |   137   |	
| Бортовий комп'ютер	                         |   188   | 
| Парктронік передній	                        |   192   |
| Водія	                                      |   211   |
| Антиблокувальна система (ABS)	              |   217   |	
| Газобалонне обладнання (ГБО)	               |   246   |	
| Датчик дощу	                                |   255   |	
| Акустика	                                   |   258   |
| Сигналізація	                               |   303   |
| Навігаційна система	                        |   355   |
| Датчик світла	                              |   437   |
| Омивач фар	                                 |   441   |
| Посилена підвіска	                          |   442   |
| Підігрів дзеркал	                           |   443   |
| Система стабілізації (ESP)	                 |   459   |
| Тюнінг	                                     |   475   |
| Гаражне зберігання	                         |   477   |
| Сервісна книжка	                            |   484   |
| Тоновані вікна	                             |   486   |
| Перший власник	                             |   496   |
| Перша реєстрація	                           |   501   |
| Ручне керування для людей з інвалідністю	   |   502   |
| Броньований кузов	                          |   515   |
| Обігрів керма	                              |   524   |
| Запуск двигуна з кнопки	                    |   525   |
| Пандус для людей з інвалідністю	            |   526   |
| Денні ходові вогні	                         |   527   |
| Протитуманні фари	                          |   528   |
| Система адаптивного освітлення	             |   531   |
| Система управління дальнім світлом	         |   532   |
| Аудіопідготовка	                            |   534   |
| Мультимедіа система з LCD-екраном	          |   536   |
| AUX	                                        |   538   |
| Bluetooth	                                  |   539   |
| USB	                                        |   540   |
| Система мультимедіа для задніх пасажирів	   |   541   |
| Голосове керування	                         |   543   |
| Android Auto	                               |   544   |
| CarPlay	                                    |   545   |
| Бездротова зарядка для смартфону	           |   546   |
| Складане заднє сидіння	                     |   548   |
| Функція складання спинки сидіння пасажира	  |   549   |
| Третій задній підголівник	                  |   550   |
| Третій ряд сидінь	                          |   551   |
| Довга база	                                 |   552   |
| Кузов MAXI	                                 |   553   |
| Складний столик на спинках передніх сидінь	 |   554   |
| Оздоблення керма шкірою	                    |   555   |
| Оздоблення шкірою важеля КПП	               |   556   |
| Панорамний дах / Лобове скло	               |   558   |
| Оздоблення стелі чорного кольору	           |   559   |
| Передній центральний підлокітник	           |   560   |
| Сонцезахисні шторки в задніх дверях	        |   563   |
| Декоративне підсвічування салону	           |   564   |
| Декоративні накладки на педалі	             |   565   |
| Накладки на пороги	                         |   566   |
| Розетка 220V	                               |   567   |
| Розетка 12V	                                |   568   |
| Захист картера	                             |   569   |
| Захист коробки	                             |   570   |
| Фаркоп	                                     |   571   |
| Система доступу без ключа	                  |   572   |
| Система «старт-стоп»	                       |   574   |
| Проекційний дисплей	                        |   575   |
| Електрорегулювання керма	                   |   576   |
| Кермо з пам'яттю положення	                 |   577   |
| Мультифункціональне кермо	                  |   579   |
| Підрульові пелюстки перемикання передач	    |   580   |
| Сидіння з масажем	                          |   581   |
| Відкриття багажника без допомоги рук	       |   582   |
| Електропривід дзеркал	                      |   583   |
| Електроскладання дзеркал	                   |   584   |
| Бардачок з охолодженням	                    |   585   |
| Регульований педальний вузол	               |   586   |
| Доводчик дверей	                            |   587   |
| Підкурювач і попільничка	                   |   588   |
| Обігрів лобового скла	                      |   589   |
| Холодильник	                                |   590   |
| Адаптивний круїз	                           |   591   |
| Пневмопідвіска	                             |   592   |
| Електронна приладова панель	                |   594   |
| Дистанційний запуск двигуна	                |   595   |
| Автономний обігрівач webasto	               |   596   |
| Швидка зарядка CHAdeMO	                     |   597   |
| Парктронік задній	                          |   598   |
| Система автоматичного паркування	           |   599   |
| Передня камера	                             |   601   |
| Задня камера	                               |   602   |
| Камера 360	                                 |   603   |
| Імобілайзер	                                |   604   |
| Круїз контроль	                             |   605   |
| Антипробуксовочна система (ASR)	            |   606   |
| Стабілізація рульового управління (VSM)	    |   607   |
| Розподіл гальмівних зусиль (BAS, EBD)	      |   608   |
| Допомога при старті в гору	                 |   609   |
| Вибір режиму руху	                          |   610   |
| Допомога при спуску	                        |   611   |
| Запобігання зіткнення	                      |   612   |
| Контроль сліпих зон	                        |   615   |
| Контроль за смугою руху	                    |   616   |
| Датчик втоми водія	                         |   617   |
| Розпізнавання дорожніх знаків	              |   618   |
| Нічне бачення	                              |   619   |
| Датчик тиску в шинах	                       |   620   |
| Система кріплення IsoFix	                   |   621   |
| Блокування замків задніх дверей	            |   622   |
| Датчик проникнення в салон (датчик об`єму)	 |   623   |
| Пасажира	                                   |   624   |
| Бічні передні	                              |   625   |
| Бічні задні	                                |   626   |
| Віконні (шторки)	                           |   627   |
| Колін водія	                                |   628   |
| Електропривід кришки багажника	             |   629   |
| Авто в кредиті	                             |   630   |
| Сонцезахисна шторка на задньому склі	       |   631   |
| Керування жестами	                          |   632   |
| MirrorLink	                                 |   633   |
| Центральна подушка між водієм та пасажиром	 |   634   |
| Багажник на дах	                            |   635   |
| Лебідка	                                    |   636   |
| Шноркель	                                   |   637   |
| Ліфтована підвіска	                         |   638   |
