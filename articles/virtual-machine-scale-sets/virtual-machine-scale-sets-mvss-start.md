---
title: "aaaLearn о масштабирования виртуальных машин выбирать шаблоны | Документы Microsoft"
description: "Дополнительные сведения toocreate Минимальный масштаб допустимого набора шаблона для набора масштабирования виртуальной машины"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a><span data-ttu-id="e1352-103">Подробнее о шаблонах масштабируемых наборов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e1352-103">Learn about virtual machine scale set templates</span></span>
<span data-ttu-id="e1352-104">[Шаблоны Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) — toodeploy хорошим способом группы связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e1352-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="e1352-105">Этот учебник, показывающие, как toocreate Минимальный масштаб допустимого шаблона набора и как toomodify этот шаблон toosuit различных сценариев.</span><span class="sxs-lookup"><span data-stu-id="e1352-105">This tutorial series shows how toocreate a minimum viable scale set template and how toomodify this template toosuit various scenarios.</span></span> <span data-ttu-id="e1352-106">Все примеры взяты из этого [репозитория GitHub](https://github.com/gatneil/mvss).</span><span class="sxs-lookup"><span data-stu-id="e1352-106">All examples come from this [GitHub repository](https://github.com/gatneil/mvss).</span></span> 

<span data-ttu-id="e1352-107">Этот шаблон является предполагаемым toobe простой.</span><span class="sxs-lookup"><span data-stu-id="e1352-107">This template is intended toobe simple.</span></span> <span data-ttu-id="e1352-108">Более полные примеры шкалы набор шаблонов см. в разделе hello [репозитории GitHub шаблоны быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates) и выполните поиск папок, содержащих строку hello `vmss`.</span><span class="sxs-lookup"><span data-stu-id="e1352-108">For more complete examples of scale set templates, see hello [Azure Quickstart Templates GitHub repository](https://github.com/Azure/azure-quickstart-templates) and search for folders that contain hello string `vmss`.</span></span>

<span data-ttu-id="e1352-109">Если вы уже знакомы с созданием шаблоны, можно пропустить toohello toosee раздел «Дальнейшие действия» как toomodify этот шаблон.</span><span class="sxs-lookup"><span data-stu-id="e1352-109">If you are already familiar with creating templates, you can skip toohello "Next steps" section toosee how toomodify this template.</span></span>

## <a name="review-hello-template"></a><span data-ttu-id="e1352-110">Шаблон проверке hello</span><span class="sxs-lookup"><span data-stu-id="e1352-110">Review hello template</span></span>

<span data-ttu-id="e1352-111">Использовать GitHub tooreview шаблона, набора наши Минимальный масштаб реальную [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="e1352-111">Use GitHub tooreview our minimum viable scale set template, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).</span></span>

<span data-ttu-id="e1352-112">В этом учебнике мы изучаем hello diff (`git diff master minimum-viable-scale-set`) toocreate hello минимальное работало в наборе шаблона по частям.</span><span class="sxs-lookup"><span data-stu-id="e1352-112">In this tutorial, we examine hello diff (`git diff master minimum-viable-scale-set`) toocreate hello minimum viable scale set template piece by piece.</span></span>

## <a name="define-schema-and-contentversion"></a><span data-ttu-id="e1352-113">Определение элементов $schema и contentVersion</span><span class="sxs-lookup"><span data-stu-id="e1352-113">Define $schema and contentVersion</span></span>
<span data-ttu-id="e1352-114">Во-первых, определим `$schema` и `contentVersion` в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="e1352-114">First, we define `$schema` and `contentVersion` in hello template.</span></span> <span data-ttu-id="e1352-115">Hello `$schema` элемент определяет версию hello языка шаблона hello и используется для выделения синтаксиса в Visual Studio и другие аналогичные возможности проверки.</span><span class="sxs-lookup"><span data-stu-id="e1352-115">hello `$schema` element defines hello version of hello template language and is used for Visual Studio syntax highlighting and similar validation features.</span></span> <span data-ttu-id="e1352-116">Hello `contentVersion` элемент не используется в Azure.</span><span class="sxs-lookup"><span data-stu-id="e1352-116">hello `contentVersion` element is not used by Azure.</span></span> <span data-ttu-id="e1352-117">Вместо этого он позволяет хранить список версия шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="e1352-117">Instead, it helps you keep track of hello template version.</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a><span data-ttu-id="e1352-118">Определение параметров</span><span class="sxs-lookup"><span data-stu-id="e1352-118">Define parameters</span></span>
<span data-ttu-id="e1352-119">Далее мы определим два параметра: `adminUsername` и `adminPassword`.</span><span class="sxs-lookup"><span data-stu-id="e1352-119">Next, we define two parameters, `adminUsername` and `adminPassword`.</span></span> <span data-ttu-id="e1352-120">Параметры являются значениями, задаваемыми во время развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="e1352-120">Parameters are values you specify at hello time of deployment.</span></span> <span data-ttu-id="e1352-121">Hello `adminUsername` параметр является просто `string` типа, но поскольку `adminPassword` такое секрет, мы отправляем тип `securestring`.</span><span class="sxs-lookup"><span data-stu-id="e1352-121">hello `adminUsername` parameter is simply a `string` type, but because `adminPassword` is a secret, we give it type `securestring`.</span></span> <span data-ttu-id="e1352-122">Более поздней версии эти параметры передаются в конфигурацию набора масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="e1352-122">Later, these parameters are passed into hello scale set configuration.</span></span>

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a><span data-ttu-id="e1352-123">Определение переменных</span><span class="sxs-lookup"><span data-stu-id="e1352-123">Define variables</span></span>
<span data-ttu-id="e1352-124">Шаблоны диспетчера ресурсов также позволяют определить toobe переменных, используемых в дальнейшем в шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="e1352-124">Resource Manager templates also let you define variables toobe used later in hello template.</span></span> <span data-ttu-id="e1352-125">Поэтому мы оставили hello объекта JSON пустым в нашем примере не используется любые переменные.</span><span class="sxs-lookup"><span data-stu-id="e1352-125">Our example doesn't use any variables, so we've left hello JSON object empty.</span></span>

```json
  "variables": {},
```

## <a name="define-resources"></a><span data-ttu-id="e1352-126">Определение ресурсов</span><span class="sxs-lookup"><span data-stu-id="e1352-126">Define resources</span></span>
<span data-ttu-id="e1352-127">Далее следует hello раздел ресурсов шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="e1352-127">Next is hello resources section of hello template.</span></span> <span data-ttu-id="e1352-128">Здесь, определить, действительно требуется toodeploy.</span><span class="sxs-lookup"><span data-stu-id="e1352-128">Here, you define what you actually want toodeploy.</span></span> <span data-ttu-id="e1352-129">В отличие от разделов `parameters` и `variables`, которые сами являются объектами JSON, раздел `resources` представляет собой JSON-список объектов JSON.</span><span class="sxs-lookup"><span data-stu-id="e1352-129">Unlike `parameters` and `variables` (which are JSON objects), `resources` is a JSON list of JSON objects.</span></span>

```json
   "resources": [
```

<span data-ttu-id="e1352-130">Каждый ресурс должен иметь свойства `type`, `name`, `apiVersion` и `location`.</span><span class="sxs-lookup"><span data-stu-id="e1352-130">All resources require `type`, `name`, `apiVersion`, and `location` properties.</span></span> <span data-ttu-id="e1352-131">В этом примере для первого ресурса указан тип `Microsft.Network/virtualNetwork`, имя `myVnet` и версия API `2016-03-30`.</span><span class="sxs-lookup"><span data-stu-id="e1352-131">This example's first resource has type `Microsft.Network/virtualNetwork`, name `myVnet`, and apiVersion `2016-03-30`.</span></span> <span data-ttu-id="e1352-132">(toofind hello последнюю версию API для типа ресурса в разделе hello [документация по Azure REST API](https://docs.microsoft.com/rest/api/).)</span><span class="sxs-lookup"><span data-stu-id="e1352-132">(toofind hello latest API version for a resource type, see hello [Azure REST API documentation](https://docs.microsoft.com/rest/api/).)</span></span>

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a><span data-ttu-id="e1352-133">Определение расположения</span><span class="sxs-lookup"><span data-stu-id="e1352-133">Specify location</span></span>
<span data-ttu-id="e1352-134">расположение hello toospecify hello виртуальной сети, мы используем [функции шаблона диспетчера ресурсов](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="e1352-134">toospecify hello location for hello virtual network, we use a [Resource Manager template function](../azure-resource-manager/resource-group-template-functions.md).</span></span> <span data-ttu-id="e1352-135">Каждая функция заключается в кавычки и квадратные скобки, примерно так: `"[<template-function>]"`.</span><span class="sxs-lookup"><span data-stu-id="e1352-135">This function must be enclosed in quotes and square brackets like this: `"[<template-function>]"`.</span></span> <span data-ttu-id="e1352-136">В этом случае мы используем hello `resourceGroup` функции.</span><span class="sxs-lookup"><span data-stu-id="e1352-136">In this case, we use hello `resourceGroup` function.</span></span> <span data-ttu-id="e1352-137">Он принимает аргументы и возвращает объект JSON, содержащий метаданные о группе ресурсов hello, развертывания для этого развертывания.</span><span class="sxs-lookup"><span data-stu-id="e1352-137">It takes in no arguments and returns a JSON object with metadata about hello resource group this deployment is being deployed to.</span></span> <span data-ttu-id="e1352-138">Группа ресурсов Hello задается пользователем hello во время hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="e1352-138">hello resource group is set by hello user at hello time of deployment.</span></span> <span data-ttu-id="e1352-139">Мы затем индекс в этот объект JSON с `.location` tooget hello, откуда hello объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="e1352-139">We then index into this JSON object with `.location` tooget hello location from hello JSON object.</span></span>

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a><span data-ttu-id="e1352-140">Определение свойств виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="e1352-140">Specify virtual network properties</span></span>
<span data-ttu-id="e1352-141">Каждый диспетчер ресурсов ресурс имеет свой собственный `properties` раздела для ресурса toohello определенных конфигураций.</span><span class="sxs-lookup"><span data-stu-id="e1352-141">Each Resource Manager resource has its own `properties` section for configurations specific toohello resource.</span></span> <span data-ttu-id="e1352-142">В этом случае мы указываем hello виртуальной сети должен иметь одну подсеть hello диапазон частных IP-адресов с помощью `10.0.0.0/16`.</span><span class="sxs-lookup"><span data-stu-id="e1352-142">In this case, we specify that hello virtual network should have one subnet using hello private IP address range `10.0.0.0/16`.</span></span> <span data-ttu-id="e1352-143">Масштабируемый набор всегда содержится в одной подсети.</span><span class="sxs-lookup"><span data-stu-id="e1352-143">A scale set is always contained within one subnet.</span></span> <span data-ttu-id="e1352-144">Он не может охватывать подсети.</span><span class="sxs-lookup"><span data-stu-id="e1352-144">It cannot span subnets.</span></span>

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a><span data-ttu-id="e1352-145">Добавление списка зависимостей (dependsOn)</span><span class="sxs-lookup"><span data-stu-id="e1352-145">Add dependsOn list</span></span>
<span data-ttu-id="e1352-146">В дополнение к этому требуется toohello `type`, `name`, `apiVersion`, и `location` свойства каждого ресурса может иметь дополнительный `dependsOn` список строк.</span><span class="sxs-lookup"><span data-stu-id="e1352-146">In addition toohello required `type`, `name`, `apiVersion`, and `location` properties, each resource can have an optional `dependsOn` list of strings.</span></span> <span data-ttu-id="e1352-147">Этот список определяет, какие еще ресурсы из текущего развертывания необходимо создать перед развертыванием этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="e1352-147">This list specifies which other resources from this deployment must finish before deploying this resource.</span></span>

<span data-ttu-id="e1352-148">В этом случае есть только один элемент в списке hello hello виртуальной сети из предыдущего примера hello.</span><span class="sxs-lookup"><span data-stu-id="e1352-148">In this case, there is only one element in hello list, hello virtual network from hello previous example.</span></span> <span data-ttu-id="e1352-149">Мы указать эту зависимость, поскольку hello в наборе потребностей сети tooexist hello перед созданием все виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="e1352-149">We specify this dependency because hello scale set needs hello network tooexist before creating any VMs.</span></span> <span data-ttu-id="e1352-150">Таким образом, набор масштабирования hello можно предоставить эти виртуальные машины частных IP-адресов из диапазона IP-адресов hello, указанные в свойствах сети hello.</span><span class="sxs-lookup"><span data-stu-id="e1352-150">This way, hello scale set can give these VMs private IP addresses from hello IP address range previously specified in hello network properties.</span></span> <span data-ttu-id="e1352-151">Каждая строка в списке dependsOn hello Hello формат `<type>/<name>`.</span><span class="sxs-lookup"><span data-stu-id="e1352-151">hello format of each string in hello dependsOn list is `<type>/<name>`.</span></span> <span data-ttu-id="e1352-152">Используйте hello же `type` и `name` ранее используется в определении ресурса hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e1352-152">Use hello same `type` and `name` used previously in hello virtual network resource definition.</span></span>

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a><span data-ttu-id="e1352-153">Определение свойств масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="e1352-153">Specify scale set properties</span></span>
<span data-ttu-id="e1352-154">Наборы масштабирования имеют множество свойств для настройки виртуальных машин hello в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="e1352-154">Scale sets have many properties for customizing hello VMs in hello scale set.</span></span> <span data-ttu-id="e1352-155">Полный список этих свойств см. в разделе hello [в наборе документации по REST API](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span><span class="sxs-lookup"><span data-stu-id="e1352-155">For a full list of these properties, see hello [scale set REST API documentation](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set).</span></span> <span data-ttu-id="e1352-156">В этом руководстве мы определим лишь несколько наиболее распространенных свойств.</span><span class="sxs-lookup"><span data-stu-id="e1352-156">For this tutorial, we will set only a few commonly used properties.</span></span>
### <a name="supply-vm-size-and-capacity"></a><span data-ttu-id="e1352-157">Определение размера и емкости виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e1352-157">Supply VM size and capacity</span></span>
<span data-ttu-id="e1352-158">tooknow потребности набора масштабирования Hello, выберите размер виртуальной Машины toocreate («имя sku») и сколько таких виртуальных машин toocreate («объем sku»).</span><span class="sxs-lookup"><span data-stu-id="e1352-158">hello scale set needs tooknow what size of VM toocreate ("sku name") and how many such VMs toocreate ("sku capacity").</span></span> <span data-ttu-id="e1352-159">toosee какие размеры виртуальных Машин доступны в разделе hello [размеры виртуальных Машин документации](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span><span class="sxs-lookup"><span data-stu-id="e1352-159">toosee which VM sizes are available, see hello [VM Sizes documentation](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).</span></span>

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a><span data-ttu-id="e1352-160">Выбор типа обновления</span><span class="sxs-lookup"><span data-stu-id="e1352-160">Choose type of updates</span></span>
<span data-ttu-id="e1352-161">набор масштабирования Hello также должен tooknow способ toohandle обновления в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="e1352-161">hello scale set also needs tooknow how toohandle updates on hello scale set.</span></span> <span data-ttu-id="e1352-162">Сейчас поддерживаются два варианта: `Manual` и `Automatic`.</span><span class="sxs-lookup"><span data-stu-id="e1352-162">Currently, there are two options, `Manual` and `Automatic`.</span></span> <span data-ttu-id="e1352-163">Дополнительные сведения о hello различия между двумя hello документации hello на [tooupgrade шкалу настроек](./virtual-machine-scale-sets-upgrade-scale-set.md).</span><span class="sxs-lookup"><span data-stu-id="e1352-163">For more information on hello differences between hello two, see hello documentation on [how tooupgrade a scale set](./virtual-machine-scale-sets-upgrade-scale-set.md).</span></span>

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a><span data-ttu-id="e1352-164">Выбор операционной системы для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e1352-164">Choose VM operating system</span></span>
<span data-ttu-id="e1352-165">Hello набора масштабирования tooknow потребностей какие tooput операционной системы на виртуальных машинах hello.</span><span class="sxs-lookup"><span data-stu-id="e1352-165">hello scale set needs tooknow what operating system tooput on hello VMs.</span></span> <span data-ttu-id="e1352-166">Здесь мы создать виртуальные машины hello с полностью обновленного образа 16.04 LTS Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e1352-166">Here, we create hello VMs with a fully patched Ubuntu 16.04-LTS image.</span></span>

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a><span data-ttu-id="e1352-167">Определение префикса имени компьютера (computerNamePrefix)</span><span class="sxs-lookup"><span data-stu-id="e1352-167">Specify computerNamePrefix</span></span>
<span data-ttu-id="e1352-168">набор масштабирования Hello развертывает несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e1352-168">hello scale set deploys multiple VMs.</span></span> <span data-ttu-id="e1352-169">Мы не будем указывать имя отдельно для каждой из них, а просто укажем префикс `computerNamePrefix`.</span><span class="sxs-lookup"><span data-stu-id="e1352-169">Instead of specifying each VM name, we specify `computerNamePrefix`.</span></span> <span data-ttu-id="e1352-170">Hello набор масштабирования добавляет префикс toohello индекс для каждой виртуальной Машины, имена виртуальных Машин имеют форму hello `<computerNamePrefix>_<auto-generated-index>`.</span><span class="sxs-lookup"><span data-stu-id="e1352-170">hello scale set appends an index toohello prefix for each VM, so VM names have hello form `<computerNamePrefix>_<auto-generated-index>`.</span></span>

<span data-ttu-id="e1352-171">В следующий фрагмент кода hello мы используем hello параметров из перед tooset hello администратора, имя пользователя и пароль для всех виртуальных машин в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="e1352-171">In hello following snippet, we use hello parameters from before tooset hello administrator username and password for all VMs in hello scale set.</span></span> <span data-ttu-id="e1352-172">Это делается с hello `parameters` функции шаблона.</span><span class="sxs-lookup"><span data-stu-id="e1352-172">We do this with hello `parameters` template function.</span></span> <span data-ttu-id="e1352-173">Эта функция принимает строку, указывающую, какой параметр toorefer tooand выводит hello значение для этого параметра.</span><span class="sxs-lookup"><span data-stu-id="e1352-173">This function takes in a string that specifies which parameter toorefer tooand outputs hello value for that parameter.</span></span>

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a><span data-ttu-id="e1352-174">Определение конфигурации сети для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e1352-174">Specify VM network configuration</span></span>
<span data-ttu-id="e1352-175">Наконец мы должны toospecify hello сетевая конфигурация для виртуальных машин hello в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="e1352-175">Finally, we need toospecify hello network configuration for hello VMs in hello scale set.</span></span> <span data-ttu-id="e1352-176">В этом случае нам требуется только идентификатор hello toospecify подсети hello, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="e1352-176">In this case, we only need toospecify hello ID of hello subnet created earlier.</span></span> <span data-ttu-id="e1352-177">Это значение определяет масштаб hello набора tooput hello сетевых интерфейсов в этой подсети.</span><span class="sxs-lookup"><span data-stu-id="e1352-177">This tells hello scale set tooput hello network interfaces in this subnet.</span></span>

<span data-ttu-id="e1352-178">Можно получить идентификатор hello hello виртуальной сети, содержащего hello подсети с помощью hello `resourceId` функции шаблона.</span><span class="sxs-lookup"><span data-stu-id="e1352-178">You can get hello ID of hello virtual network containing hello subnet by using hello `resourceId` template function.</span></span> <span data-ttu-id="e1352-179">Эта функция принимает hello тип и имя ресурса и возвращает hello полный идентификатор этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="e1352-179">This function takes in hello type and name of a resource and returns hello fully qualified identifier of that resource.</span></span> <span data-ttu-id="e1352-180">Этот идентификатор имеет форму hello.`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span><span class="sxs-lookup"><span data-stu-id="e1352-180">This ID has hello form: `/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`</span></span>

<span data-ttu-id="e1352-181">Однако идентификатор hello hello виртуальной сети недостаточно.</span><span class="sxs-lookup"><span data-stu-id="e1352-181">However, hello identifier of hello virtual network is not enough.</span></span> <span data-ttu-id="e1352-182">Необходимо указать, hello масштабный набор виртуальных машин должны находиться в определенной подсети hello.</span><span class="sxs-lookup"><span data-stu-id="e1352-182">You must specify hello specific subnet that hello scale set VMs should be in.</span></span> <span data-ttu-id="e1352-183">toodo этого объединения `/subnets/mySubnet` toohello идентификатор hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e1352-183">toodo this, concatenate `/subnets/mySubnet` toohello ID of hello virtual network.</span></span> <span data-ttu-id="e1352-184">результат Hello — идентификатор hello полное hello подсети.</span><span class="sxs-lookup"><span data-stu-id="e1352-184">hello result is hello fully qualified ID of hello subnet.</span></span> <span data-ttu-id="e1352-185">Сделать это объединение с hello `concat` функции, которая принимает набор строк и возвращает их объединения.</span><span class="sxs-lookup"><span data-stu-id="e1352-185">Do this concatenation with hello `concat` function, which takes in a series of strings and returns their concatenation.</span></span>

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a><span data-ttu-id="e1352-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e1352-186">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
