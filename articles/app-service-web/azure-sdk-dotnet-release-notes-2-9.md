---
title: "aaaAzure SDK .NET 2.9 заметки о выпуске"
description: "Заметки о выпуске пакета SDK для Azure для .NET 2.9"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="02c2a-103">Заметки о выпуске пакета Azure SDK для .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="02c2a-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="02c2a-104">В этой статье содержатся заметки о выпуске для версий 2.9 и 2.9.6 пакета Azure SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="02c2a-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="02c2a-105">Сведения о выпуске Azure SDK для .NET 2.9.6</span><span class="sxs-lookup"><span data-stu-id="02c2a-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="02c2a-106">Дата выпуска: 16.11.2016</span><span class="sxs-lookup"><span data-stu-id="02c2a-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="02c2a-107">В этом выпуске были введены нет критические изменения toohello Azure SDK 2.9.</span><span class="sxs-lookup"><span data-stu-id="02c2a-107">No breaking changes toohello Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="02c2a-108">Имеется также tooleverage нет необходимости процесса обновления этот пакет SDK с существующие проекты облачной службы.</span><span class="sxs-lookup"><span data-stu-id="02c2a-108">There is also no upgrade process needed tooleverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="02c2a-109">релиз-кандидат Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="02c2a-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="02c2a-110">В Visual Studio RC 2017 г. Этот выпуск hello Azure SDK для .NET встроенная hello Azure рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="02c2a-110">In Visual Studio 2017 RC, this release of hello Azure SDK for .NET is built in in hello Azure Workload.</span></span> <span data-ttu-id="02c2a-111">Все hello инструменты разработки Azure toodo будет входить в состав Visual Studio 2017 г. версия-кандидат Забегая вперед.</span><span class="sxs-lookup"><span data-stu-id="02c2a-111">All hello tools you need toodo Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="02c2a-112">Для Visual Studio 2015 и Visual Studio 2013 hello SDK по-прежнему доступны через WebPI.</span><span class="sxs-lookup"><span data-stu-id="02c2a-112">For Visual Studio 2015 and Visual Studio 2013, hello SDK will still be available through WebPI.</span></span> <span data-ttu-id="02c2a-113">Когда Visual Studio 2017 будет выпущен в качестве конечного продукта, версии пакета Azure SDK для .NET больше не будут доступны для Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="02c2a-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="02c2a-114">Следуйте этой связи toodownload версии-Кандидата Visual Studio 2017 г.: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="02c2a-114">Follow this link toodownload Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="02c2a-115">Диагностика Azure</span><span class="sxs-lookup"><span data-stu-id="02c2a-115">Azure Diagnostics</span></span>

