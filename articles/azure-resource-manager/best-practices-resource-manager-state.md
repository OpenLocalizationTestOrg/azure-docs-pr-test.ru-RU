---
title: "aaaPass сложных значений между шаблоны Azure | Документы Microsoft"
description: "Отображает рекомендуется подходов к использованию данных о состоянии tooshare сложные объекты с помощью шаблонов диспетчера ресурсов Azure и связанных шаблонов."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a><span data-ttu-id="0460c-103">Tooand состояния общего ресурса на основе шаблонов диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="0460c-103">Share state tooand from Azure Resource Manager templates</span></span>
<span data-ttu-id="0460c-104">В этой статье приводятся рекомендации по управлению и совместному использованию состояния в шаблонах.</span><span class="sxs-lookup"><span data-stu-id="0460c-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="0460c-105">Hello параметры и переменные, приведенные в этом разделе приведены примеры hello типов объектов, можно определить tooconveniently организовать требований к развертыванию.</span><span class="sxs-lookup"><span data-stu-id="0460c-105">hello parameters and variables shown in this topic are examples of hello type of objects you can define tooconveniently organize your deployment requirements.</span></span> <span data-ttu-id="0460c-106">На основе этих примеров можно реализовать собственные объекты со значениями свойств, которые имеют смысл для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="0460c-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="0460c-107">Данная тема является частью другого технического документа.</span><span class="sxs-lookup"><span data-stu-id="0460c-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="0460c-108">загрузить полной бумага hello tooread [вопросы World класс ресурса диспетчера шаблонов и проверенные методики](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span><span class="sxs-lookup"><span data-stu-id="0460c-108">tooread hello full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="0460c-109">Указание стандартных параметров конфигурации</span><span class="sxs-lookup"><span data-stu-id="0460c-109">Provide standard configuration settings</span></span>
<span data-ttu-id="0460c-110">А не реализует шаблон, который обеспечивает общее гибкость и множество вариантов, распространенный подход заключается в tooprovide набора известных конфигураций.</span><span class="sxs-lookup"><span data-stu-id="0460c-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is tooprovide a selection of known configurations.</span></span> <span data-ttu-id="0460c-111">Фактически размеры песочницы определяются по аналогии со стандартными размерами футболки (малый, средний и большой).</span><span class="sxs-lookup"><span data-stu-id="0460c-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="0460c-112">Другие примеры использования этого подхода включают такие продукты, как Community Edition или Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="0460c-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="0460c-113">Другие случаи могут быть представлены конфигурациями технологий, зависящими от рабочей нагрузки, включая решения Map/Reduce или NoSQL.</span><span class="sxs-lookup"><span data-stu-id="0460c-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="0460c-114">С сложные объекты можно создать переменные, содержащие наборы данных, которую иногда называют «контейнеры свойств» и использовать ресурс объявления hello этого toodrive данных в шаблон.</span><span class="sxs-lookup"><span data-stu-id="0460c-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data toodrive hello resource declaration in your template.</span></span> <span data-ttu-id="0460c-115">Такой подход позволяет использовать хорошие и известные конфигурации разных размеров, предварительно настроенные для клиентов.</span><span class="sxs-lookup"><span data-stu-id="0460c-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="0460c-116">Без известной конфигурации пользователей hello шаблона необходимо определить изменения размера кластера на собственные, фактором ограничения ресурсов платформы и выполнять математические tooidentify hello возникающие секционирование учетные записи хранения и другие ресурсы (из-за размера toocluster и ограничения ресурсов).</span><span class="sxs-lookup"><span data-stu-id="0460c-116">Without known configurations, users of hello template must determine cluster sizing on their own, factor in platform resource constraints, and do math tooidentify hello resulting partitioning of storage accounts and other resources (due toocluster size and resource constraints).</span></span> <span data-ttu-id="0460c-117">Кроме toomaking для повышения удобства для клиента hello несколько известных конфигураций, проще toosupport и может помочь вам предоставлять более высокий уровень плотности.</span><span class="sxs-lookup"><span data-stu-id="0460c-117">In addition toomaking a better experience for hello customer, a few known configurations are easier toosupport and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="0460c-118">Следующий пример показывает как Hello toodefine переменных, содержащих сложные объекты для представления коллекции данных.</span><span class="sxs-lookup"><span data-stu-id="0460c-118">hello following example shows how toodefine variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="0460c-119">коллекции Hello определяют значения, используемые для размера виртуальной машины, параметры сети, параметры операционной системы и доступности.</span><span class="sxs-lookup"><span data-stu-id="0460c-119">hello collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

