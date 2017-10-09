
### <a name="cacheskuname"></a>Параметр cacheSKUName
Hello ценовую категорию hello кэша redis для Azure — новый.

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "hello pricing tier of hello new Azure Redis Cache."
      }
    },

шаблон Hello определяет hello значения, которые являются допустимыми для этого параметра (Basic или Standard) и назначает значение по умолчанию (Basic), если значение не указано. Basic предоставляет отдельным узлом, имеющим несколько размеров, доступных too53 Гбайт.
Стандарт предоставляет первичный/реплика двух узлов с несколько размеров, доступных вверх too53 ГБ и 99,9% SLA.

### <a name="cacheskufamily"></a>Параметр cacheSKUFamily
Hello семейства для номера sku hello.

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "hello family for hello sku."
      }
    },


### <a name="cacheskucapacity"></a>Параметр cacheSKUCapacity
размер Hello hello новый экземпляр кэша Redis для Azure. 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "hello size of hello new Azure Redis Cache instance. "
      }
    }


шаблон Hello определяет hello значения, разрешенные для этого параметра (0, 1, 2, 3, 4, 5 или 6) и назначает значение по умолчанию (1), если значение не указано. Эти числа соответствуют toofollowing объем кэш-памяти: 0 = 250 МБ, 1 = 1 ГБ, 2 = 2,5 ГБ, 3 = 6 ГБ, 4 = 13 ГБ, 5 = 26 ГБ, 6 = 53 ГБ