- <span data-ttu-id="02c2a-116">Измененные hello поведение tooonly хранить частичную строку соединения с ключом hello заменяется маркер для строки подключения к хранилищу диагностики облачных служб.</span><span class="sxs-lookup"><span data-stu-id="02c2a-116">Changed hello behavior tooonly store a partial connection string with hello key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="02c2a-117">ключ фактического хранения Hello теперь хранится в папке профиля пользователя hello, можно контролировать доступ к нему.</span><span class="sxs-lookup"><span data-stu-id="02c2a-117">hello actual storage key is now stored in hello user profile folder so its access can be controlled.</span></span> <span data-ttu-id="02c2a-118">Visual Studio прочитает hello ключ хранилища из папке профиля пользователя для локальной отладки и процесс публикации.</span><span class="sxs-lookup"><span data-stu-id="02c2a-118">Visual Studio will read hello storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="02c2a-119">В ответ toohello изменений, описанных выше Visual Studio Online team улучшенные hello шаблона задачи развертывания облачных служб Azure, пользователи могут указать hello ключ хранилища для настройки расширения системы диагностики при публикации tooAzure в непрерывной интеграции и развертывания.</span><span class="sxs-lookup"><span data-stu-id="02c2a-119">In response toohello change described above, Visual Studio Online team enhanced hello Azure Cloud Services deployment task template so users could specify hello storage key for setting diagnostics extension when publishing tooAzure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="02c2a-120">Мы уже сделали возможных toostore строку безопасного соединения и разметки для Azure Diagnostics (WAD), toohelp через environements устранить проблемы с конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="02c2a-120">We’ve made it possible toostore secure connection string and tokenization for Azure Diagnostics (WAD), toohelp you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="02c2a-121">Виртуальные машины Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="02c2a-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="02c2a-122">Visual Studio теперь поддерживает развертывание облачных служб tooOS семейство 5 (Windows Server 2016) виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="02c2a-122">Visual Studio now supports deploying Cloud Services tooOS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="02c2a-123">Для существующих облачных служб можно изменить ваш tootarget параметры hello новое семейство ОС.</span><span class="sxs-lookup"><span data-stu-id="02c2a-123">For existing cloud services, you can change your settings tootarget hello new OS Family.</span></span> <span data-ttu-id="02c2a-124">Если при создании новых облачных служб, выберите службу hello toocreate, с помощью .net 4.6 или более поздней версии, то по умолчанию hello службы toouse 5 семейства ОС.</span><span class="sxs-lookup"><span data-stu-id="02c2a-124">When creating new cloud services, if you choose toocreate hello service using .net 4.6 or higher, it will default hello service toouse OS Family 5.</span></span>  <span data-ttu-id="02c2a-125">Дополнительные сведения можно просмотреть hello [семейства гостевых ОС поддерживает таблицу](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span><span class="sxs-lookup"><span data-stu-id="02c2a-125">For more information, you can review hello [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="02c2a-126">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="02c2a-126">Known issues</span></span>

