---
title: "Общие сведения об экземпляре метаданных службы aaaAzure | Документы Microsoft"
description: "Интерфейс rESTful tooget сведения о Виртуальных машин вычислительных, сети и предстоящем обслуживании события."
services: virtual-machines-windows, virtual-machines-linux,virtual-machines-scale-sets, cloud-services
documentationcenter: virtual-machines
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 03/27/2017
ms.author: harijay
ms.openlocfilehash: e87cdf28f80b9ef8cc566b637549c48846862f0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service"></a><span data-ttu-id="393d8-103">Служба метаданных экземпляров Azure</span><span class="sxs-lookup"><span data-stu-id="393d8-103">Azure Instance Metadata Service</span></span> 


<span data-ttu-id="393d8-104">Hello служба метаданных экземпляра Azure предоставляет сведения о выполнении экземпляров виртуальных машин, которые можно использовать toomanage и настроить виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="393d8-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="393d8-105">Сюда входят сведения о номере SKU, конфигурации сети и ближайших мероприятиях обслуживания.</span><span class="sxs-lookup"><span data-stu-id="393d8-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="393d8-106">Дополнительные сведения о том, какие сведения доступны, см. в разделе [Категории данных метаданных экземпляров](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="393d8-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="393d8-107">Служба метаданных экземпляра Azure является конечной точкой REST, доступный tooall ВМ IaaS, созданные при помощи hello [диспетчера ресурсов Azure](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="393d8-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="393d8-108">Hello конечная точка доступна по хорошо известных немаршрутизируемый IP-адрес (`169.254.169.254`), можно обратиться только из hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="393d8-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>

### <a name="important-information"></a><span data-ttu-id="393d8-109">Важные сведения</span><span class="sxs-lookup"><span data-stu-id="393d8-109">Important information</span></span>

<span data-ttu-id="393d8-110">Эта служба является **общедоступной** в глобальных регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="393d8-110">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="393d8-111">Она находится в общедоступной предварительной версии для государственных организаций, облачной службы Azure для Китая и Германии.</span><span class="sxs-lookup"><span data-stu-id="393d8-111">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="393d8-112">Регулярно, он получает обновления tooexpose новые сведения об экземплярах виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="393d8-112">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="393d8-113">Эта страница отражает hello актуальные [категории данных](#instance-metadata-data-categories) доступны.</span><span class="sxs-lookup"><span data-stu-id="393d8-113">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="393d8-114">Доступность службы</span><span class="sxs-lookup"><span data-stu-id="393d8-114">Service Availability</span></span>
<span data-ttu-id="393d8-115">Служба Hello доступна во всех регионах общедоступной глобального Azure.</span><span class="sxs-lookup"><span data-stu-id="393d8-115">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="393d8-116">Hello служба находится в общедоступной предварительной версии в регионах hello государственных организаций, Китай или Германии.</span><span class="sxs-lookup"><span data-stu-id="393d8-116">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="393d8-117">регионы</span><span class="sxs-lookup"><span data-stu-id="393d8-117">Regions</span></span>                                        | <span data-ttu-id="393d8-118">Доступность?</span><span class="sxs-lookup"><span data-stu-id="393d8-118">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="393d8-119">Все общедоступные глобальные регионы Azure</span><span class="sxs-lookup"><span data-stu-id="393d8-119">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/en-us/regions/)     | <span data-ttu-id="393d8-120">Общедоступная версия</span><span class="sxs-lookup"><span data-stu-id="393d8-120">Generally Available</span></span> 
[<span data-ttu-id="393d8-121">Azure для государственных организаций</span><span class="sxs-lookup"><span data-stu-id="393d8-121">Azure Government</span></span>](https://azure.microsoft.com/en-us/overview/clouds/government/)              | <span data-ttu-id="393d8-122">В предварительной версии</span><span class="sxs-lookup"><span data-stu-id="393d8-122">In Preview</span></span> 
[<span data-ttu-id="393d8-123">Azure для Китая</span><span class="sxs-lookup"><span data-stu-id="393d8-123">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="393d8-124">В предварительной версии</span><span class="sxs-lookup"><span data-stu-id="393d8-124">In Preview</span></span>
[<span data-ttu-id="393d8-125">Azure для Германии</span><span class="sxs-lookup"><span data-stu-id="393d8-125">Azure Germany</span></span>](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | <span data-ttu-id="393d8-126">В предварительной версии</span><span class="sxs-lookup"><span data-stu-id="393d8-126">In Preview</span></span>

<span data-ttu-id="393d8-127">Эта таблица обновляется, когда служба hello станет доступным в других облаках, Azure.</span><span class="sxs-lookup"><span data-stu-id="393d8-127">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="393d8-128">tootry out hello экземпляр метаданных службы, создайте виртуальную Машину из [диспетчера ресурсов Azure](https://docs.microsoft.com/rest/api/resources/) или hello [портал Azure](http://portal.azure.com) в hello выше области и выполните hello примеры ниже.</span><span class="sxs-lookup"><span data-stu-id="393d8-128">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="393d8-129">Использование</span><span class="sxs-lookup"><span data-stu-id="393d8-129">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="393d8-130">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="393d8-130">Versioning</span></span>
<span data-ttu-id="393d8-131">Hello метаданных экземпляра службы с версиями.</span><span class="sxs-lookup"><span data-stu-id="393d8-131">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="393d8-132">Версии являются обязательными, и текущая версия hello `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="393d8-132">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="393d8-133">Предыдущие выпуски Предварительный просмотр поддерживается {последние} в качестве hello api-version запланированные события.</span><span class="sxs-lookup"><span data-stu-id="393d8-133">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="393d8-134">Этот формат не поддерживается и будет считаться устаревшей в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="393d8-134">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="393d8-135">Так как мы добавляем новые версии, вы все еще можете получить доступ к предыдущим версиям для обеспечения совместимости, если используемый скрипт зависит от конкретных форматов данных.</span><span class="sxs-lookup"><span data-stu-id="393d8-135">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="393d8-136">Однако обратите внимание, что этой version(2017-03-01) hello текущего предварительного просмотра может оказаться недоступным после общедоступной службы hello.</span><span class="sxs-lookup"><span data-stu-id="393d8-136">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="393d8-137">Использование заголовков</span><span class="sxs-lookup"><span data-stu-id="393d8-137">Using Headers</span></span>
<span data-ttu-id="393d8-138">При запросе hello экземпляр метаданных службы, необходимо указать заголовок hello `Metadata: true` tooensure hello запрос не был перенаправлен непреднамеренно.</span><span class="sxs-lookup"><span data-stu-id="393d8-138">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="393d8-139">Получение метаданных</span><span class="sxs-lookup"><span data-stu-id="393d8-139">Retrieving metadata</span></span>

<span data-ttu-id="393d8-140">Используйте метаданные экземпляров для запуска виртуальных машин, созданных или управляемых с помощью [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="393d8-140">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="393d8-141">Доступ к все категории данных для экземпляра виртуальной машины с помощью hello, следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="393d8-141">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="393d8-142">Во всех запросах метаданных экземпляров учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="393d8-142">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="393d8-143">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="393d8-143">Data output</span></span>
<span data-ttu-id="393d8-144">По умолчанию hello метаданных экземпляра службы возвращает данные в формате JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="393d8-144">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="393d8-145">Однако при необходимости другие API-интерфейсы могут возвращать данные в различных форматах.</span><span class="sxs-lookup"><span data-stu-id="393d8-145">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="393d8-146">Hello Следующая таблица представляет ссылки из других форматов данных, которые API-интерфейсы могут поддерживать.</span><span class="sxs-lookup"><span data-stu-id="393d8-146">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="393d8-147">API</span><span class="sxs-lookup"><span data-stu-id="393d8-147">API</span></span> | <span data-ttu-id="393d8-148">Формат данных по умолчанию</span><span class="sxs-lookup"><span data-stu-id="393d8-148">Default Data Format</span></span> | <span data-ttu-id="393d8-149">Другие форматы</span><span class="sxs-lookup"><span data-stu-id="393d8-149">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="393d8-150">/instance</span><span class="sxs-lookup"><span data-stu-id="393d8-150">/instance</span></span> | <span data-ttu-id="393d8-151">json</span><span class="sxs-lookup"><span data-stu-id="393d8-151">json</span></span> | <span data-ttu-id="393d8-152">text</span><span class="sxs-lookup"><span data-stu-id="393d8-152">text</span></span>
<span data-ttu-id="393d8-153">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="393d8-153">/scheduledevents</span></span> | <span data-ttu-id="393d8-154">json</span><span class="sxs-lookup"><span data-stu-id="393d8-154">json</span></span> | <span data-ttu-id="393d8-155">Нет</span><span class="sxs-lookup"><span data-stu-id="393d8-155">none</span></span>

<span data-ttu-id="393d8-156">tooaccess формата ответа не по умолчанию, укажите запрошенный формат hello в качестве параметра строки запроса в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="393d8-156">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="393d8-157">Например:</span><span class="sxs-lookup"><span data-stu-id="393d8-157">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="393d8-158">Безопасность</span><span class="sxs-lookup"><span data-stu-id="393d8-158">Security</span></span>
<span data-ttu-id="393d8-159">Конечная точка службы метаданных экземпляра Hello доступна только из hello ОС немаршрутизируемый IP-адрес экземпляра виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="393d8-159">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="393d8-160">Кроме того, любой запрос с `X-Forwarded-For` заголовок, отклоняется службой hello.</span><span class="sxs-lookup"><span data-stu-id="393d8-160">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="393d8-161">Мы также требуется toocontain запросы `Metadata: true` tooensure заголовок, hello сам запрос непосредственно было предназначено и не является частью непреднамеренного перенаправления.</span><span class="sxs-lookup"><span data-stu-id="393d8-161">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="393d8-162">Ошибка</span><span class="sxs-lookup"><span data-stu-id="393d8-162">Error</span></span>
<span data-ttu-id="393d8-163">Если элемент данных не найден или имеет неправильный формат запроса hello метаданных экземпляра службы возвращает стандартные ошибки HTTP.</span><span class="sxs-lookup"><span data-stu-id="393d8-163">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="393d8-164">Например:</span><span class="sxs-lookup"><span data-stu-id="393d8-164">For example:</span></span>

<span data-ttu-id="393d8-165">Код состояния HTTP</span><span class="sxs-lookup"><span data-stu-id="393d8-165">HTTP Status Code</span></span> | <span data-ttu-id="393d8-166">Причина</span><span class="sxs-lookup"><span data-stu-id="393d8-166">Reason</span></span>
----------------|-------
<span data-ttu-id="393d8-167">200 ОК</span><span class="sxs-lookup"><span data-stu-id="393d8-167">200 OK</span></span> |
<span data-ttu-id="393d8-168">400 — недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="393d8-168">400 Bad Request</span></span> | <span data-ttu-id="393d8-169">Отсутствует заголовок `Metadata: true`</span><span class="sxs-lookup"><span data-stu-id="393d8-169">Missing `Metadata: true` header</span></span>
<span data-ttu-id="393d8-170">404 — не найдено</span><span class="sxs-lookup"><span data-stu-id="393d8-170">404 Not Found</span></span> | <span data-ttu-id="393d8-171">Hello does't запрошенный элемент существует</span><span class="sxs-lookup"><span data-stu-id="393d8-171">hello requested element does't exist</span></span> 
<span data-ttu-id="393d8-172">405 — недопустимый метод</span><span class="sxs-lookup"><span data-stu-id="393d8-172">405 Method Not Allowed</span></span> | <span data-ttu-id="393d8-173">Поддерживаются только запросы `GET` и `POST`</span><span class="sxs-lookup"><span data-stu-id="393d8-173">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="393d8-174">429 — слишком много запросов</span><span class="sxs-lookup"><span data-stu-id="393d8-174">429 Too Many Requests</span></span> | <span data-ttu-id="393d8-175">Hello API в настоящее время поддерживает не более 5 запросов в секунду</span><span class="sxs-lookup"><span data-stu-id="393d8-175">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="393d8-176">500 — ошибка службы</span><span class="sxs-lookup"><span data-stu-id="393d8-176">500 Service Error</span></span>     | <span data-ttu-id="393d8-177">Повторите попытку через некоторое время</span><span class="sxs-lookup"><span data-stu-id="393d8-177">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="393d8-178">Примеры</span><span class="sxs-lookup"><span data-stu-id="393d8-178">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="393d8-179">Все ответы API — это строки в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="393d8-179">All API responses are JSON strings.</span></span> <span data-ttu-id="393d8-180">Все следующие примеры ответов представлены в удобном для чтения формате.</span><span class="sxs-lookup"><span data-stu-id="393d8-180">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="393d8-181">Получение сведений о сети</span><span class="sxs-lookup"><span data-stu-id="393d8-181">Retrieving network information</span></span>

<span data-ttu-id="393d8-182">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="393d8-182">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="393d8-183">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="393d8-183">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="393d8-184">Hello ответа представляет собой строку JSON.</span><span class="sxs-lookup"><span data-stu-id="393d8-184">hello response is a JSON string.</span></span> <span data-ttu-id="393d8-185">Следующий пример ответа Hello, представленное для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="393d8-185">hello following example response is pretty-printed for readability.</span></span>

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="393d8-186">Получение общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="393d8-186">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="393d8-187">Получение всех метаданных для экземпляра</span><span class="sxs-lookup"><span data-stu-id="393d8-187">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="393d8-188">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="393d8-188">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="393d8-189">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="393d8-189">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="393d8-190">Hello ответа представляет собой строку JSON.</span><span class="sxs-lookup"><span data-stu-id="393d8-190">hello response is a JSON string.</span></span> <span data-ttu-id="393d8-191">Следующий пример ответа Hello, представленное для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="393d8-191">hello following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="393d8-192">Получение метаданных в виртуальной машине Windows</span><span class="sxs-lookup"><span data-stu-id="393d8-192">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="393d8-193">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="393d8-193">**Request**</span></span>

<span data-ttu-id="393d8-194">Можно получить метаданные экземпляра в Windows через PowerShell программа hello `curl`:</span><span class="sxs-lookup"><span data-stu-id="393d8-194">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="393d8-195">Или с помощью hello `Invoke-RestMethod` командлета:</span><span class="sxs-lookup"><span data-stu-id="393d8-195">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="393d8-196">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="393d8-196">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="393d8-197">Hello ответа представляет собой строку JSON.</span><span class="sxs-lookup"><span data-stu-id="393d8-197">hello response is a JSON string.</span></span> <span data-ttu-id="393d8-198">Следующий пример ответа Hello, представленное для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="393d8-198">hello following example response  is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="393d8-199">Категории данных метаданных экземпляров</span><span class="sxs-lookup"><span data-stu-id="393d8-199">Instance metadata data categories</span></span>
<span data-ttu-id="393d8-200">Привет, следующие категории данных доступны через hello экземпляр службы метаданных:</span><span class="sxs-lookup"><span data-stu-id="393d8-200">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="393d8-201">Данные</span><span class="sxs-lookup"><span data-stu-id="393d8-201">Data</span></span> | <span data-ttu-id="393d8-202">Описание</span><span class="sxs-lookup"><span data-stu-id="393d8-202">Description</span></span>
-----|------------
<span data-ttu-id="393d8-203">location</span><span class="sxs-lookup"><span data-stu-id="393d8-203">location</span></span> | <span data-ttu-id="393d8-204">Hello Azure области ВМ работает</span><span class="sxs-lookup"><span data-stu-id="393d8-204">Azure Region hello VM is running in</span></span>
<span data-ttu-id="393d8-205">name</span><span class="sxs-lookup"><span data-stu-id="393d8-205">name</span></span> | <span data-ttu-id="393d8-206">Имя виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="393d8-206">Name of hello VM</span></span> 
<span data-ttu-id="393d8-207">offer</span><span class="sxs-lookup"><span data-stu-id="393d8-207">offer</span></span> | <span data-ttu-id="393d8-208">Предоставляют сведения для hello образа виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="393d8-208">Offer information for hello VM image.</span></span> <span data-ttu-id="393d8-209">Это значение доступно только для образов, развернутых из коллекции образов Azure.</span><span class="sxs-lookup"><span data-stu-id="393d8-209">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="393d8-210">publisher</span><span class="sxs-lookup"><span data-stu-id="393d8-210">publisher</span></span> | <span data-ttu-id="393d8-211">Издатель образа ВМ hello</span><span class="sxs-lookup"><span data-stu-id="393d8-211">Publisher of hello VM image</span></span>
<span data-ttu-id="393d8-212">sku</span><span class="sxs-lookup"><span data-stu-id="393d8-212">sku</span></span> | <span data-ttu-id="393d8-213">Конфигурации для образа виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="393d8-213">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="393d8-214">версия</span><span class="sxs-lookup"><span data-stu-id="393d8-214">version</span></span> | <span data-ttu-id="393d8-215">Версия образа виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="393d8-215">Version of hello VM image</span></span> 
<span data-ttu-id="393d8-216">osType</span><span class="sxs-lookup"><span data-stu-id="393d8-216">osType</span></span> | <span data-ttu-id="393d8-217">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="393d8-217">Linux or Windows</span></span> 
<span data-ttu-id="393d8-218">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="393d8-218">platformUpdateDomain</span></span> |  <span data-ttu-id="393d8-219">[Домен обновления](virtual-machines-windows-manage-availability.md) hello в запущенной виртуальной Машине</span><span class="sxs-lookup"><span data-stu-id="393d8-219">[Update domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="393d8-220">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="393d8-220">platformFaultDomain</span></span> | <span data-ttu-id="393d8-221">[Домен сбоя](virtual-machines-windows-manage-availability.md) hello в запущенной виртуальной Машине</span><span class="sxs-lookup"><span data-stu-id="393d8-221">[Fault domain](virtual-machines-windows-manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="393d8-222">vmId</span><span class="sxs-lookup"><span data-stu-id="393d8-222">vmId</span></span> | <span data-ttu-id="393d8-223">[Уникальный идентификатор](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) для hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="393d8-223">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="393d8-224">vmSize</span><span class="sxs-lookup"><span data-stu-id="393d8-224">vmSize</span></span> | [<span data-ttu-id="393d8-225">Размер виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="393d8-225">VM size</span></span>](virtual-machines-windows-sizes.md)
<span data-ttu-id="393d8-226">ipv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="393d8-226">ipv4/privateIpAddress</span></span> | <span data-ttu-id="393d8-227">Локальный адрес IPv4 hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="393d8-227">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="393d8-228">ipv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="393d8-228">ipv4/publicIpAddress</span></span> | <span data-ttu-id="393d8-229">Общедоступный адрес IPv4 hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="393d8-229">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="393d8-230">subnet/address</span><span class="sxs-lookup"><span data-stu-id="393d8-230">subnet/address</span></span> | <span data-ttu-id="393d8-231">Адрес подсети hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="393d8-231">Subnet address of hello VM</span></span>
<span data-ttu-id="393d8-232">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="393d8-232">subnet/prefix</span></span> | <span data-ttu-id="393d8-233">Префикс подсети, пример 24</span><span class="sxs-lookup"><span data-stu-id="393d8-233">Subnet prefix, example 24</span></span>
<span data-ttu-id="393d8-234">ipv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="393d8-234">ipv6/ipAddress</span></span> | <span data-ttu-id="393d8-235">Локальный адрес IPv6 hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="393d8-235">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="393d8-236">macAddress</span><span class="sxs-lookup"><span data-stu-id="393d8-236">macAddress</span></span> | <span data-ttu-id="393d8-237">Mac-адрес виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="393d8-237">VM mac address</span></span> 
<span data-ttu-id="393d8-238">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="393d8-238">scheduledevents</span></span> | <span data-ttu-id="393d8-239">Сейчас в общедоступной предварительной версии. Дополнительные сведения см. в статье [Служба метаданных Azure. Запланированные события (предварительная версия)](virtual-machines-scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="393d8-239">Currently in Public Preview See [scheduledevents](virtual-machines-scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="393d8-240">Примеры сценариев использования</span><span class="sxs-lookup"><span data-stu-id="393d8-240">Example Scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="393d8-241">Отслеживание виртуальной машины в Azure</span><span class="sxs-lookup"><span data-stu-id="393d8-241">Tracking VM running on Azure</span></span>

<span data-ttu-id="393d8-242">Как поставщик услуг может потребоваться tootrack hello число работающих виртуальных машин программного обеспечения или агентами, которые должны tootrack уникальность hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="393d8-242">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="393d8-243">возможности tooget toobe уникальный идентификатор для виртуальной Машины, используйте hello `vmId` из метаданных службы экземпляра.</span><span class="sxs-lookup"><span data-stu-id="393d8-243">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="393d8-244">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="393d8-244">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="393d8-245">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="393d8-245">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="393d8-246">Размещение контейнеров и секций данных на основе домена сбоя или обновления</span><span class="sxs-lookup"><span data-stu-id="393d8-246">Placement of containers, data-partitions based Fault/Update domain</span></span> 

<span data-ttu-id="393d8-247">В некоторых сценариях размещение разных реплик имеет первостепенное значение.</span><span class="sxs-lookup"><span data-stu-id="393d8-247">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="393d8-248">Например [размещения реплики HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) или размещения контейнера через [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) может потребоваться tooknow hello `platformFaultDomain` и `platformUpdateDomain` hello, Виртуальная машина работает на.</span><span class="sxs-lookup"><span data-stu-id="393d8-248">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="393d8-249">Вы можете запрашивать эти данные напрямую через hello экземпляр метаданных службы.</span><span class="sxs-lookup"><span data-stu-id="393d8-249">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="393d8-250">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="393d8-250">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="393d8-251">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="393d8-251">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="393d8-252">Получение дополнительных сведений о hello виртуальной Машины во время службу технической поддержки Майкрософт</span><span class="sxs-lookup"><span data-stu-id="393d8-252">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="393d8-253">Как поставщик услуг то появляется поддержки по телефону куда tooknow Дополнительные сведения о hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="393d8-253">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="393d8-254">Запрос клиента tooshare hello hello вычислений метаданных может предоставить основные сведения для специалистов tooknow поддержки hello о hello типа ВМ в Azure.</span><span class="sxs-lookup"><span data-stu-id="393d8-254">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="393d8-255">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="393d8-255">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="393d8-256">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="393d8-256">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="393d8-257">Hello ответа представляет собой строку JSON.</span><span class="sxs-lookup"><span data-stu-id="393d8-257">hello response is a JSON string.</span></span> <span data-ttu-id="393d8-258">Следующий пример ответа Hello, представленное для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="393d8-258">hello following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="393d8-259">Примеры вызова метаданные службы с использованием различных языков внутри hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="393d8-259">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="393d8-260">Язык</span><span class="sxs-lookup"><span data-stu-id="393d8-260">Language</span></span> | <span data-ttu-id="393d8-261">Пример</span><span class="sxs-lookup"><span data-stu-id="393d8-261">Example</span></span> 
---------|----------------
<span data-ttu-id="393d8-262">Ruby</span><span class="sxs-lookup"><span data-stu-id="393d8-262">Ruby</span></span>     | <span data-ttu-id="393d8-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="393d8-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="393d8-264">Перейдите в локальную сеть</span><span class="sxs-lookup"><span data-stu-id="393d8-264">Go Lan</span></span>   | <span data-ttu-id="393d8-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="393d8-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="393d8-266">python</span><span class="sxs-lookup"><span data-stu-id="393d8-266">python</span></span>   | <span data-ttu-id="393d8-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="393d8-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="393d8-268">C++</span><span class="sxs-lookup"><span data-stu-id="393d8-268">C++</span></span>      | <span data-ttu-id="393d8-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="393d8-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="393d8-270">C#</span><span class="sxs-lookup"><span data-stu-id="393d8-270">C#</span></span>       | <span data-ttu-id="393d8-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="393d8-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="393d8-272">JavaScript</span><span class="sxs-lookup"><span data-stu-id="393d8-272">Javascript</span></span> | <span data-ttu-id="393d8-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="393d8-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="393d8-274">PowerShell</span><span class="sxs-lookup"><span data-stu-id="393d8-274">Powershell</span></span> | <span data-ttu-id="393d8-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="393d8-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="393d8-276">Bash</span><span class="sxs-lookup"><span data-stu-id="393d8-276">Bash</span></span>       | <span data-ttu-id="393d8-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="393d8-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="393d8-278">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="393d8-278">FAQ</span></span>
1. <span data-ttu-id="393d8-279">Я получаю hello ошибки `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="393d8-279">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="393d8-280">Что это означает?</span><span class="sxs-lookup"><span data-stu-id="393d8-280">What does this mean?</span></span>
   * <span data-ttu-id="393d8-281">Hello служба метаданных экземпляра требуется заголовок hello `Metadata: true` toobe переданный запрос hello.</span><span class="sxs-lookup"><span data-stu-id="393d8-281">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="393d8-282">Передача этого заголовка в вызове REST hello позволяет toohello доступ службы метаданных экземпляра.</span><span class="sxs-lookup"><span data-stu-id="393d8-282">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="393d8-283">Почему я не получаю сведения о вычислениях для виртуальной машины?</span><span class="sxs-lookup"><span data-stu-id="393d8-283">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="393d8-284">Hello экземпляр метаданных службы, в настоящее время поддерживает только экземпляры, созданные с помощью диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="393d8-284">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="393d8-285">В будущем hello Корпорация Майкрософт может расширить поддержку виртуальных машин облачной службы.</span><span class="sxs-lookup"><span data-stu-id="393d8-285">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="393d8-286">Виртуальная машина была недавно создана с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="393d8-286">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="393d8-287">Почему не отображаются сведения о метаданных вычислений?</span><span class="sxs-lookup"><span data-stu-id="393d8-287">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="393d8-288">Все виртуальные машины, созданные после сентября 2016, добавьте [тега](../azure-resource-manager/resource-group-using-tags.md) toostart просматривают метаданные вычислений.</span><span class="sxs-lookup"><span data-stu-id="393d8-288">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="393d8-289">Для более старых виртуальных машин (создан до сентября 2016) Добавление и удаление расширения или данных метаданных toorefresh дисков toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="393d8-289">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="393d8-290">Почему выдается ошибка hello `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="393d8-290">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="393d8-291">Повторите запрос в зависимости от экспоненциальной системы.</span><span class="sxs-lookup"><span data-stu-id="393d8-291">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="393d8-292">Если hello проблема повторится, обратитесь в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="393d8-292">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="393d8-293">Где можно задать дополнительные вопросы или оставить комментарии?</span><span class="sxs-lookup"><span data-stu-id="393d8-293">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="393d8-294">Оставьте комментарии на сайте http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="393d8-294">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="393d8-295">Будет ли это работать для экземпляра масштабируемого набора виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="393d8-295">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="393d8-296">Да, служба метаданных доступна для экземпляров масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="393d8-296">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="393d8-297">Получение поддержки для службы hello</span><span class="sxs-lookup"><span data-stu-id="393d8-297">How do I get support for hello service?</span></span>
   * <span data-ttu-id="393d8-298">tooget поддержка hello службы, создайте возникшей проблемы на портале Azure для виртуальной Машины, где вы не может tooget ответа метаданных после нескольких попыток long hello</span><span class="sxs-lookup"><span data-stu-id="393d8-298">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![Поддержка метаданных экземпляров](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="393d8-300">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="393d8-300">Next Steps</span></span>

- <span data-ttu-id="393d8-301">Дополнительные сведения о hello [scheduledevents](virtual-machines-scheduled-events.md) API **в общедоступной предварительной версии** предоставляемые hello экземпляр метаданных службы.</span><span class="sxs-lookup"><span data-stu-id="393d8-301">Learn more about hello [scheduledevents](virtual-machines-scheduled-events.md) API **In Public Preview** provided by hello Instance Metadata Service.</span></span>