<span data-ttu-id="0460c-120">Обратите внимание, что hello **tshirtSize** переменной Сцепляет hello размер футболки, предоставляемые через параметр (**небольшой**, **Средний**, **большой**) текст toohello **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="0460c-120">Notice that hello **tshirtSize** variable concatenates hello t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) toohello text **tshirtSize**.</span></span> <span data-ttu-id="0460c-121">Эта переменная связанного сложный объект переменной tooretrieve hello используется для такой размер футболки.</span><span class="sxs-lookup"><span data-stu-id="0460c-121">You use this variable tooretrieve hello associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="0460c-122">Затем можно ссылаться на эти переменные позже в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="0460c-122">You can then reference these variables later in hello template.</span></span> <span data-ttu-id="0460c-123">Hello возможность tooreference с именем переменных и их свойства упрощает синтаксис шаблона hello и делает его легко toounderstand контекста.</span><span class="sxs-lookup"><span data-stu-id="0460c-123">hello ability tooreference named-variables and their properties simplifies hello template syntax, and makes it easy toounderstand context.</span></span> <span data-ttu-id="0460c-124">Следующий пример Hello определяет toodeploy ресурсов с помощью объектов hello, показанному ранее tooset значения.</span><span class="sxs-lookup"><span data-stu-id="0460c-124">hello following example defines a resource toodeploy by using hello objects shown previously tooset values.</span></span> <span data-ttu-id="0460c-125">Например, hello размер виртуальной Машины будет задано, получая значение hello `variables('tshirtSize').vmSize` while hello значение для hello места на диске, извлекается из `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="0460c-125">For example, hello VM size is set by retrieving hello value for `variables('tshirtSize').vmSize` while hello value for hello disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="0460c-126">Кроме того, hello URI для связанного шаблона задается значением hello для `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="0460c-126">In addition, hello URI for a linked template is set with hello value for `variables('tshirtSize').vmTemplate`.</span></span>

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-tooa-template"></a><span data-ttu-id="0460c-127">Передать состояние tooa шаблона</span><span class="sxs-lookup"><span data-stu-id="0460c-127">Pass state tooa template</span></span>
<span data-ttu-id="0460c-128">Общий доступ к состоянию в шаблоне предоставляется с помощью параметров, которые вы указываете во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="0460c-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="0460c-129">Здравствуйте, следуя таблице перечислены часто используемые параметры в шаблонах.</span><span class="sxs-lookup"><span data-stu-id="0460c-129">hello following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="0460c-130">Имя</span><span class="sxs-lookup"><span data-stu-id="0460c-130">Name</span></span> | <span data-ttu-id="0460c-131">Значение</span><span class="sxs-lookup"><span data-stu-id="0460c-131">Value</span></span> | <span data-ttu-id="0460c-132">Описание</span><span class="sxs-lookup"><span data-stu-id="0460c-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0460c-133">location</span><span class="sxs-lookup"><span data-stu-id="0460c-133">location</span></span> |<span data-ttu-id="0460c-134">Строка из ограниченного списка регионов Azure</span><span class="sxs-lookup"><span data-stu-id="0460c-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="0460c-135">Hello расположение, где развернуты ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="0460c-135">hello location where hello resources are deployed.</span></span> |
| <span data-ttu-id="0460c-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="0460c-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="0460c-137">Строка</span><span class="sxs-lookup"><span data-stu-id="0460c-137">String</span></span> |<span data-ttu-id="0460c-138">Уникальное имя DNS для учетной записи хранилища, там, где размещены диски ВМ hello hello</span><span class="sxs-lookup"><span data-stu-id="0460c-138">Unique DNS name for hello Storage Account where hello VM's disks are placed</span></span> |
| <span data-ttu-id="0460c-139">domainName</span><span class="sxs-lookup"><span data-stu-id="0460c-139">domainName</span></span> |<span data-ttu-id="0460c-140">Строка</span><span class="sxs-lookup"><span data-stu-id="0460c-140">String</span></span> |<span data-ttu-id="0460c-141">Имя домена общедоступный jumpbox hello виртуальной Машины в формате hello: **{domainName}. {} расположение}.cloudapp.com** пример: **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="0460c-141">Domain name of hello publicly accessible jumpbox VM in hello format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="0460c-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="0460c-142">adminUsername</span></span> |<span data-ttu-id="0460c-143">Строка</span><span class="sxs-lookup"><span data-stu-id="0460c-143">String</span></span> |<span data-ttu-id="0460c-144">Имя пользователя для hello виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="0460c-144">Username for hello VMs</span></span> |
| <span data-ttu-id="0460c-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="0460c-145">adminPassword</span></span> |<span data-ttu-id="0460c-146">Строка</span><span class="sxs-lookup"><span data-stu-id="0460c-146">String</span></span> |<span data-ttu-id="0460c-147">Пароль для hello виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="0460c-147">Password for hello VMs</span></span> |
| <span data-ttu-id="0460c-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="0460c-148">tshirtSize</span></span> |<span data-ttu-id="0460c-149">Строка из ограниченного списка предлагаемых размеров</span><span class="sxs-lookup"><span data-stu-id="0460c-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="0460c-150">Здравствуйте, с именем tooprovision размер единицы масштабирования.</span><span class="sxs-lookup"><span data-stu-id="0460c-150">hello named scale unit size tooprovision.</span></span> <span data-ttu-id="0460c-151">Например, Small, Medium, Large</span><span class="sxs-lookup"><span data-stu-id="0460c-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="0460c-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="0460c-152">virtualNetworkName</span></span> |<span data-ttu-id="0460c-153">Строка</span><span class="sxs-lookup"><span data-stu-id="0460c-153">String</span></span> |<span data-ttu-id="0460c-154">Имя виртуальной сети hello, hello потребитель хочет toouse.</span><span class="sxs-lookup"><span data-stu-id="0460c-154">Name of hello virtual network that hello consumer wants toouse.</span></span> |
| <span data-ttu-id="0460c-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="0460c-155">enableJumpbox</span></span> |<span data-ttu-id="0460c-156">Строка из ограниченного списка (enabled, disabled)</span><span class="sxs-lookup"><span data-stu-id="0460c-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="0460c-157">Параметр, определяющий ли tooenable jumpbox для hello среды.</span><span class="sxs-lookup"><span data-stu-id="0460c-157">Parameter that identifies whether tooenable a jumpbox for hello environment.</span></span> <span data-ttu-id="0460c-158">Значения: enabled, disabled</span><span class="sxs-lookup"><span data-stu-id="0460c-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="0460c-159">Hello **tshirtSize** параметр, используемый в предыдущем разделе hello определяется как:</span><span class="sxs-lookup"><span data-stu-id="0460c-159">hello **tshirtSize** parameter used in hello previous section is defined as:</span></span>

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a><span data-ttu-id="0460c-160">Передать состояние toolinked шаблонов</span><span class="sxs-lookup"><span data-stu-id="0460c-160">Pass state toolinked templates</span></span>
<span data-ttu-id="0460c-161">При подключении toolinked шаблоны, часто использовать как статический, созданные переменные.</span><span class="sxs-lookup"><span data-stu-id="0460c-161">When connecting toolinked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="0460c-162">Статические переменные</span><span class="sxs-lookup"><span data-stu-id="0460c-162">Static variables</span></span>
<span data-ttu-id="0460c-163">Статические переменные чаще используется tooprovide базового значения, такие как URL-адреса, которые используются в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="0460c-163">Static variables are often used tooprovide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="0460c-164">В следующий фрагмент шаблона hello `templateBaseUrl` указывает hello корневой путь для шаблона hello в GitHub.</span><span class="sxs-lookup"><span data-stu-id="0460c-164">In hello following template excerpt, `templateBaseUrl` specifies hello root location for hello template in GitHub.</span></span> <span data-ttu-id="0460c-165">Следующая строка Hello создает новую переменную `sharedTemplateUrl` , объединяет hello базовый URL-адрес с известным именем hello hello общих ресурсов шаблона.</span><span class="sxs-lookup"><span data-stu-id="0460c-165">hello next line builds a new variable `sharedTemplateUrl` that concatenates hello base URL with hello known name of hello shared resources template.</span></span> <span data-ttu-id="0460c-166">Ниже этой линии сложный объект переменной находится используется toostore размер футболки, базовый URL-адрес hello сцепленные toohello известно расположение шаблонов конфигурации и хранятся в hello `vmTemplate` свойство.</span><span class="sxs-lookup"><span data-stu-id="0460c-166">Below that line, a complex object variable is used toostore a t-shirt size, where hello base URL is concatenated toohello known configuration template location and stored in hello `vmTemplate` property.</span></span>

