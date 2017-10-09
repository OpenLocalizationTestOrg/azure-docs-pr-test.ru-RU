---
title: "Параметры aaaCustom для среды службы приложений"
description: "Настраиваемые параметры конфигурации для сред службы приложений"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="cbcd8-103">Настраиваемые параметры конфигурации для сред службы приложений</span><span class="sxs-lookup"><span data-stu-id="cbcd8-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="cbcd8-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="cbcd8-104">Overview</span></span>
<span data-ttu-id="cbcd8-105">Поскольку среды службы приложений теперь изолированной tooa одного клиента, есть определенные параметры конфигурации, которые могут быть применены только tooApp среды службы.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-105">Because App Service Environments are isolated tooa single customer, there are certain configuration settings that can be applied exclusively tooApp Service Environments.</span></span> <span data-ttu-id="cbcd8-106">В данной статье описывается hello различные отдельные настройки, доступные для среды службы приложения.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-106">This article documents hello various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="cbcd8-107">Если у вас среды службы приложений, см. раздел [как tooCreate среды службы приложений](app-service-web-how-to-create-an-app-service-environment.md).</span><span class="sxs-lookup"><span data-stu-id="cbcd8-107">If you do not have an App Service Environment, see [How tooCreate an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="cbcd8-108">Можно сохранить настройки среды службы приложений с помощью нового массива hello **clusterSettings** атрибута.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-108">You can store App Service Environment customizations by using an array in hello new **clusterSettings** attribute.</span></span> <span data-ttu-id="cbcd8-109">Этот атрибут находится в словарь «Свойства» hello hello *hostingEnvironments* сущности диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-109">This attribute is found in hello "Properties" dictionary of hello *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="cbcd8-110">Hello следующий сокращенный диспетчера ресурсов шаблона фрагмент показывает hello **clusterSettings** атрибута:</span><span class="sxs-lookup"><span data-stu-id="cbcd8-110">hello following abbreviated Resource Manager template snippet shows hello **clusterSettings** attribute:</span></span>

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

<span data-ttu-id="cbcd8-111">Hello **clusterSettings** атрибута может быть включено в hello tooupdate шаблона диспетчера ресурсов среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-111">hello **clusterSettings** attribute can be included in a Resource Manager template tooupdate hello App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a><span data-ttu-id="cbcd8-112">Использование обозревателя ресурсов Azure tooupdate среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="cbcd8-112">Use Azure Resource Explorer tooupdate an App Service Environment</span></span>
<span data-ttu-id="cbcd8-113">Кроме того, можно обновить hello среды службы приложений с помощью [обозревателя ресурсов Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cbcd8-113">Alternatively, you can update hello App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="cbcd8-114">В обозревателе ресурсов, перейдите в узел toohello для hello среды службы приложений (**подписки** > **resourceGroups** > **поставщики**  >  **Microsoft.Web** > **hostingEnvironments**).</span><span class="sxs-lookup"><span data-stu-id="cbcd8-114">In Resource Explorer, go toohello node for hello App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="cbcd8-115">Нажмите кнопку hello определенной среды службы приложений, которые должны tooupdate.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-115">Then click hello specific App Service Environment that you want tooupdate.</span></span>
2. <span data-ttu-id="cbcd8-116">Hello правой панели щелкните **чтения и записи** в tooallow верхней панели инструментов hello интерактивного редактирования в обозревателе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-116">In hello right pane, click **Read/Write** in hello upper toolbar tooallow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="cbcd8-117">Щелкните голубой hello **изменить** кнопку toomake hello шаблона диспетчера ресурсов для редактирования.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-117">Click hello blue **Edit** button toomake hello Resource Manager template editable.</span></span>
4. <span data-ttu-id="cbcd8-118">Прокрутите toohello нижней правой области hello.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-118">Scroll toohello bottom of hello right pane.</span></span> <span data-ttu-id="cbcd8-119">Hello **clusterSettings** атрибут находится в самом низу hello, где можно ввести или обновить его значение.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-119">hello **clusterSettings** attribute is at hello very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="cbcd8-120">Тип (или копировать и вставить) hello массив значений параметров конфигурации в hello **clusterSettings** атрибута.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-120">Type (or copy and paste) hello array of configuration values you want in hello **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="cbcd8-121">Щелкните зеленый hello **ПОМЕСТИТЬ** кнопку, который находится вверху hello toohello hello правой панели toocommit hello изменение среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-121">Click hello green **PUT** button that's located at hello top of hello right pane toocommit hello change toohello App Service Environment.</span></span>

<span data-ttu-id="cbcd8-122">Однако при отправке изменений hello, занимает приблизительно 30 минут, умноженное на количество hello интерфейсы в hello среды службы приложений для hello изменение tootake эффекта.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-122">However you submit hello change, it takes roughly 30 minutes multiplied by hello number of front ends in hello App Service Environment for hello change tootake effect.</span></span>
<span data-ttu-id="cbcd8-123">Например если среды службы приложений имеет четыре интерфейсных, он займет приблизительно два часа для toofinish обновления конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for hello configuration update toofinish.</span></span> <span data-ttu-id="cbcd8-124">При изменении конфигурации hello разворачивается, никакие другие операции масштабирования или операций изменения конфигурации могут иметь место в hello среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-124">While hello configuration change is being rolled out, no other scaling operations or configuration change operations can take place in hello App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="cbcd8-125">Отключение TLS 1.0</span><span class="sxs-lookup"><span data-stu-id="cbcd8-125">Disable TLS 1.0</span></span>
<span data-ttu-id="cbcd8-126">Повторяющиеся вопрос от клиентов, особенно пользователи сталкиваются со соответствие стандартам PCI событий аудита, является то, каким образом tooexplicitly отключить TLS 1.0 для своих приложений.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how tooexplicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="cbcd8-127">Протокол TLS 1.0 можно отключить с помощью следующих hello **clusterSettings** входа:</span><span class="sxs-lookup"><span data-stu-id="cbcd8-127">TLS 1.0 can be disabled through hello following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="cbcd8-128">Порядок изменения комплекта шифров TLS </span><span class="sxs-lookup"><span data-stu-id="cbcd8-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="cbcd8-129">Другой вопрос от клиентов — Если hello список шифров согласовывается путем их сервер могут быть изменены, и это можно сделать, изменив hello **clusterSettings** как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-129">Another question from customers is if they can modify hello list of ciphers negotiated by their server and this can be achieved by modifying hello **clusterSettings** as shown below.</span></span> <span data-ttu-id="cbcd8-130">Список доступных комплектов шифров Hello можно получить из [в этой статье MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="cbcd8-130">hello list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="cbcd8-131">Если для hello комплекты шифров SChannel не понимают заданы неверные значения, все сервера tooyour TLS связи могут перестать работать.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-131">If incorrect values are set for hello cipher suite that SChannel cannot understand, all TLS communication tooyour server might stop functioning.</span></span> <span data-ttu-id="cbcd8-132">В этом случае вам потребуется tooremove hello *FrontEndSSLCipherSuiteOrder* запись из **clusterSettings** и отправьте hello обновления диспетчера ресурсов шаблона toorevert toohello назад по умолчанию шифров набор параметров.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-132">In such a case, you will need tooremove hello *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit hello updated Resource Manager template toorevert back toohello default cipher suite settings.</span></span>  <span data-ttu-id="cbcd8-133">Используйте эту возможность с осторожностью.</span><span class="sxs-lookup"><span data-stu-id="cbcd8-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="cbcd8-134">Начало работы</span><span class="sxs-lookup"><span data-stu-id="cbcd8-134">Get started</span></span>
<span data-ttu-id="cbcd8-135">Hello сайта шаблона диспетчера ресурсов Azure краткое руководство предоставляет шаблон с hello базовое определение для [создание среды службы приложений](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span><span class="sxs-lookup"><span data-stu-id="cbcd8-135">hello Azure Quickstart Resource Manager template site includes a template with hello base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
