# @application/average-price

# REST API

Зі всіма айді можна ознайомитись тут (тип транспорту, марка, модель, кузов і тд) за посиланням нижче
https://api-docs-v2.readthedocs.io/ru/latest/auto_ria/used_cars/options/index.html

Документація для роботи з сервісом розрахунку ціни автомобіля

## Отримати мінімальну середню ціну по унікальному ідентифікатору (omniId)

### omniId - VIN або держномер або айді оголошення

### minAvgValue - мінімальна середня ціна автомобіля

### intervalType - тип інтервалу, за яким рахуємо (string: 'day', 'month', 'year), default: 'day'

### intervalNumber - значення інтервалу (integer), default: 365

### Request

`GET /average/omniId/`

    curl -i -H 'Accept: application/json' 'https://auto.ria.com/rest/average-price/public/average/omniId?omniId=JTEBU29JX05132444&minAvgValue=1&intervalType=day&intervalNumber=365'

### Response

    {
        "minAvgValue": 17053
        "advertisementData": { "categoryId": 1, ... }
    }

*advertisementData - інформація по знайденому оголошенню

### Request

`GET /average/params/`

    curl -i -H 'Accept: application/json' 'https://auto.ria.com/rest/average-price/public/average/params?categoryId=1&brandId=62&modelId=586&minAvgValue=1'

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

    {
        "minAvgValue": 17053
    }

### Request

`POST /average/omniId`

    curl -i -H 'Accept: application/json' POST 'https://auto.ria.com/rest/average-price/public/average/omniId?minAvgValue=1' -d 'omniId=ab9999it'

### Response

    {
        "minAvgValue": 17053
    }

### Request

`POST /average/params`

    curl --location --request POST 'https://auto.ria.com/rest/average-price/public/average/params?minAvgValue=1' -H "Content-Type: application/json" -d "{\"categoryId\": \"1\",\"brandId\": \"62\",\"modelId\": \"586\"}"

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

    {
        "minAvgValue": 17053
    }