<span data-ttu-id="0460c-167">Преимущество этого подхода Hello —, если изменяется расположение шаблонов hello, достаточно лишь toochange hello статической переменной в одном месте, который передает его на протяжении hello связанных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="0460c-167">hello benefit of this approach is that if hello template location changes, you only need toochange hello static variable in one place, which passes it throughout hello linked templates.</span></span>

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a><span data-ttu-id="0460c-168">Создаваемые переменные</span><span class="sxs-lookup"><span data-stu-id="0460c-168">Generated variables</span></span>
<span data-ttu-id="0460c-169">В переменных toostatic сложения динамически создаются несколько переменных.</span><span class="sxs-lookup"><span data-stu-id="0460c-169">In addition toostatic variables, several variables are generated dynamically.</span></span> <span data-ttu-id="0460c-170">В этом разделе определяет некоторые из распространенных типов hello созданный переменных.</span><span class="sxs-lookup"><span data-stu-id="0460c-170">This section identifies some of hello common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="0460c-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="0460c-171">tshirtSize</span></span>
<span data-ttu-id="0460c-172">Вы знакомы с этой переменной, созданный из вышеприведенных примерах hello.</span><span class="sxs-lookup"><span data-stu-id="0460c-172">You are familiar with this generated variable from hello examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="0460c-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="0460c-173">networkSettings</span></span>
<span data-ttu-id="0460c-174">В емкости, возможностей или решение с областью начала до конца шаблона, hello связанных шаблонов обычно Создание ресурсов, которые существуют в сети.</span><span class="sxs-lookup"><span data-stu-id="0460c-174">In a capacity, capability, or end-to-end scoped solution template, hello linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="0460c-175">Один простой подход является toouse параметров сети toostore сложный объект и передавать их toolinked шаблонов.</span><span class="sxs-lookup"><span data-stu-id="0460c-175">One straightforward approach is toouse a complex object toostore network settings and pass them toolinked templates.</span></span>

