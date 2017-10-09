## <a name="azure-dns"></a><span data-ttu-id="818d2-101">Azure DNS</span><span class="sxs-lookup"><span data-stu-id="818d2-101">Azure DNS</span></span>
<span data-ttu-id="818d2-102">Azure DNS является службой размещения для доменов DNS, предоставляющей разрешение имен с помощью инфраструктуры Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="818d2-102">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span>

| <span data-ttu-id="818d2-103">Свойство</span><span class="sxs-lookup"><span data-stu-id="818d2-103">Property</span></span> | <span data-ttu-id="818d2-104">Описание</span><span class="sxs-lookup"><span data-stu-id="818d2-104">Description</span></span> | <span data-ttu-id="818d2-105">Образец значения</span><span class="sxs-lookup"><span data-stu-id="818d2-105">Sample Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="818d2-106">**DNSzones**</span><span class="sxs-lookup"><span data-stu-id="818d2-106">**DNSzones**</span></span> |<span data-ttu-id="818d2-107">Домен зоны сведения toohost записи DNS определенного домена</span><span class="sxs-lookup"><span data-stu-id="818d2-107">Domain zone information toohost DNS records of a particular domain</span></span> |<span data-ttu-id="818d2-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span><span class="sxs-lookup"><span data-stu-id="818d2-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span></span> |

### <a name="dns-record-sets"></a><span data-ttu-id="818d2-109">Наборы записей DNS</span><span class="sxs-lookup"><span data-stu-id="818d2-109">DNS record sets</span></span>
<span data-ttu-id="818d2-110">Зоны DNS имеют дочерний объект, называемый набором записей.</span><span class="sxs-lookup"><span data-stu-id="818d2-110">DNS zones have a child object named record set.</span></span> <span data-ttu-id="818d2-111">Наборы записей представляют собой упорядоченную по типу коллекцию записей узла для зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="818d2-111">Record sets are a collection of host records by type for a DNS zone.</span></span> <span data-ttu-id="818d2-112">Типы записей: A, AAAA, CNAME, MX, NS, SOA, SRV и TXT.</span><span class="sxs-lookup"><span data-stu-id="818d2-112">Record types are A, AAAA, CNAME, MX, NS, SOA,SRV and TXT.</span></span>

| <span data-ttu-id="818d2-113">Свойство</span><span class="sxs-lookup"><span data-stu-id="818d2-113">Property</span></span> | <span data-ttu-id="818d2-114">Описание</span><span class="sxs-lookup"><span data-stu-id="818d2-114">Description</span></span> | <span data-ttu-id="818d2-115">Образец значения</span><span class="sxs-lookup"><span data-stu-id="818d2-115">Sample value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="818d2-116">Файл ,</span><span class="sxs-lookup"><span data-stu-id="818d2-116">A</span></span> |<span data-ttu-id="818d2-117">Тип записи IPv4</span><span class="sxs-lookup"><span data-stu-id="818d2-117">IPv4 record type</span></span> |<span data-ttu-id="818d2-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span><span class="sxs-lookup"><span data-stu-id="818d2-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span></span> |
| <span data-ttu-id="818d2-119">AAAA</span><span class="sxs-lookup"><span data-stu-id="818d2-119">AAAA</span></span> |<span data-ttu-id="818d2-120">Тип записи IPv6</span><span class="sxs-lookup"><span data-stu-id="818d2-120">IPv6 record type</span></span> |<span data-ttu-id="818d2-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span><span class="sxs-lookup"><span data-stu-id="818d2-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span></span> |
| <span data-ttu-id="818d2-122">CNAME</span><span class="sxs-lookup"><span data-stu-id="818d2-122">CNAME</span></span> |<span data-ttu-id="818d2-123">Тип записи канонического имени <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="818d2-123">canonical name record type <sup>1</sup></span></span> |<span data-ttu-id="818d2-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span><span class="sxs-lookup"><span data-stu-id="818d2-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span></span> |
| <span data-ttu-id="818d2-125">MX</span><span class="sxs-lookup"><span data-stu-id="818d2-125">MX</span></span> |<span data-ttu-id="818d2-126">Тип записи почты</span><span class="sxs-lookup"><span data-stu-id="818d2-126">mail record type</span></span> |<span data-ttu-id="818d2-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span><span class="sxs-lookup"><span data-stu-id="818d2-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span></span> |
| <span data-ttu-id="818d2-128">NS</span><span class="sxs-lookup"><span data-stu-id="818d2-128">NS</span></span> |<span data-ttu-id="818d2-129">Тип записи имени сервера</span><span class="sxs-lookup"><span data-stu-id="818d2-129">name server record type</span></span> |<span data-ttu-id="818d2-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span><span class="sxs-lookup"><span data-stu-id="818d2-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span></span> |
| <span data-ttu-id="818d2-131">SOA</span><span class="sxs-lookup"><span data-stu-id="818d2-131">SOA</span></span> |<span data-ttu-id="818d2-132">Тип записи SOA (начальная запись зоны) <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="818d2-132">Start of Authority record type <sup>2</sup></span></span> |<span data-ttu-id="818d2-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span><span class="sxs-lookup"><span data-stu-id="818d2-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span></span> |
| <span data-ttu-id="818d2-134">SRV</span><span class="sxs-lookup"><span data-stu-id="818d2-134">SRV</span></span> |<span data-ttu-id="818d2-135">Тип записи службы</span><span class="sxs-lookup"><span data-stu-id="818d2-135">service record type</span></span> |<span data-ttu-id="818d2-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span><span class="sxs-lookup"><span data-stu-id="818d2-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span></span> |

