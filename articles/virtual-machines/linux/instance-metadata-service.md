---
title: "aaaAzure экземпляра метаданные службы для виртуальных машин Linux | Документы Microsoft"
description: "Интерфейс rESTful tooget сведения о виртуальной Машине Linux вычислительных, сети и предстоящем обслуживании события."
services: virtual-machines-linux
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: 138822addea322c6e565b39a1b2002d7305f5fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-linux-vms"></a><span data-ttu-id="bf2df-103">Служба метаданных экземпляров Azure для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="bf2df-103">Azure Instance Metadata service for Linux VMs</span></span>


<span data-ttu-id="bf2df-104">Hello служба метаданных экземпляра Azure предоставляет сведения о выполнении экземпляров виртуальных машин, которые можно использовать toomanage и настроить виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="bf2df-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="bf2df-105">Сюда входят сведения о номере SKU, конфигурации сети и ближайших мероприятиях обслуживания.</span><span class="sxs-lookup"><span data-stu-id="bf2df-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="bf2df-106">Дополнительные сведения о том, какие сведения доступны, см. в разделе [Категории данных метаданных экземпляров](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="bf2df-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="bf2df-107">Служба метаданных экземпляра Azure является конечной точкой REST, доступный tooall ВМ IaaS, созданные при помощи hello [диспетчера ресурсов Azure](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="bf2df-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="bf2df-108">Hello конечная точка доступна по хорошо известных немаршрутизируемый IP-адрес (`169.254.169.254`), можно обратиться только из hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bf2df-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf2df-109">Эта служба является **общедоступной** в глобальных регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="bf2df-109">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="bf2df-110">Она находится в общедоступной предварительной версии для государственных организаций, облачной службы Azure для Китая и Германии.</span><span class="sxs-lookup"><span data-stu-id="bf2df-110">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="bf2df-111">Регулярно, он получает обновления tooexpose новые сведения об экземплярах виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="bf2df-111">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="bf2df-112">Эта страница отражает hello актуальные [категории данных](#instance-metadata-data-categories) доступны.</span><span class="sxs-lookup"><span data-stu-id="bf2df-112">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="bf2df-113">Доступность службы</span><span class="sxs-lookup"><span data-stu-id="bf2df-113">Service availability</span></span>
<span data-ttu-id="bf2df-114">Служба Hello доступна во всех регионах общедоступной глобального Azure.</span><span class="sxs-lookup"><span data-stu-id="bf2df-114">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="bf2df-115">Hello служба находится в общедоступной предварительной версии в регионах hello государственных организаций, Китай или Германии.</span><span class="sxs-lookup"><span data-stu-id="bf2df-115">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="bf2df-116">регионы</span><span class="sxs-lookup"><span data-stu-id="bf2df-116">Regions</span></span>                                        | <span data-ttu-id="bf2df-117">Доступность?</span><span class="sxs-lookup"><span data-stu-id="bf2df-117">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="bf2df-118">Все общедоступные глобальные регионы Azure</span><span class="sxs-lookup"><span data-stu-id="bf2df-118">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/regions/)     | <span data-ttu-id="bf2df-119">Общедоступная версия</span><span class="sxs-lookup"><span data-stu-id="bf2df-119">Generally Available</span></span> 
[<span data-ttu-id="bf2df-120">Azure для государственных организаций</span><span class="sxs-lookup"><span data-stu-id="bf2df-120">Azure Government</span></span>](https://azure.microsoft.com/overview/clouds/government/)              | <span data-ttu-id="bf2df-121">В предварительной версии</span><span class="sxs-lookup"><span data-stu-id="bf2df-121">In Preview</span></span> 
[<span data-ttu-id="bf2df-122">Azure для Китая</span><span class="sxs-lookup"><span data-stu-id="bf2df-122">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="bf2df-123">В предварительной версии</span><span class="sxs-lookup"><span data-stu-id="bf2df-123">In Preview</span></span>
[<span data-ttu-id="bf2df-124">Azure для Германии</span><span class="sxs-lookup"><span data-stu-id="bf2df-124">Azure Germany</span></span>](https://azure.microsoft.com/overview/clouds/germany/)                    | <span data-ttu-id="bf2df-125">В предварительной версии</span><span class="sxs-lookup"><span data-stu-id="bf2df-125">In Preview</span></span>

<span data-ttu-id="bf2df-126">Эта таблица обновляется, когда служба hello станет доступным в других облаках, Azure.</span><span class="sxs-lookup"><span data-stu-id="bf2df-126">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="bf2df-127">tootry out hello экземпляр метаданных службы, создайте виртуальную Машину из [диспетчера ресурсов Azure](https://docs.microsoft.com/rest/api/resources/) или hello [портал Azure](http://portal.azure.com) в hello выше области и выполните hello примеры ниже.</span><span class="sxs-lookup"><span data-stu-id="bf2df-127">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="bf2df-128">Использование</span><span class="sxs-lookup"><span data-stu-id="bf2df-128">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="bf2df-129">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="bf2df-129">Versioning</span></span>
<span data-ttu-id="bf2df-130">Hello метаданных экземпляра службы с версиями.</span><span class="sxs-lookup"><span data-stu-id="bf2df-130">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="bf2df-131">Версии являются обязательными, и текущая версия hello `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="bf2df-131">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="bf2df-132">Предыдущие выпуски Предварительный просмотр поддерживается {последние} в качестве hello api-version запланированные события.</span><span class="sxs-lookup"><span data-stu-id="bf2df-132">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="bf2df-133">Этот формат не поддерживается и будет считаться устаревшей в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="bf2df-133">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="bf2df-134">Так как мы добавляем новые версии, вы все еще можете получить доступ к предыдущим версиям для обеспечения совместимости, если используемый скрипт зависит от конкретных форматов данных.</span><span class="sxs-lookup"><span data-stu-id="bf2df-134">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="bf2df-135">Однако обратите внимание, что этой version(2017-03-01) hello текущего предварительного просмотра может оказаться недоступным после общедоступной службы hello.</span><span class="sxs-lookup"><span data-stu-id="bf2df-135">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="bf2df-136">Использование заголовков</span><span class="sxs-lookup"><span data-stu-id="bf2df-136">Using headers</span></span>
<span data-ttu-id="bf2df-137">При запросе hello экземпляр метаданных службы, необходимо указать заголовок hello `Metadata: true` tooensure hello запрос не был перенаправлен непреднамеренно.</span><span class="sxs-lookup"><span data-stu-id="bf2df-137">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="bf2df-138">Получение метаданных</span><span class="sxs-lookup"><span data-stu-id="bf2df-138">Retrieving metadata</span></span>

<span data-ttu-id="bf2df-139">Используйте метаданные экземпляров для запуска виртуальных машин, созданных или управляемых с помощью [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="bf2df-139">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="bf2df-140">Доступ к все категории данных для экземпляра виртуальной машины с помощью hello, следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="bf2df-140">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="bf2df-141">Во всех запросах метаданных экземпляров учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="bf2df-141">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="bf2df-142">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="bf2df-142">Data output</span></span>
<span data-ttu-id="bf2df-143">По умолчанию hello метаданных экземпляра службы возвращает данные в формате JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="bf2df-143">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="bf2df-144">Однако при необходимости другие API-интерфейсы могут возвращать данные в различных форматах.</span><span class="sxs-lookup"><span data-stu-id="bf2df-144">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="bf2df-145">Hello Следующая таблица представляет ссылки из других форматов данных, которые API-интерфейсы могут поддерживать.</span><span class="sxs-lookup"><span data-stu-id="bf2df-145">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="bf2df-146">API</span><span class="sxs-lookup"><span data-stu-id="bf2df-146">API</span></span> | <span data-ttu-id="bf2df-147">Формат данных по умолчанию</span><span class="sxs-lookup"><span data-stu-id="bf2df-147">Default Data Format</span></span> | <span data-ttu-id="bf2df-148">Другие форматы</span><span class="sxs-lookup"><span data-stu-id="bf2df-148">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="bf2df-149">/instance</span><span class="sxs-lookup"><span data-stu-id="bf2df-149">/instance</span></span> | <span data-ttu-id="bf2df-150">json</span><span class="sxs-lookup"><span data-stu-id="bf2df-150">json</span></span> | <span data-ttu-id="bf2df-151">text</span><span class="sxs-lookup"><span data-stu-id="bf2df-151">text</span></span>
<span data-ttu-id="bf2df-152">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="bf2df-152">/scheduledevents</span></span> | <span data-ttu-id="bf2df-153">json</span><span class="sxs-lookup"><span data-stu-id="bf2df-153">json</span></span> | <span data-ttu-id="bf2df-154">Нет</span><span class="sxs-lookup"><span data-stu-id="bf2df-154">none</span></span>

<span data-ttu-id="bf2df-155">tooaccess формата ответа не по умолчанию, укажите запрошенный формат hello в качестве параметра строки запроса в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="bf2df-155">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="bf2df-156">Например:</span><span class="sxs-lookup"><span data-stu-id="bf2df-156">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="bf2df-157">Безопасность</span><span class="sxs-lookup"><span data-stu-id="bf2df-157">Security</span></span>
<span data-ttu-id="bf2df-158">Конечная точка службы метаданных экземпляра Hello доступна только из hello ОС немаршрутизируемый IP-адрес экземпляра виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="bf2df-158">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="bf2df-159">Кроме того, любой запрос с `X-Forwarded-For` заголовок, отклоняется службой hello.</span><span class="sxs-lookup"><span data-stu-id="bf2df-159">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="bf2df-160">Мы также требуется toocontain запросы `Metadata: true` tooensure заголовок, hello сам запрос непосредственно было предназначено и не является частью непреднамеренного перенаправления.</span><span class="sxs-lookup"><span data-stu-id="bf2df-160">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="bf2df-161">Ошибка</span><span class="sxs-lookup"><span data-stu-id="bf2df-161">Error</span></span>
<span data-ttu-id="bf2df-162">Если элемент данных не найден или имеет неправильный формат запроса hello метаданных экземпляра службы возвращает стандартные ошибки HTTP.</span><span class="sxs-lookup"><span data-stu-id="bf2df-162">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="bf2df-163">Например:</span><span class="sxs-lookup"><span data-stu-id="bf2df-163">For example:</span></span>

<span data-ttu-id="bf2df-164">Код состояния HTTP</span><span class="sxs-lookup"><span data-stu-id="bf2df-164">HTTP Status Code</span></span> | <span data-ttu-id="bf2df-165">Причина</span><span class="sxs-lookup"><span data-stu-id="bf2df-165">Reason</span></span>
----------------|-------
<span data-ttu-id="bf2df-166">200 ОК</span><span class="sxs-lookup"><span data-stu-id="bf2df-166">200 OK</span></span> |
<span data-ttu-id="bf2df-167">400 — недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="bf2df-167">400 Bad Request</span></span> | <span data-ttu-id="bf2df-168">Отсутствует заголовок `Metadata: true`</span><span class="sxs-lookup"><span data-stu-id="bf2df-168">Missing `Metadata: true` header</span></span>
<span data-ttu-id="bf2df-169">404 — не найдено</span><span class="sxs-lookup"><span data-stu-id="bf2df-169">404 Not Found</span></span> | <span data-ttu-id="bf2df-170">Hello does't запрошенный элемент существует</span><span class="sxs-lookup"><span data-stu-id="bf2df-170">hello requested element does't exist</span></span> 
<span data-ttu-id="bf2df-171">405 — недопустимый метод</span><span class="sxs-lookup"><span data-stu-id="bf2df-171">405 Method Not Allowed</span></span> | <span data-ttu-id="bf2df-172">Поддерживаются только запросы `GET` и `POST`</span><span class="sxs-lookup"><span data-stu-id="bf2df-172">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="bf2df-173">429 — слишком много запросов</span><span class="sxs-lookup"><span data-stu-id="bf2df-173">429 Too Many Requests</span></span> | <span data-ttu-id="bf2df-174">Hello API в настоящее время поддерживает не более 5 запросов в секунду</span><span class="sxs-lookup"><span data-stu-id="bf2df-174">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="bf2df-175">500 — ошибка службы</span><span class="sxs-lookup"><span data-stu-id="bf2df-175">500 Service Error</span></span>     | <span data-ttu-id="bf2df-176">Повторите попытку через некоторое время</span><span class="sxs-lookup"><span data-stu-id="bf2df-176">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="bf2df-177">Примеры</span><span class="sxs-lookup"><span data-stu-id="bf2df-177">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="bf2df-178">Все ответы API — это строки в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="bf2df-178">All API responses are JSON strings.</span></span> <span data-ttu-id="bf2df-179">Все следующие примеры ответов представлены в удобном для чтения формате.</span><span class="sxs-lookup"><span data-stu-id="bf2df-179">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="bf2df-180">Получение сведений о сети</span><span class="sxs-lookup"><span data-stu-id="bf2df-180">Retrieving network information</span></span>

<span data-ttu-id="bf2df-181">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="bf2df-181">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="bf2df-182">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="bf2df-182">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="bf2df-183">Hello ответа представляет собой строку JSON.</span><span class="sxs-lookup"><span data-stu-id="bf2df-183">hello response is a JSON string.</span></span> <span data-ttu-id="bf2df-184">Следующий пример ответа Hello, представленное для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="bf2df-184">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="bf2df-185">Получение общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="bf2df-185">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="bf2df-186">Получение всех метаданных для экземпляра</span><span class="sxs-lookup"><span data-stu-id="bf2df-186">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="bf2df-187">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="bf2df-187">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="bf2df-188">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="bf2df-188">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="bf2df-189">Hello ответа представляет собой строку JSON.</span><span class="sxs-lookup"><span data-stu-id="bf2df-189">hello response is a JSON string.</span></span> <span data-ttu-id="bf2df-190">Следующий пример ответа Hello, представленное для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="bf2df-190">hello following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="bf2df-191">Получение метаданных в виртуальной машине Windows</span><span class="sxs-lookup"><span data-stu-id="bf2df-191">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="bf2df-192">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="bf2df-192">**Request**</span></span>

<span data-ttu-id="bf2df-193">Можно получить метаданные экземпляра в Windows через PowerShell программа hello `curl`:</span><span class="sxs-lookup"><span data-stu-id="bf2df-193">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="bf2df-194">Или с помощью hello `Invoke-RestMethod` командлета:</span><span class="sxs-lookup"><span data-stu-id="bf2df-194">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="bf2df-195">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="bf2df-195">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="bf2df-196">Hello ответа представляет собой строку JSON.</span><span class="sxs-lookup"><span data-stu-id="bf2df-196">hello response is a JSON string.</span></span> <span data-ttu-id="bf2df-197">Следующий пример ответа Hello, представленное для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="bf2df-197">hello following example response  is pretty-printed for readability.</span></span>

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

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="bf2df-198">Категории данных метаданных экземпляров</span><span class="sxs-lookup"><span data-stu-id="bf2df-198">Instance metadata data categories</span></span>
<span data-ttu-id="bf2df-199">Привет, следующие категории данных доступны через hello экземпляр службы метаданных:</span><span class="sxs-lookup"><span data-stu-id="bf2df-199">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="bf2df-200">Данные</span><span class="sxs-lookup"><span data-stu-id="bf2df-200">Data</span></span> | <span data-ttu-id="bf2df-201">Описание</span><span class="sxs-lookup"><span data-stu-id="bf2df-201">Description</span></span>
-----|------------
<span data-ttu-id="bf2df-202">location</span><span class="sxs-lookup"><span data-stu-id="bf2df-202">location</span></span> | <span data-ttu-id="bf2df-203">Hello Azure области ВМ работает</span><span class="sxs-lookup"><span data-stu-id="bf2df-203">Azure Region hello VM is running in</span></span>
<span data-ttu-id="bf2df-204">name</span><span class="sxs-lookup"><span data-stu-id="bf2df-204">name</span></span> | <span data-ttu-id="bf2df-205">Имя виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="bf2df-205">Name of hello VM</span></span> 
<span data-ttu-id="bf2df-206">offer</span><span class="sxs-lookup"><span data-stu-id="bf2df-206">offer</span></span> | <span data-ttu-id="bf2df-207">Предоставляют сведения для hello образа виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bf2df-207">Offer information for hello VM image.</span></span> <span data-ttu-id="bf2df-208">Это значение доступно только для образов, развернутых из коллекции образов Azure.</span><span class="sxs-lookup"><span data-stu-id="bf2df-208">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="bf2df-209">publisher</span><span class="sxs-lookup"><span data-stu-id="bf2df-209">publisher</span></span> | <span data-ttu-id="bf2df-210">Издатель образа ВМ hello</span><span class="sxs-lookup"><span data-stu-id="bf2df-210">Publisher of hello VM image</span></span>
<span data-ttu-id="bf2df-211">sku</span><span class="sxs-lookup"><span data-stu-id="bf2df-211">sku</span></span> | <span data-ttu-id="bf2df-212">Конфигурации для образа виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="bf2df-212">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="bf2df-213">версия</span><span class="sxs-lookup"><span data-stu-id="bf2df-213">version</span></span> | <span data-ttu-id="bf2df-214">Версия образа виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="bf2df-214">Version of hello VM image</span></span> 
<span data-ttu-id="bf2df-215">osType</span><span class="sxs-lookup"><span data-stu-id="bf2df-215">osType</span></span> | <span data-ttu-id="bf2df-216">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="bf2df-216">Linux or Windows</span></span> 
<span data-ttu-id="bf2df-217">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="bf2df-217">platformUpdateDomain</span></span> |  <span data-ttu-id="bf2df-218">[Домен обновления](manage-availability.md) hello в запущенной виртуальной Машине</span><span class="sxs-lookup"><span data-stu-id="bf2df-218">[Update domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="bf2df-219">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="bf2df-219">platformFaultDomain</span></span> | <span data-ttu-id="bf2df-220">[Домен сбоя](manage-availability.md) hello в запущенной виртуальной Машине</span><span class="sxs-lookup"><span data-stu-id="bf2df-220">[Fault domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="bf2df-221">vmId</span><span class="sxs-lookup"><span data-stu-id="bf2df-221">vmId</span></span> | <span data-ttu-id="bf2df-222">[Уникальный идентификатор](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) для hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="bf2df-222">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="bf2df-223">vmSize</span><span class="sxs-lookup"><span data-stu-id="bf2df-223">vmSize</span></span> | [<span data-ttu-id="bf2df-224">Размер виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="bf2df-224">VM size</span></span>](sizes.md)
<span data-ttu-id="bf2df-225">ipv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="bf2df-225">ipv4/privateIpAddress</span></span> | <span data-ttu-id="bf2df-226">Локальный адрес IPv4 hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="bf2df-226">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="bf2df-227">ipv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="bf2df-227">ipv4/publicIpAddress</span></span> | <span data-ttu-id="bf2df-228">Общедоступный адрес IPv4 hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="bf2df-228">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="bf2df-229">subnet/address</span><span class="sxs-lookup"><span data-stu-id="bf2df-229">subnet/address</span></span> | <span data-ttu-id="bf2df-230">Адрес подсети hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="bf2df-230">Subnet address of hello VM</span></span>
<span data-ttu-id="bf2df-231">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="bf2df-231">subnet/prefix</span></span> | <span data-ttu-id="bf2df-232">Префикс подсети, пример 24</span><span class="sxs-lookup"><span data-stu-id="bf2df-232">Subnet prefix, example 24</span></span>
<span data-ttu-id="bf2df-233">ipv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="bf2df-233">ipv6/ipAddress</span></span> | <span data-ttu-id="bf2df-234">Локальный адрес IPv6 hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="bf2df-234">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="bf2df-235">macAddress</span><span class="sxs-lookup"><span data-stu-id="bf2df-235">macAddress</span></span> | <span data-ttu-id="bf2df-236">Mac-адрес виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="bf2df-236">VM mac address</span></span> 
<span data-ttu-id="bf2df-237">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="bf2df-237">scheduledevents</span></span> | <span data-ttu-id="bf2df-238">Сейчас в общедоступной предварительной версии. Дополнительные сведения см. в статье [Служба метаданных Azure. Запланированные события (предварительная версия)](scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="bf2df-238">Currently in Public Preview See [scheduledevents](scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="bf2df-239">Примеры сценариев использования</span><span class="sxs-lookup"><span data-stu-id="bf2df-239">Example scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="bf2df-240">Отслеживание виртуальной машины в Azure</span><span class="sxs-lookup"><span data-stu-id="bf2df-240">Tracking VM running on Azure</span></span>

<span data-ttu-id="bf2df-241">Как поставщик услуг может потребоваться tootrack hello число работающих виртуальных машин программного обеспечения или агентами, которые должны tootrack уникальность hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bf2df-241">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="bf2df-242">возможности tooget toobe уникальный идентификатор для виртуальной Машины, используйте hello `vmId` из метаданных службы экземпляра.</span><span class="sxs-lookup"><span data-stu-id="bf2df-242">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="bf2df-243">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="bf2df-243">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="bf2df-244">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="bf2df-244">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="bf2df-245">Размещение контейнеров и секций данных на основе домена сбоя или обновления</span><span class="sxs-lookup"><span data-stu-id="bf2df-245">Placement of containers, data-partitions based fault/update domain</span></span> 

<span data-ttu-id="bf2df-246">В некоторых сценариях размещение разных реплик имеет первостепенное значение.</span><span class="sxs-lookup"><span data-stu-id="bf2df-246">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="bf2df-247">Например [размещения реплики HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) или размещения контейнера через [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) может потребоваться tooknow hello `platformFaultDomain` и `platformUpdateDomain` hello, Виртуальная машина работает на.</span><span class="sxs-lookup"><span data-stu-id="bf2df-247">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="bf2df-248">Вы можете запрашивать эти данные напрямую через hello экземпляр метаданных службы.</span><span class="sxs-lookup"><span data-stu-id="bf2df-248">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="bf2df-249">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="bf2df-249">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="bf2df-250">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="bf2df-250">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="bf2df-251">Получение дополнительных сведений о hello виртуальной Машины во время службу технической поддержки Майкрософт</span><span class="sxs-lookup"><span data-stu-id="bf2df-251">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="bf2df-252">Как поставщик услуг то появляется поддержки по телефону куда tooknow Дополнительные сведения о hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bf2df-252">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="bf2df-253">Запрос клиента tooshare hello hello вычислений метаданных может предоставить основные сведения для специалистов tooknow поддержки hello о hello типа ВМ в Azure.</span><span class="sxs-lookup"><span data-stu-id="bf2df-253">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="bf2df-254">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="bf2df-254">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="bf2df-255">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="bf2df-255">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="bf2df-256">Hello ответа представляет собой строку JSON.</span><span class="sxs-lookup"><span data-stu-id="bf2df-256">hello response is a JSON string.</span></span> <span data-ttu-id="bf2df-257">Следующий пример ответа Hello, представленное для удобства чтения.</span><span class="sxs-lookup"><span data-stu-id="bf2df-257">hello following example response is pretty-printed for readability.</span></span>

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="bf2df-258">Примеры вызова метаданные службы с использованием различных языков внутри hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="bf2df-258">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="bf2df-259">Язык</span><span class="sxs-lookup"><span data-stu-id="bf2df-259">Language</span></span> | <span data-ttu-id="bf2df-260">Пример</span><span class="sxs-lookup"><span data-stu-id="bf2df-260">Example</span></span> 
---------|----------------
<span data-ttu-id="bf2df-261">Ruby</span><span class="sxs-lookup"><span data-stu-id="bf2df-261">Ruby</span></span>     | <span data-ttu-id="bf2df-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="bf2df-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="bf2df-263">Перейдите в локальную сеть</span><span class="sxs-lookup"><span data-stu-id="bf2df-263">Go Lan</span></span>   | <span data-ttu-id="bf2df-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="bf2df-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="bf2df-265">python</span><span class="sxs-lookup"><span data-stu-id="bf2df-265">python</span></span>   | <span data-ttu-id="bf2df-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="bf2df-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="bf2df-267">C++</span><span class="sxs-lookup"><span data-stu-id="bf2df-267">C++</span></span>      | <span data-ttu-id="bf2df-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="bf2df-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="bf2df-269">C#</span><span class="sxs-lookup"><span data-stu-id="bf2df-269">C#</span></span>       | <span data-ttu-id="bf2df-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="bf2df-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="bf2df-271">JavaScript</span><span class="sxs-lookup"><span data-stu-id="bf2df-271">Javascript</span></span> | <span data-ttu-id="bf2df-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="bf2df-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="bf2df-273">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf2df-273">Powershell</span></span> | <span data-ttu-id="bf2df-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="bf2df-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="bf2df-275">Bash</span><span class="sxs-lookup"><span data-stu-id="bf2df-275">Bash</span></span>       | <span data-ttu-id="bf2df-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="bf2df-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="bf2df-277">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="bf2df-277">FAQ</span></span>
1. <span data-ttu-id="bf2df-278">Я получаю hello ошибки `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="bf2df-278">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="bf2df-279">Что это означает?</span><span class="sxs-lookup"><span data-stu-id="bf2df-279">What does this mean?</span></span>
   * <span data-ttu-id="bf2df-280">Hello служба метаданных экземпляра требуется заголовок hello `Metadata: true` toobe переданный запрос hello.</span><span class="sxs-lookup"><span data-stu-id="bf2df-280">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="bf2df-281">Передача этого заголовка в вызове REST hello позволяет toohello доступ службы метаданных экземпляра.</span><span class="sxs-lookup"><span data-stu-id="bf2df-281">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="bf2df-282">Почему я не получаю сведения о вычислениях для виртуальной машины?</span><span class="sxs-lookup"><span data-stu-id="bf2df-282">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="bf2df-283">Hello экземпляр метаданных службы, в настоящее время поддерживает только экземпляры, созданные с помощью диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="bf2df-283">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="bf2df-284">В будущем hello Корпорация Майкрософт может расширить поддержку виртуальных машин облачной службы.</span><span class="sxs-lookup"><span data-stu-id="bf2df-284">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="bf2df-285">Виртуальная машина была недавно создана с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bf2df-285">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="bf2df-286">Почему не отображаются сведения о метаданных вычислений?</span><span class="sxs-lookup"><span data-stu-id="bf2df-286">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="bf2df-287">Все виртуальные машины, созданные после сентября 2016, добавьте [тега](../../azure-resource-manager/resource-group-using-tags.md) toostart просматривают метаданные вычислений.</span><span class="sxs-lookup"><span data-stu-id="bf2df-287">For any VMs created after Sep 2016, add a [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="bf2df-288">Для более старых виртуальных машин (создан до сентября 2016) Добавление и удаление расширения или данных метаданных toorefresh дисков toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bf2df-288">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="bf2df-289">Почему выдается ошибка hello `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="bf2df-289">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="bf2df-290">Повторите запрос в зависимости от экспоненциальной системы.</span><span class="sxs-lookup"><span data-stu-id="bf2df-290">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="bf2df-291">Если hello проблема повторится, обратитесь в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="bf2df-291">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="bf2df-292">Где можно задать дополнительные вопросы или оставить комментарии?</span><span class="sxs-lookup"><span data-stu-id="bf2df-292">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="bf2df-293">Оставьте комментарии на сайте http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="bf2df-293">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="bf2df-294">Будет ли это работать для экземпляра масштабируемого набора виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="bf2df-294">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="bf2df-295">Да, служба метаданных доступна для экземпляров масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="bf2df-295">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="bf2df-296">Получение поддержки для службы hello</span><span class="sxs-lookup"><span data-stu-id="bf2df-296">How do I get support for hello service?</span></span>
   * <span data-ttu-id="bf2df-297">tooget поддержка hello службы, создайте возникшей проблемы на портале Azure для виртуальной Машины, где вы не может tooget ответа метаданных после нескольких попыток long hello</span><span class="sxs-lookup"><span data-stu-id="bf2df-297">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![Поддержка метаданных экземпляров](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="bf2df-299">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bf2df-299">Next steps</span></span>

- <span data-ttu-id="bf2df-300">Дополнительные сведения о hello [запланированные события](scheduled-events.md) API **в общедоступной предварительной версии** предоставляемые hello метаданные экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="bf2df-300">Learn more about hello [Scheduled Events](scheduled-events.md) API **in public preview** provided by hello Instance Metadata service.</span></span>