<span data-ttu-id="0460c-176">Ниже приведен пример взаимодействующих сетевых параметров.</span><span class="sxs-lookup"><span data-stu-id="0460c-176">An example of communicating network settings can be seen below.</span></span>

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a><span data-ttu-id="0460c-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="0460c-177">availabilitySettings</span></span>
<span data-ttu-id="0460c-178">Ресурсы, созданные в связанных шаблонах, часто помещаются в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="0460c-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="0460c-179">В следующем примере hello имя набора доступности hello указан и также hello домен сбоя и обновление домена toouse число.</span><span class="sxs-lookup"><span data-stu-id="0460c-179">In hello following example, hello availability set name is specified and also hello fault domain and update domain count toouse.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="0460c-180">Если требуется несколько групп доступности (например, один для главных узлов), а другой для узлов данных можно использовать имя с префиксом, указать несколько наборов доступности или выполните hello модели приведенный выше, для создания переменной для определенного размера футболки.</span><span class="sxs-lookup"><span data-stu-id="0460c-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow hello model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="0460c-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="0460c-181">storageSettings</span></span>
<span data-ttu-id="0460c-182">Информация о хранилище часто совместно используется со связанными шаблонами.</span><span class="sxs-lookup"><span data-stu-id="0460c-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="0460c-183">В следующем примере hello *storageSettings* объект предоставляет сведения о hello имена учетной записи и контейнера хранилища.</span><span class="sxs-lookup"><span data-stu-id="0460c-183">In hello example below, a *storageSettings* object provides details about hello storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="0460c-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="0460c-184">osSettings</span></span>
<span data-ttu-id="0460c-185">С помощью связанных шаблонов может понадобиться типы узлов toovarious параметры операционной системы toopass через различные известные типы конфигураций.</span><span class="sxs-lookup"><span data-stu-id="0460c-185">With linked templates, you may need toopass operating system settings toovarious nodes types across different known configuration types.</span></span> <span data-ttu-id="0460c-186">Сложный объект информационное легко toostore и общую папку операционной системы, а также делает проще toosupport множественный выбор операционной системы для развертывания.</span><span class="sxs-lookup"><span data-stu-id="0460c-186">A complex object is an easy way toostore and share operating system information and also makes it easier toosupport multiple operating system choices for deployment.</span></span>