<span data-ttu-id="818d2-137"><sup>1</sup> допускает только одно значение на каждый набор записей.</span><span class="sxs-lookup"><span data-stu-id="818d2-137"><sup>1</sup> only allows one value per record set.</span></span>

<span data-ttu-id="818d2-138"><sup>2</sup> допускает только один тип записи SOA на каждую зону DNS.</span><span class="sxs-lookup"><span data-stu-id="818d2-138"><sup>2</sup> only allows one record type SOA per DNS zone.</span></span> 

<span data-ttu-id="818d2-139">Пример зоны DNS в формате Json:</span><span class="sxs-lookup"><span data-stu-id="818d2-139">Sample of DNS zone in Json format:</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "newZoneName": {
          "type": "String",
          "metadata": {
              "description": "hello name of hello DNS zone toobe created."
          }
        },
        "newRecordName": {
          "type": "String",
          "defaultValue": "www",
          "metadata": {
              "description": "hello name of hello DNS record toobe created.  hello name is relative toohello zone, not hello FQDN."
          }
        }
      },
      "resources": 
      [
        {
          "type": "microsoft.network/dnszones",
          "name": "[parameters('newZoneName')]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": {
          }
        },
        {
          "type": "microsoft.network/dnszones/a",
          "name": "[concat(parameters('newZoneName'), concat('/', parameters('newRecordName')))]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": 
          {
            "TTL": 3600,
            "ARecords": 
            [
                {
                    "ipv4Address": "1.2.3.4"
                },
                {
                    "ipv4Address": "1.2.3.5"
                }
            ]
          },
          "dependsOn": [
            "[concat('Microsoft.Network/dnszones/', parameters('newZoneName'))]"
          ]
        }
          ]
    }

## <a name="additional-resources"></a><span data-ttu-id="818d2-140">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="818d2-140">Additional resources</span></span>
<span data-ttu-id="818d2-141">Чтение hello [документация по REST API для зон DNS ](https://msdn.microsoft.com/library/azure/mt130626.aspx) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="818d2-141">Read hello [REST API documentation for DNS zones ](https://msdn.microsoft.com/library/azure/mt130626.aspx) for more information.</span></span>

<span data-ttu-id="818d2-142">Чтение hello [документации REST API для наборов записей DNS](https://msdn.microsoft.com/library/azure/mt130627.aspx) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="818d2-142">Read hello [REST API documentation for DNS record sets](https://msdn.microsoft.com/library/azure/mt130627.aspx) for more information.</span></span>

