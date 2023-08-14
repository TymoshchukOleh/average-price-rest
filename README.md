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

| paramName  | Value  |        comment |
|:-----------|:------:|---------------:|
| categoryId | number | Тип транспорту |
| brandId         | number |          Марка |
| modelId         | number |         Модель |
| bodyId         | number |          Кузов |
| gearBoxId         | number |        Коробка |
| fuelId          | number |        Тип палива |
| driveId         | number |         Привід |
| colorId         | number |          Колір |
| stateId         | number |        Область |
| generationId         | number |      Покоління |
| modificationId         | number |    Модифікація |
| engineVolume         | Object |  Об'єм двигуна |
| year         | Object |            Рік |
| mileage         | Object |         Пробіг |

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
