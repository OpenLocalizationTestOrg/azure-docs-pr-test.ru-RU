---
title: "Общие сведения о службе метаданных экземпляров Azure | Документация Майкрософт"
description: "Использование интерфейса RESTful для получения сведений о вычислительных ресурсах виртуальной машины, сети и ближайших мероприятиях обслуживания."
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
ms.openlocfilehash: d601d8fdb92bf2d3253ba99cdeee10e09591689c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-instance-metadata-service"></a><span data-ttu-id="cb840-103">Служба метаданных экземпляров Azure</span><span class="sxs-lookup"><span data-stu-id="cb840-103">Azure Instance Metadata Service</span></span> 


<span data-ttu-id="cb840-104">Служба метаданных экземпляров Azure предоставляет сведения о выполнении экземпляров виртуальных машин, которые можно использовать для настройки виртуальных машин и управления ими.</span><span class="sxs-lookup"><span data-stu-id="cb840-104">The Azure Instance Metadata Service provides information about running virtual machine instances that can be used to manage and configure your virtual machines.</span></span>
<span data-ttu-id="cb840-105">Сюда входят сведения о номере SKU, конфигурации сети и ближайших мероприятиях обслуживания.</span><span class="sxs-lookup"><span data-stu-id="cb840-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="cb840-106">Дополнительные сведения о том, какие сведения доступны, см. в разделе [Категории данных метаданных экземпляров](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="cb840-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="cb840-107">Служба метаданных экземпляров Azure — это конечная точка REST, доступная для всех виртуальных машин IaaS, созданных с помощью нового [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="cb840-107">Azure's Instance Metadata Service is a REST Endpoint accessible to all IaaS VMs created via the [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="cb840-108">Конечная точка доступна по известному IP-адресу без поддержки маршрутизации (`169.254.169.254`), к которому можно получить доступ только в пределах виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="cb840-108">The endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within the VM.</span></span>

### <a name="important-information"></a><span data-ttu-id="cb840-109">Важные сведения</span><span class="sxs-lookup"><span data-stu-id="cb840-109">Important information</span></span>

<span data-ttu-id="cb840-110">Эта служба является **общедоступной** в глобальных регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="cb840-110">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="cb840-111">Она находится в общедоступной предварительной версии для государственных организаций, облачной службы Azure для Китая и Германии.</span><span class="sxs-lookup"><span data-stu-id="cb840-111">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="cb840-112">Она регулярно получает обновления, чтобы предоставлять новые сведения об экземплярах виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="cb840-112">It regularly receives updates to expose new information about virtual machine instances.</span></span> <span data-ttu-id="cb840-113">На этой странице представлены актуальные сведения о доступных [категориях данных](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="cb840-113">This page reflects the up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="cb840-114">Доступность службы</span><span class="sxs-lookup"><span data-stu-id="cb840-114">Service Availability</span></span>
<span data-ttu-id="cb840-115">Служба доступна во всех общедоступных глобальных регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="cb840-115">The service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="cb840-116">Служба находится в общедоступной предварительной версии в регионах государственных организаций, Китая и Германии.</span><span class="sxs-lookup"><span data-stu-id="cb840-116">The service is in public preview  in the Government, China, or Germany regions.</span></span>

<span data-ttu-id="cb840-117">регионы</span><span class="sxs-lookup"><span data-stu-id="cb840-117">Regions</span></span>                                        | <span data-ttu-id="cb840-118">Доступность?</span><span class="sxs-lookup"><span data-stu-id="cb840-118">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="cb840-119">Все общедоступные глобальные регионы Azure</span><span class="sxs-lookup"><span data-stu-id="cb840-119">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/en-us/regions/)     | <span data-ttu-id="cb840-120">Общедоступная версия</span><span class="sxs-lookup"><span data-stu-id="cb840-120">Generally Available</span></span> 
[<span data-ttu-id="cb840-121">Azure для государственных организаций</span><span class="sxs-lookup"><span data-stu-id="cb840-121">Azure Government</span></span>](https://azure.microsoft.com/en-us/overview/clouds/government/)              | <span data-ttu-id="cb840-122">В предварительной версии</span><span class="sxs-lookup"><span data-stu-id="cb840-122">In Preview</span></span> 
[<span data-ttu-id="cb840-123">Azure для Китая</span><span class="sxs-lookup"><span data-stu-id="cb840-123">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="cb840-124">В предварительной версии</span><span class="sxs-lookup"><span data-stu-id="cb840-124">In Preview</span></span>
[<span data-ttu-id="cb840-125">Azure для Германии</span><span class="sxs-lookup"><span data-stu-id="cb840-125">Azure Germany</span></span>](https://azure.microsoft.com/en-us/overview/clouds/germany/)                    | <span data-ttu-id="cb840-126">В предварительной версии</span><span class="sxs-lookup"><span data-stu-id="cb840-126">In Preview</span></span>

<span data-ttu-id="cb840-127">Эта таблица обновляется, когда служба становится доступной в других облачных службах Azure.</span><span class="sxs-lookup"><span data-stu-id="cb840-127">This table is updated when the service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="cb840-128">Чтобы проверить службу метаданных экземпляров, создайте виртуальную машину в [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) или на [портале Azure](http://portal.azure.com) в приведенных выше регионах согласно примерам ниже.</span><span class="sxs-lookup"><span data-stu-id="cb840-128">To try out the Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or the [Azure portal](http://portal.azure.com) in the above regions and follow the examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="cb840-129">Использование</span><span class="sxs-lookup"><span data-stu-id="cb840-129">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="cb840-130">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="cb840-130">Versioning</span></span>
<span data-ttu-id="cb840-131">Для службы метаданных экземпляров включено управление версиями.</span><span class="sxs-lookup"><span data-stu-id="cb840-131">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="cb840-132">Версии являются обязательными. На данный момент используется версия от `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="cb840-132">Versions are mandatory and the current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="cb840-133">В предыдущих выпусках предварительной версии в качестве api-version поддерживалось значение {latest}.</span><span class="sxs-lookup"><span data-stu-id="cb840-133">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="cb840-134">Этот формат больше не поддерживается и в дальнейшем будет считаться устаревшим.</span><span class="sxs-lookup"><span data-stu-id="cb840-134">This format is no longer supported and will be deprecated in the future.</span></span>

<span data-ttu-id="cb840-135">Так как мы добавляем новые версии, вы все еще можете получить доступ к предыдущим версиям для обеспечения совместимости, если используемый скрипт зависит от конкретных форматов данных.</span><span class="sxs-lookup"><span data-stu-id="cb840-135">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="cb840-136">Тем не менее обратите внимание, что текущая предварительная версия (от 01.03.2017) может быть недоступна после выпуска общедоступной службы.</span><span class="sxs-lookup"><span data-stu-id="cb840-136">However, note that the current preview version(2017-03-01) may not be available once the service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="cb840-137">Использование заголовков</span><span class="sxs-lookup"><span data-stu-id="cb840-137">Using Headers</span></span>
<span data-ttu-id="cb840-138">При запросе службы метаданных экземпляров необходимо указать заголовок `Metadata: true`, чтобы избежать случайного перенаправления запроса.</span><span class="sxs-lookup"><span data-stu-id="cb840-138">When you query the Instance Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="cb840-139">Получение метаданных</span><span class="sxs-lookup"><span data-stu-id="cb840-139">Retrieving metadata</span></span>

<span data-ttu-id="cb840-140">Используйте метаданные экземпляров для запуска виртуальных машин, созданных или управляемых с помощью [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="cb840-140">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="cb840-141">Вы можете получить доступ ко всем категориям данных экземпляров виртуальной машины с помощью следующего запроса:</span><span class="sxs-lookup"><span data-stu-id="cb840-141">Access all data categories for a virtual machine instance using the following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="cb840-142">Во всех запросах метаданных экземпляров учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="cb840-142">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="cb840-143">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="cb840-143">Data output</span></span>
<span data-ttu-id="cb840-144">По умолчанию служба метаданных экземпляров возвращает данные в формате JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="cb840-144">By default, the Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="cb840-145">Однако при необходимости другие API-интерфейсы могут возвращать данные в различных форматах.</span><span class="sxs-lookup"><span data-stu-id="cb840-145">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="cb840-146">В следующей таблице приведены сведения о других форматах данных, поддерживаемых API-интерфейсами.</span><span class="sxs-lookup"><span data-stu-id="cb840-146">The following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="cb840-147">API</span><span class="sxs-lookup"><span data-stu-id="cb840-147">API</span></span> | <span data-ttu-id="cb840-148">Формат данных по умолчанию</span><span class="sxs-lookup"><span data-stu-id="cb840-148">Default Data Format</span></span> | <span data-ttu-id="cb840-149">Другие форматы</span><span class="sxs-lookup"><span data-stu-id="cb840-149">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="cb840-150">/instance</span><span class="sxs-lookup"><span data-stu-id="cb840-150">/instance</span></span> | <span data-ttu-id="cb840-151">json</span><span class="sxs-lookup"><span data-stu-id="cb840-151">json</span></span> | <span data-ttu-id="cb840-152">text</span><span class="sxs-lookup"><span data-stu-id="cb840-152">text</span></span>
<span data-ttu-id="cb840-153">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="cb840-153">/scheduledevents</span></span> | <span data-ttu-id="cb840-154">json</span><span class="sxs-lookup"><span data-stu-id="cb840-154">json</span></span> | <span data-ttu-id="cb840-155">Нет</span><span class="sxs-lookup"><span data-stu-id="cb840-155">none</span></span>

<span data-ttu-id="cb840-156">Для доступа к нестандартному формату ответа укажите в запросе запрошенный формат в качестве параметра строки запроса.</span><span class="sxs-lookup"><span data-stu-id="cb840-156">To access a non-default response format, specify the requested format as a querystring parameter in the request.</span></span> <span data-ttu-id="cb840-157">Например:</span><span class="sxs-lookup"><span data-stu-id="cb840-157">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="cb840-158">Безопасность</span><span class="sxs-lookup"><span data-stu-id="cb840-158">Security</span></span>
<span data-ttu-id="cb840-159">Конечная точка службы метаданных экземпляров доступна только в пределах запущенного экземпляра виртуальной машины на IP-адресе, не поддерживающем маршрутизацию.</span><span class="sxs-lookup"><span data-stu-id="cb840-159">The Instance Metadata Service endpoint is accessible only from within the running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="cb840-160">Кроме того, любой запрос с заголовком `X-Forwarded-For` отклоняется службой.</span><span class="sxs-lookup"><span data-stu-id="cb840-160">In addition, any request with a `X-Forwarded-For` header is rejected by the service.</span></span>
<span data-ttu-id="cb840-161">Чтобы гарантировать, что фактический запрос отправлен напрямую и не был получен в ходе непреднамеренного перенаправления, он должен содержать отправляемый заголовок `Metadata: true`.</span><span class="sxs-lookup"><span data-stu-id="cb840-161">We also require requests to contain a `Metadata: true` header to ensure that the actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="cb840-162">Ошибка</span><span class="sxs-lookup"><span data-stu-id="cb840-162">Error</span></span>
<span data-ttu-id="cb840-163">Если элемент данных не найден или запрос неправильно сформирован, службы метаданных экземпляров возвращают стандартные ошибки HTTP.</span><span class="sxs-lookup"><span data-stu-id="cb840-163">If there is a data element not found or a malformed request, the Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="cb840-164">Например:</span><span class="sxs-lookup"><span data-stu-id="cb840-164">For example:</span></span>

<span data-ttu-id="cb840-165">Код состояния HTTP</span><span class="sxs-lookup"><span data-stu-id="cb840-165">HTTP Status Code</span></span> | <span data-ttu-id="cb840-166">Причина</span><span class="sxs-lookup"><span data-stu-id="cb840-166">Reason</span></span>
----------------|-------
<span data-ttu-id="cb840-167">200 ОК</span><span class="sxs-lookup"><span data-stu-id="cb840-167">200 OK</span></span> |
<span data-ttu-id="cb840-168">400 — недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="cb840-168">400 Bad Request</span></span> | <span data-ttu-id="cb840-169">Отсутствует заголовок `Metadata: true`</span><span class="sxs-lookup"><span data-stu-id="cb840-169">Missing `Metadata: true` header</span></span>
<span data-ttu-id="cb840-170">404 — не найдено</span><span class="sxs-lookup"><span data-stu-id="cb840-170">404 Not Found</span></span> | <span data-ttu-id="cb840-171">Запрашиваемый элемент не существует</span><span class="sxs-lookup"><span data-stu-id="cb840-171">The requested element does't exist</span></span> 
<span data-ttu-id="cb840-172">405 — недопустимый метод</span><span class="sxs-lookup"><span data-stu-id="cb840-172">405 Method Not Allowed</span></span> | <span data-ttu-id="cb840-173">Поддерживаются только запросы `GET` и `POST`</span><span class="sxs-lookup"><span data-stu-id="cb840-173">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="cb840-174">429 — слишком много запросов</span><span class="sxs-lookup"><span data-stu-id="cb840-174">429 Too Many Requests</span></span> | <span data-ttu-id="cb840-175">Сейчас API-интерфейс поддерживает максимум 5 запросов в секунду</span><span class="sxs-lookup"><span data-stu-id="cb840-175">The API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="cb840-176">500 — ошибка службы</span><span class="sxs-lookup"><span data-stu-id="cb840-176">500 Service Error</span></span>     | <span data-ttu-id="cb840-177">Повторите попытку через некоторое время</span><span class="sxs-lookup"><span data-stu-id="cb840-177">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="cb840-178">Примеры</span><span class="sxs-lookup"><span data-stu-id="cb840-178">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="cb840-179">Все ответы API — это строки в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="cb840-179">All API responses are JSON strings.</span></span> <span data-ttu-id="cb840-180">Все следующие примеры ответов представлены в удобном для чтения формате.</span><span class="sxs-lookup"><span data-stu-id="cb840-180">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="cb840-181">Получение сведений о сети</span><span class="sxs-lookup"><span data-stu-id="cb840-181">Retrieving network information</span></span>

<span data-ttu-id="cb840-182">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="cb840-182">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="cb840-183">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="cb840-183">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="cb840-184">Ответ представляет собой строку JSON.</span><span class="sxs-lookup"><span data-stu-id="cb840-184">The response is a JSON string.</span></span> <span data-ttu-id="cb840-185">Следующие примеры ответов представлены в удобном для чтения формате.</span><span class="sxs-lookup"><span data-stu-id="cb840-185">The following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="cb840-186">Получение общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="cb840-186">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="cb840-187">Получение всех метаданных для экземпляра</span><span class="sxs-lookup"><span data-stu-id="cb840-187">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="cb840-188">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="cb840-188">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="cb840-189">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="cb840-189">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="cb840-190">Ответ представляет собой строку JSON.</span><span class="sxs-lookup"><span data-stu-id="cb840-190">The response is a JSON string.</span></span> <span data-ttu-id="cb840-191">Следующие примеры ответов представлены в удобном для чтения формате.</span><span class="sxs-lookup"><span data-stu-id="cb840-191">The following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="cb840-192">Получение метаданных в виртуальной машине Windows</span><span class="sxs-lookup"><span data-stu-id="cb840-192">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="cb840-193">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="cb840-193">**Request**</span></span>

<span data-ttu-id="cb840-194">Метаданные экземпляра в Windows можно получить с помощью служебной программы `curl` службы PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cb840-194">Instance metadata can be retrieved in Windows via the PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="cb840-195">Либо с помощью командлета `Invoke-RestMethod`:</span><span class="sxs-lookup"><span data-stu-id="cb840-195">Or through the `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="cb840-196">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="cb840-196">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="cb840-197">Ответ представляет собой строку JSON.</span><span class="sxs-lookup"><span data-stu-id="cb840-197">The response is a JSON string.</span></span> <span data-ttu-id="cb840-198">Следующие примеры ответов представлены в удобном для чтения формате.</span><span class="sxs-lookup"><span data-stu-id="cb840-198">The following example response  is pretty-printed for readability.</span></span>

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

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="cb840-199">Категории данных метаданных экземпляров</span><span class="sxs-lookup"><span data-stu-id="cb840-199">Instance metadata data categories</span></span>
<span data-ttu-id="cb840-200">Следующие категории данных доступны через службу метаданных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="cb840-200">The following data categories are available through the Instance Metadata Service:</span></span>

<span data-ttu-id="cb840-201">Данные</span><span class="sxs-lookup"><span data-stu-id="cb840-201">Data</span></span> | <span data-ttu-id="cb840-202">Описание</span><span class="sxs-lookup"><span data-stu-id="cb840-202">Description</span></span>
-----|------------
<span data-ttu-id="cb840-203">location</span><span class="sxs-lookup"><span data-stu-id="cb840-203">location</span></span> | <span data-ttu-id="cb840-204">Регион Azure, в котором запущена виртуальная машина</span><span class="sxs-lookup"><span data-stu-id="cb840-204">Azure Region the VM is running in</span></span>
<span data-ttu-id="cb840-205">name</span><span class="sxs-lookup"><span data-stu-id="cb840-205">name</span></span> | <span data-ttu-id="cb840-206">Имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="cb840-206">Name of the VM</span></span> 
<span data-ttu-id="cb840-207">offer</span><span class="sxs-lookup"><span data-stu-id="cb840-207">offer</span></span> | <span data-ttu-id="cb840-208">Предоставляют сведения об образе виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="cb840-208">Offer information for the VM image.</span></span> <span data-ttu-id="cb840-209">Это значение доступно только для образов, развернутых из коллекции образов Azure.</span><span class="sxs-lookup"><span data-stu-id="cb840-209">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="cb840-210">publisher</span><span class="sxs-lookup"><span data-stu-id="cb840-210">publisher</span></span> | <span data-ttu-id="cb840-211">Издатель образа виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cb840-211">Publisher of the VM image</span></span>
<span data-ttu-id="cb840-212">sku</span><span class="sxs-lookup"><span data-stu-id="cb840-212">sku</span></span> | <span data-ttu-id="cb840-213">Определенный номер SKU для образа виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cb840-213">Specific SKU for the VM image</span></span>  
<span data-ttu-id="cb840-214">версия</span><span class="sxs-lookup"><span data-stu-id="cb840-214">version</span></span> | <span data-ttu-id="cb840-215">Версия образа виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cb840-215">Version of the VM image</span></span> 
<span data-ttu-id="cb840-216">osType</span><span class="sxs-lookup"><span data-stu-id="cb840-216">osType</span></span> | <span data-ttu-id="cb840-217">Linux или Windows</span><span class="sxs-lookup"><span data-stu-id="cb840-217">Linux or Windows</span></span> 
<span data-ttu-id="cb840-218">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="cb840-218">platformUpdateDomain</span></span> |  <span data-ttu-id="cb840-219">[Домен обновления](virtual-machines-windows-manage-availability.md), на котором запущена виртуальная машина</span><span class="sxs-lookup"><span data-stu-id="cb840-219">[Update domain](virtual-machines-windows-manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="cb840-220">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="cb840-220">platformFaultDomain</span></span> | <span data-ttu-id="cb840-221">[Домен сбоя](virtual-machines-windows-manage-availability.md), на котором запущена виртуальная машина</span><span class="sxs-lookup"><span data-stu-id="cb840-221">[Fault domain](virtual-machines-windows-manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="cb840-222">vmId</span><span class="sxs-lookup"><span data-stu-id="cb840-222">vmId</span></span> | <span data-ttu-id="cb840-223">[Уникальный идентификатор](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cb840-223">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for the VM</span></span>
<span data-ttu-id="cb840-224">vmSize</span><span class="sxs-lookup"><span data-stu-id="cb840-224">vmSize</span></span> | [<span data-ttu-id="cb840-225">Размер виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cb840-225">VM size</span></span>](virtual-machines-windows-sizes.md)
<span data-ttu-id="cb840-226">ipv4/privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="cb840-226">ipv4/privateIpAddress</span></span> | <span data-ttu-id="cb840-227">Локальный IPv4-адрес виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cb840-227">Local IPv4 address of the VM</span></span> 
<span data-ttu-id="cb840-228">ipv4/publicIpAddress</span><span class="sxs-lookup"><span data-stu-id="cb840-228">ipv4/publicIpAddress</span></span> | <span data-ttu-id="cb840-229">Общедоступный IPv4-адрес виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cb840-229">Public IPv4 address of the VM</span></span>
<span data-ttu-id="cb840-230">subnet/address</span><span class="sxs-lookup"><span data-stu-id="cb840-230">subnet/address</span></span> | <span data-ttu-id="cb840-231">Адрес подсети виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cb840-231">Subnet address of the VM</span></span>
<span data-ttu-id="cb840-232">subnet/prefix</span><span class="sxs-lookup"><span data-stu-id="cb840-232">subnet/prefix</span></span> | <span data-ttu-id="cb840-233">Префикс подсети, пример 24</span><span class="sxs-lookup"><span data-stu-id="cb840-233">Subnet prefix, example 24</span></span>
<span data-ttu-id="cb840-234">ipv6/ipAddress</span><span class="sxs-lookup"><span data-stu-id="cb840-234">ipv6/ipAddress</span></span> | <span data-ttu-id="cb840-235">Локальный IPv6-адрес виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cb840-235">Local IPv6 address of the VM</span></span>
<span data-ttu-id="cb840-236">macAddress</span><span class="sxs-lookup"><span data-stu-id="cb840-236">macAddress</span></span> | <span data-ttu-id="cb840-237">Mac-адрес виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="cb840-237">VM mac address</span></span> 
<span data-ttu-id="cb840-238">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="cb840-238">scheduledevents</span></span> | <span data-ttu-id="cb840-239">Сейчас в общедоступной предварительной версии. Дополнительные сведения см. в статье [Служба метаданных Azure. Запланированные события (предварительная версия)](virtual-machines-scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="cb840-239">Currently in Public Preview See [scheduledevents](virtual-machines-scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="cb840-240">Примеры сценариев использования</span><span class="sxs-lookup"><span data-stu-id="cb840-240">Example Scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="cb840-241">Отслеживание виртуальной машины в Azure</span><span class="sxs-lookup"><span data-stu-id="cb840-241">Tracking VM running on Azure</span></span>

<span data-ttu-id="cb840-242">Поставщику услуг может потребоваться отслеживать количество виртуальных машин, использующих ваше программное обеспечение, или установить агенты, отслеживающие уникальность виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="cb840-242">As a service provider, you may require to track the number of VMs running your software or have agents that need to track uniqueness of the VM.</span></span> <span data-ttu-id="cb840-243">Чтобы получить уникальный идентификатор для виртуальной машины, используйте поле `vmId` службы метаданных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="cb840-243">To be able to get a unique ID for a VM, use the `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="cb840-244">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="cb840-244">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="cb840-245">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="cb840-245">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="cb840-246">Размещение контейнеров и секций данных на основе домена сбоя или обновления</span><span class="sxs-lookup"><span data-stu-id="cb840-246">Placement of containers, data-partitions based Fault/Update domain</span></span> 

<span data-ttu-id="cb840-247">В некоторых сценариях размещение разных реплик имеет первостепенное значение.</span><span class="sxs-lookup"><span data-stu-id="cb840-247">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="cb840-248">Например, для [размещения реплики HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) или размещения контейнера с помощью [оркестратора](https://kubernetes.io/docs/user-guide/node-selection/) необходимо знать домен сбоя `platformFaultDomain` и домен обновления `platformUpdateDomain`, на которых запущена виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="cb840-248">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require to know the `platformFaultDomain` and `platformUpdateDomain` the VM is running on.</span></span>
<span data-ttu-id="cb840-249">Вы можете запросить данные непосредственно через службу метаданных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="cb840-249">You can query this data directly via the Instance Metadata Service.</span></span>

<span data-ttu-id="cb840-250">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="cb840-250">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="cb840-251">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="cb840-251">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-the-vm-during-support-case"></a><span data-ttu-id="cb840-252">Получение дополнительных сведений о виртуальной машине при обращении в службу поддержки</span><span class="sxs-lookup"><span data-stu-id="cb840-252">Getting more information about the VM during support case</span></span> 

<span data-ttu-id="cb840-253">Чтобы получить дополнительные сведения о виртуальной машине, поставщик услуг может позвонить в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="cb840-253">As a service provider, you may get a support call where you would like to know more information about the VM.</span></span> <span data-ttu-id="cb840-254">Если клиент предоставит сведения о метаданных вычислений, специалист службы поддержки получит основные сведения о виртуальной машине в Azure.</span><span class="sxs-lookup"><span data-stu-id="cb840-254">Asking the customer to share the compute metadata can provide basic information for the support professional to know about the kind of VM on Azure.</span></span> 

<span data-ttu-id="cb840-255">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="cb840-255">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="cb840-256">**Ответ**</span><span class="sxs-lookup"><span data-stu-id="cb840-256">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="cb840-257">Ответ представляет собой строку JSON.</span><span class="sxs-lookup"><span data-stu-id="cb840-257">The response is a JSON string.</span></span> <span data-ttu-id="cb840-258">Следующие примеры ответов представлены в удобном для чтения формате.</span><span class="sxs-lookup"><span data-stu-id="cb840-258">The following example response is pretty-printed for readability.</span></span>

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-the-vm"></a><span data-ttu-id="cb840-259">Примеры вызова службы метаданных с использованием различных языков в виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="cb840-259">Examples of calling metadata service using different languages inside the VM</span></span> 

<span data-ttu-id="cb840-260">Язык</span><span class="sxs-lookup"><span data-stu-id="cb840-260">Language</span></span> | <span data-ttu-id="cb840-261">Пример</span><span class="sxs-lookup"><span data-stu-id="cb840-261">Example</span></span> 
---------|----------------
<span data-ttu-id="cb840-262">Ruby</span><span class="sxs-lookup"><span data-stu-id="cb840-262">Ruby</span></span>     | <span data-ttu-id="cb840-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span><span class="sxs-lookup"><span data-stu-id="cb840-263">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="cb840-264">Перейдите в локальную сеть</span><span class="sxs-lookup"><span data-stu-id="cb840-264">Go Lan</span></span>   | <span data-ttu-id="cb840-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="cb840-265">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="cb840-266">python</span><span class="sxs-lookup"><span data-stu-id="cb840-266">python</span></span>   | <span data-ttu-id="cb840-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span><span class="sxs-lookup"><span data-stu-id="cb840-267">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="cb840-268">C++</span><span class="sxs-lookup"><span data-stu-id="cb840-268">C++</span></span>      | <span data-ttu-id="cb840-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span><span class="sxs-lookup"><span data-stu-id="cb840-269">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="cb840-270">C#</span><span class="sxs-lookup"><span data-stu-id="cb840-270">C#</span></span>       | <span data-ttu-id="cb840-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span><span class="sxs-lookup"><span data-stu-id="cb840-271">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="cb840-272">JavaScript</span><span class="sxs-lookup"><span data-stu-id="cb840-272">Javascript</span></span> | <span data-ttu-id="cb840-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="cb840-273">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="cb840-274">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb840-274">Powershell</span></span> | <span data-ttu-id="cb840-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="cb840-275">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="cb840-276">Bash</span><span class="sxs-lookup"><span data-stu-id="cb840-276">Bash</span></span>       | <span data-ttu-id="cb840-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="cb840-277">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="cb840-278">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="cb840-278">FAQ</span></span>
1. <span data-ttu-id="cb840-279">Я получаю ошибку `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="cb840-279">I am getting the error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="cb840-280">Что это означает?</span><span class="sxs-lookup"><span data-stu-id="cb840-280">What does this mean?</span></span>
   * <span data-ttu-id="cb840-281">Для работы службы метаданных экземпляров заголовок `Metadata: true` необходимо передать в запрос.</span><span class="sxs-lookup"><span data-stu-id="cb840-281">The Instance Metadata Service requires the header `Metadata: true` to be passed in the request.</span></span> <span data-ttu-id="cb840-282">Передача заголовка в вызов REST позволяет получить доступ к службе метаданных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="cb840-282">Passing this header in the REST call allows access to the Instance Metadata Service.</span></span> 
2. <span data-ttu-id="cb840-283">Почему я не получаю сведения о вычислениях для виртуальной машины?</span><span class="sxs-lookup"><span data-stu-id="cb840-283">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="cb840-284">Сейчас служба метаданных экземпляров поддерживает только экземпляры, созданные с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cb840-284">Currently the Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="cb840-285">В будущем мы добавим поддержку виртуальных машин облачной службы.</span><span class="sxs-lookup"><span data-stu-id="cb840-285">In the future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="cb840-286">Виртуальная машина была недавно создана с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cb840-286">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="cb840-287">Почему не отображаются сведения о метаданных вычислений?</span><span class="sxs-lookup"><span data-stu-id="cb840-287">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="cb840-288">Чтобы отобразить метаданные вычислений для любой виртуальной машины, созданной после сентября 2016 года, необходимо добавить [тег](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="cb840-288">For any VMs created after Sep 2016, add a [Tag](../azure-resource-manager/resource-group-using-tags.md) to start seeing compute metadata.</span></span> <span data-ttu-id="cb840-289">Для обновления метаданных более старых виртуальных машин (созданных до сентября 2016 г.) удалите расширения или диски данных или добавьте их к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="cb840-289">For older VMs (created before Sep 2016), add/remove extensions or data disks to the VM to refresh metadata.</span></span>
4. <span data-ttu-id="cb840-290">Почему я получаю ошибку `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="cb840-290">Why am I getting the error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="cb840-291">Повторите запрос в зависимости от экспоненциальной системы.</span><span class="sxs-lookup"><span data-stu-id="cb840-291">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="cb840-292">Если проблема не исчезла, обратитесь в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="cb840-292">If the issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="cb840-293">Где можно задать дополнительные вопросы или оставить комментарии?</span><span class="sxs-lookup"><span data-stu-id="cb840-293">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="cb840-294">Оставьте комментарии на сайте http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="cb840-294">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="cb840-295">Будет ли это работать для экземпляра масштабируемого набора виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="cb840-295">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="cb840-296">Да, служба метаданных доступна для экземпляров масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="cb840-296">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="cb840-297">Как можно получить поддержку для службы?</span><span class="sxs-lookup"><span data-stu-id="cb840-297">How do I get support for the service?</span></span>
   * <span data-ttu-id="cb840-298">Чтобы получить поддержку для службы, зарегистрируйте проблему на портале Azure для виртуальной машины, в которой вы не можете получить ответ метаданных после нескольких долгих попыток</span><span class="sxs-lookup"><span data-stu-id="cb840-298">To get support for the service, create a support issue in Azure portal for the VM where you are not able to get metadata response after long retries</span></span> 

   ![Поддержка метаданных экземпляров](./media/virtual-machines-instancemetadataservice-overview/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="cb840-300">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cb840-300">Next Steps</span></span>

- <span data-ttu-id="cb840-301">Дополнительные сведения об API-интерфейсе [scheduledevents](virtual-machines-scheduled-events.md) **в общедоступной предварительной версии**, предоставляемом службой метаданных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="cb840-301">Learn more about the [scheduledevents](virtual-machines-scheduled-events.md) API **In Public Preview** provided by the Instance Metadata Service.</span></span>