<span data-ttu-id="0460c-187">Hello пример объекта для *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="0460c-187">hello following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="0460c-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="0460c-188">machineSettings</span></span>
<span data-ttu-id="0460c-189">Создаваемая переменная *machineSettings* представляет собой составной объект, содержащий набор основных переменных для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0460c-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="0460c-190">переменные Hello включают имя пользователя администратора и пароль, префикс для имен виртуальных Машин hello и ссылка на изображение операционной системы.</span><span class="sxs-lookup"><span data-stu-id="0460c-190">hello variables include administrator user name and password, a prefix for hello VM names, and an operating system image reference.</span></span>

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

<span data-ttu-id="0460c-191">Обратите внимание, что *osImageReference* Здравствуйте, извлекает значения из hello *osSettings* переменную, заданную в главном шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="0460c-191">Note that *osImageReference* retrieves hello values from hello *osSettings* variable defined in hello main template.</span></span> <span data-ttu-id="0460c-192">Это означает, что можно легко изменить hello операционной системы для виртуальной Машины — полностью или в зависимости от предпочтений hello шаблон потребителя.</span><span class="sxs-lookup"><span data-stu-id="0460c-192">That means you can easily change hello operating system for a VM—entirely or based on hello preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="0460c-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="0460c-193">vmScripts</span></span>
<span data-ttu-id="0460c-194">Hello *vmScripts* объекта содержит подробные сведения о сценарии toodownload hello и выполнить на экземпляре виртуальной Машины, включая внешней и внутренней ссылки.</span><span class="sxs-lookup"><span data-stu-id="0460c-194">hello *vmScripts* object contains details about hello scripts toodownload and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="0460c-195">За пределами ссылки включать hello инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="0460c-195">Outside references include hello infrastructure.</span></span>
<span data-ttu-id="0460c-196">Ссылки внутри включать hello установлено программное обеспечение и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0460c-196">Inside references include hello installed software installed and configuration.</span></span>

<span data-ttu-id="0460c-197">Использовать hello *scriptsToDownload* свойство toolist hello скрипты toodownload toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0460c-197">You use hello *scriptsToDownload* property toolist hello scripts toodownload toohello VM.</span></span> <span data-ttu-id="0460c-198">Этот объект также содержит ссылки на toocommand строки для различных типов действий.</span><span class="sxs-lookup"><span data-stu-id="0460c-198">This object also contains references toocommand-line arguments for different types of actions.</span></span> <span data-ttu-id="0460c-199">Эти действия включают выполнение hello установки по умолчанию для каждого отдельного узла, установки, выполняемый после развертывания все узлы и любые дополнительные сценарии, которые могут быть конкретных tooa заданный шаблон.</span><span class="sxs-lookup"><span data-stu-id="0460c-199">These actions include executing hello default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific tooa given template.</span></span>

<span data-ttu-id="0460c-200">Этот пример взят из шаблона, который использовался toodeploy MongoDB, требующий арбитр toodeliver высокого уровня доступности.</span><span class="sxs-lookup"><span data-stu-id="0460c-200">This example is from a template used toodeploy MongoDB, which requires an arbiter toodeliver high availability.</span></span> <span data-ttu-id="0460c-201">Hello *arbiterNodeInstallCommand* добавлено слишком*vmScripts* tooinstall арбитр hello.</span><span class="sxs-lookup"><span data-stu-id="0460c-201">hello *arbiterNodeInstallCommand* has been added too*vmScripts* tooinstall hello arbiter.</span></span>