- <span data-ttu-id="02c2a-127">Ограничение, и блокирует развертывание проектов, с помощью tooany платформ (таких как .NET 4.6) не поддерживается .NET семейства ОС появился Azure .NET SDK 2.9.6 < 5.</span><span class="sxs-lookup"><span data-stu-id="02c2a-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) tooany OS Family < 5.</span></span> <span data-ttu-id="02c2a-128">Обходной путь описан [здесь](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="02c2a-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="02c2a-129">Кэш роли Azure</span><span class="sxs-lookup"><span data-stu-id="02c2a-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="02c2a-130">Поддержка кэша роли Azure закончилась 30 ноября 2016 года.</span><span class="sxs-lookup"><span data-stu-id="02c2a-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="02c2a-131">Дополнительные сведения см. [здесь](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="02c2a-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="02c2a-132">Шаблоны Azure Resource Manager для Azure Stack</span><span class="sxs-lookup"><span data-stu-id="02c2a-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="02c2a-133">Мы представляем Azure Stack как целевой объект развертывания для шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02c2a-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="02c2a-134">Сводка о пакете Azure SDK для .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="02c2a-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="02c2a-135">Обзор</span><span class="sxs-lookup"><span data-stu-id="02c2a-135">Overview</span></span>
<span data-ttu-id="02c2a-136">Этот документ содержит заметки о выпуске hello для hello Azure SDK для .NET 2.9 выпуска.</span><span class="sxs-lookup"><span data-stu-id="02c2a-136">This document contains hello release notes for hello Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="02c2a-137">Подробные сведения об обновлениях в этом выпуске см. в разделе hello [post объявления Azure SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span><span class="sxs-lookup"><span data-stu-id="02c2a-137">For detailed information about updates in this release, see hello [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="02c2a-138">Azure SDK 2.9 для Visual Studio 2015 с обновлением 2 и Visual Studio "15" (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="02c2a-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="02c2a-139">Это обновление содержит следующие исправления hello.</span><span class="sxs-lookup"><span data-stu-id="02c2a-139">This update includes hello following bug fixes:</span></span>

* <span data-ttu-id="02c2a-140">Выдача связанные tooREST создание клиента API в в какой строке hello «Неизвестный тип» будет отображаться как hello имя папки генерация кода hello и/или hello имя пространства имен hello в hello созданный код.</span><span class="sxs-lookup"><span data-stu-id="02c2a-140">Issue related tooREST API Client Generation in in which hello string "Unknown Type” would appear as hello name of hello code-gen folder and/or hello name of hello namespace dropped into hello generated code.</span></span>
* <span data-ttu-id="02c2a-141">Выполните веб-задания связанных tooScheduled строя сведения о проверке подлинности в какой hello toobe передан процесса подготовки toohello планировщика.</span><span class="sxs-lookup"><span data-stu-id="02c2a-141">Issue related tooScheduled WebJobs in which hello authentication information was failing toobe passed toohello Scheduler provisioning process.</span></span>

<span data-ttu-id="02c2a-142">Это обновление содержит следующие новые функции hello.</span><span class="sxs-lookup"><span data-stu-id="02c2a-142">This update includes hello following new feature:</span></span>

* <span data-ttu-id="02c2a-143">Поддержка дополнительного приложения служб на вкладке «Службы» Привет hello диалоговое окно подготовки службы приложений.</span><span class="sxs-lookup"><span data-stu-id="02c2a-143">Support for secondary App Services in hello "Services" tab of hello App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="02c2a-144">Средства озера данных Azure для Visual Studio 2015 с обновлением 2</span><span class="sxs-lookup"><span data-stu-id="02c2a-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="02c2a-145">Это обновление включает hello следующие:</span><span class="sxs-lookup"><span data-stu-id="02c2a-145">This updates includes hello following:</span></span>

* <span data-ttu-id="02c2a-146">**Инструменты Azure Озера данных** для Visual Studio теперь объединены в hello Azure SDK для .NET версии.</span><span class="sxs-lookup"><span data-stu-id="02c2a-146">**Azure Data Lake Tools** for Visual Studio is now merged into hello Azure SDK for .NET release.</span></span> <span data-ttu-id="02c2a-147">Программа Hello автоматически устанавливается при установке пакета SDK Azure.</span><span class="sxs-lookup"><span data-stu-id="02c2a-147">hello tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="02c2a-148">Средство Hello часто обновляется, переход [здесь](http://aka.ms/datalaketool) tooget hello обновлений.</span><span class="sxs-lookup"><span data-stu-id="02c2a-148">hello tool is updated frequently, go [here](http://aka.ms/datalaketool) tooget hello updates.</span></span>
* <span data-ttu-id="02c2a-149">**Обозреватель серверов** теперь позволяет tooview все и создать некоторые сущности метаданных U-SQL.</span><span class="sxs-lookup"><span data-stu-id="02c2a-149">**Server Explorer** now enables you tooview all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="02c2a-150">Дополнительную информацию см. в [этом](https://azure.microsoft.com/documentation/services/data-lake-analytics/) блоге.</span><span class="sxs-lookup"><span data-stu-id="02c2a-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="02c2a-151">Средства HDInsight</span><span class="sxs-lookup"><span data-stu-id="02c2a-151">HDInsight Tools</span></span>
<span data-ttu-id="02c2a-152">**Средства HDInsight** для Visual Studio теперь поддерживают HDInsight версии 3.3, включая показ графики Tez и другие языковые исправления.</span><span class="sxs-lookup"><span data-stu-id="02c2a-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="02c2a-153">Диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="02c2a-153">Azure Resource Manager</span></span>
<span data-ttu-id="02c2a-154">В этом выпуске добавлена поддержка [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) для шаблонов Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02c2a-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="02c2a-155">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="02c2a-155">See also</span></span>
[<span data-ttu-id="02c2a-156">Объявление о пакете SDK Azure 2.9</span><span class="sxs-lookup"><span data-stu-id="02c2a-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

