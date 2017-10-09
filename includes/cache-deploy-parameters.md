
### <a name="cacheskuname"></a><span data-ttu-id="69480-101">Параметр cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="69480-101">cacheSKUName</span></span>
<span data-ttu-id="69480-102">Hello ценовую категорию hello кэша redis для Azure — новый.</span><span class="sxs-lookup"><span data-stu-id="69480-102">hello pricing tier of hello new Azure Redis Cache.</span></span>

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

<span data-ttu-id="69480-103">шаблон Hello определяет hello значения, которые являются допустимыми для этого параметра (Basic или Standard) и назначает значение по умолчанию (Basic), если значение не указано.</span><span class="sxs-lookup"><span data-stu-id="69480-103">hello template defines hello values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="69480-104">Basic предоставляет отдельным узлом, имеющим несколько размеров, доступных too53 Гбайт.</span><span class="sxs-lookup"><span data-stu-id="69480-104">Basic provides a single node with multiple sizes available up too53 GB.</span></span>
<span data-ttu-id="69480-105">Стандарт предоставляет первичный/реплика двух узлов с несколько размеров, доступных вверх too53 ГБ и 99,9% SLA.</span><span class="sxs-lookup"><span data-stu-id="69480-105">Standard provides two-node Primary/Replica with multiple sizes available up too53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="69480-106">Параметр cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="69480-106">cacheSKUFamily</span></span>
<span data-ttu-id="69480-107">Hello семейства для номера sku hello.</span><span class="sxs-lookup"><span data-stu-id="69480-107">hello family for hello sku.</span></span>

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


### <a name="cacheskucapacity"></a><span data-ttu-id="69480-108">Параметр cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="69480-108">cacheSKUCapacity</span></span>
<span data-ttu-id="69480-109">размер Hello hello новый экземпляр кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="69480-109">hello size of hello new Azure Redis Cache instance.</span></span> 

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


<span data-ttu-id="69480-110">шаблон Hello определяет hello значения, разрешенные для этого параметра (0, 1, 2, 3, 4, 5 или 6) и назначает значение по умолчанию (1), если значение не указано.</span><span class="sxs-lookup"><span data-stu-id="69480-110">hello template defines hello values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="69480-111">Эти числа соответствуют toofollowing объем кэш-памяти: 0 = 250 МБ, 1 = 1 ГБ, 2 = 2,5 ГБ, 3 = 6 ГБ, 4 = 13 ГБ, 5 = 26 ГБ, 6 = 53 ГБ</span><span class="sxs-lookup"><span data-stu-id="69480-111">Those numbers correspond toofollowing cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