<span data-ttu-id="0460c-202">раздел Hello переменные — где найти hello переменные, которые определяют скрипт hello tooexecute hello определенного текста с использованием соответствующих значений hello.</span><span class="sxs-lookup"><span data-stu-id="0460c-202">hello variables section is where you find hello variables that define hello specific text tooexecute hello script with hello proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="0460c-203">Возвращение состояния из шаблона</span><span class="sxs-lookup"><span data-stu-id="0460c-203">Return state from a template</span></span>
<span data-ttu-id="0460c-204">Не только передавать данные в виде шаблона, вы также можете шаблон вызывающий задней toohello данных общей папки.</span><span class="sxs-lookup"><span data-stu-id="0460c-204">Not only can you pass data into a template, you can also share data back toohello calling template.</span></span> <span data-ttu-id="0460c-205">В hello **выводит** раздел связанного шаблона, можно указать пары "ключ значение", который может быть использован hello исходный шаблон.</span><span class="sxs-lookup"><span data-stu-id="0460c-205">In hello **outputs** section of a linked template, you can provide key/value pairs that can be consumed by hello source template.</span></span>

<span data-ttu-id="0460c-206">Hello следующем примере показано, как toopass hello частный IP-адрес, созданный в связанного шаблона.</span><span class="sxs-lookup"><span data-stu-id="0460c-206">hello following example shows how toopass hello private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="0460c-207">В главном шаблоне hello можно использовать эти данные hello, используя синтаксис:</span><span class="sxs-lookup"><span data-stu-id="0460c-207">Within hello main template, you can use that data with hello following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="0460c-208">Можно использовать это выражение в разделе выходы hello или раздел ресурсов hello hello основного шаблона.</span><span class="sxs-lookup"><span data-stu-id="0460c-208">You can use this expression in either hello outputs section or hello resources section of hello main template.</span></span> <span data-ttu-id="0460c-209">Нельзя использовать выражение hello в разделе "переменные" hello, поскольку он зависит от состояния выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="0460c-209">You cannot use hello expression in hello variables section because it relies on hello runtime state.</span></span> <span data-ttu-id="0460c-210">tooreturn это значение из основного шаблона hello, используйте:</span><span class="sxs-lookup"><span data-stu-id="0460c-210">tooreturn this value from hello main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="0460c-211">Пример использования hello выводит раздел дисков данных tooreturn связанного шаблона, для виртуальной машины, см. в разделе [Создание несколько дисков данных для виртуальной машины](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="0460c-211">For an example of using hello outputs section of a linked template tooreturn data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="0460c-212">Определение параметров проверки подлинности для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0460c-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="0460c-213">Можно использовать hello же шаблону, показанному ранее для параметров проверки подлинности hello toospecify параметры конфигурации для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0460c-213">You can use hello same pattern shown previously for configuration settings toospecify hello authentication settings for a virtual machine.</span></span> <span data-ttu-id="0460c-214">Создание параметра для передачи в hello тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="0460c-214">You create a parameter for passing in hello type of authentication.</span></span>

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

<span data-ttu-id="0460c-215">Можно добавить переменные для hello различные типы проверки подлинности и переменной toostore, какой тип используется для развертывания на основе значения параметра hello hello.</span><span class="sxs-lookup"><span data-stu-id="0460c-215">You add variables for hello different authentication types, and a variable toostore which type is used for this deployment based on hello value of hello parameter.</span></span>

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

<span data-ttu-id="0460c-216">При определении hello виртуальной машины, можно задать hello **osProfile** toohello переменной, созданной.</span><span class="sxs-lookup"><span data-stu-id="0460c-216">When defining hello virtual machine, you set hello **osProfile** toohello variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="0460c-217">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0460c-217">Next steps</span></span>
* <span data-ttu-id="0460c-218">toolearn о разделах hello шаблона hello. в разделе [разработки шаблонов диспетчера ресурсов Azure](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="0460c-218">toolearn about hello sections of hello template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="0460c-219">toosee hello функций, доступных в шаблоне, в разделе [функции шаблона диспетчера ресурсов Azure](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="0460c-219">toosee hello functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
