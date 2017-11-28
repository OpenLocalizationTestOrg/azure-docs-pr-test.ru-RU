
### <a name="cacheskuname"></a><span data-ttu-id="da089-101">Параметр cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="da089-101">cacheSKUName</span></span>
<span data-ttu-id="da089-102">Ценовая категория нового кэша Azure Redis.</span><span class="sxs-lookup"><span data-stu-id="da089-102">The pricing tier of the new Azure Redis Cache.</span></span>

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "The pricing tier of the new Azure Redis Cache."
      }
    },

<span data-ttu-id="da089-103">В шаблоне определены значения, допустимые для этого параметра (Basic и Standard). Если значение не указано, параметру назначается значение по умолчанию (Basic).</span><span class="sxs-lookup"><span data-stu-id="da089-103">The template defines the values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="da089-104">Уровень Basic предоставляет один узел с различными размерами (до 53 ГБ).</span><span class="sxs-lookup"><span data-stu-id="da089-104">Basic provides a single node with multiple sizes available up to 53 GB.</span></span>
<span data-ttu-id="da089-105">Уровень Standard предоставляет два узла (основной и реплика) с различными размерами (до 53 ГБ) и соглашением об уровне обслуживания 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="da089-105">Standard provides two-node Primary/Replica with multiple sizes available up to 53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="da089-106">Параметр cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="da089-106">cacheSKUFamily</span></span>
<span data-ttu-id="da089-107">Семейство для SKU.</span><span class="sxs-lookup"><span data-stu-id="da089-107">The family for the sku.</span></span>

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "The family for the sku."
      }
    },


### <a name="cacheskucapacity"></a><span data-ttu-id="da089-108">Параметр cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="da089-108">cacheSKUCapacity</span></span>
<span data-ttu-id="da089-109">Размер нового экземпляра кэша Azure Redis.</span><span class="sxs-lookup"><span data-stu-id="da089-109">The size of the new Azure Redis Cache instance.</span></span> 

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
        "description": "The size of the new Azure Redis Cache instance. "
      }
    }


<span data-ttu-id="da089-110">В шаблоне определены значения, допустимые для этого параметра (0, 1, 2, 3, 4, 5 или 6). Если значение не указано, параметру назначается значение по умолчанию (1).</span><span class="sxs-lookup"><span data-stu-id="da089-110">The template defines the values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="da089-111">Эти числа соответствуют следующим размерам кэша: 0 = 250 МБ, 1 = 1 ГБ, 2 = 2,5 ГБ, 3 = 6 ГБ, 4 = 13 ГБ, 5 = 26 ГБ, 6 = 53 ГБ</span><span class="sxs-lookup"><span data-stu-id="da089-111">Those numbers correspond to following cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

