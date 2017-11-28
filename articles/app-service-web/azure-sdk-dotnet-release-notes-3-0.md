---
title: "пакет SDK для .NET 3.0 заметки о выпуске aaaAzure | Документы Microsoft"
description: "Заметки о выпуске пакета Azure SDK для .NET 3.0"
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
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: 8970b4c9b64de40dc29a33d69006a00ae5e38a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a><span data-ttu-id="9c671-103">Заметки о выпуске пакета Azure SDK для .NET 3.0</span><span class="sxs-lookup"><span data-stu-id="9c671-103">Azure SDK for .NET 3.0 release notes</span></span>

<span data-ttu-id="9c671-104">Этот раздел содержит заметки о выпуске для версии 3.0 hello Azure SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="9c671-104">This topic includes release notes for version 3.0 of hello Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-30-release-summary"></a><span data-ttu-id="9c671-105">Сводные данные о выпуске пакета Azure SDK для .NET 3.0</span><span class="sxs-lookup"><span data-stu-id="9c671-105">Azure SDK for .NET 3.0 release summary</span></span>

<span data-ttu-id="9c671-106">Дата выпуска: 07.03.2017</span><span class="sxs-lookup"><span data-stu-id="9c671-106">Release date: 03/07/2017</span></span>
 
<span data-ttu-id="9c671-107">В этом выпуске были введены нет критические изменения toohello Azure SDK 3.0.</span><span class="sxs-lookup"><span data-stu-id="9c671-107">No breaking changes toohello Azure SDK 3.0 have been introduced in this release.</span></span> <span data-ttu-id="9c671-108">Имеется также tooleverage нет необходимости процесса обновления этот пакет SDK с существующие проекты облачной службы.</span><span class="sxs-lookup"><span data-stu-id="9c671-108">There is also no upgrade process needed tooleverage this SDK with existing Cloud Service projects.</span></span> <span data-ttu-id="9c671-109">Использование tooallow hello Azure SDK 3.0 без необходимости процесса обновления Azure SDK 3.0 устанавливает toohello же каталоги, что пакет Azure SDK 2.9.</span><span class="sxs-lookup"><span data-stu-id="9c671-109">tooallow use of hello Azure SDK 3.0 without requiring an upgrade process, Azure SDK 3.0 installs toohello same directories as Azure SDK 2.9.</span></span> <span data-ttu-id="9c671-110">Большинство компонентов hello не изменился с 2.9 hello основной номер версии, но вместо обновляться hello номер сборки.</span><span class="sxs-lookup"><span data-stu-id="9c671-110">Most hello components did not change hello major version from 2.9 but instead just updated hello build number.</span></span>

## <a name="visual-studio-2017-rtw"></a><span data-ttu-id="9c671-111">Visual Studio 2017 RTW</span><span class="sxs-lookup"><span data-stu-id="9c671-111">Visual Studio 2017 RTW</span></span>

- <span data-ttu-id="9c671-112">Этот выпуск hello Azure SDK для .NET в Visual Studio 2017 г., встроенной в toohello рабочей нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="9c671-112">In Visual Studio 2017, this release of hello Azure SDK for .NET is built in toohello Azure Workload.</span></span> <span data-ttu-id="9c671-113">Все hello инструменты разработки Azure toodo будет частью Visual Studio Забегая вперед 2017 г.</span><span class="sxs-lookup"><span data-stu-id="9c671-113">All hello tools you need toodo Azure development will be part of Visual Studio 2017 going forward.</span></span> <span data-ttu-id="9c671-114">Для Visual Studio 2015 hello SDK по-прежнему доступны через WebPI.</span><span class="sxs-lookup"><span data-stu-id="9c671-114">For Visual Studio 2015 hello SDK will still be available through WebPI.</span></span> <span data-ttu-id="9c671-115">Мы вывели из использования выпуски пакета Azure SDK для .NET для Visual Studio 2013, так как теперь вышла версия Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9c671-115">We have discontinued Azure SDK for .NET releases for Visual Studio 2013 now that Visual Studio 2017 has been released.</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="9c671-116">Диагностика Azure</span><span class="sxs-lookup"><span data-stu-id="9c671-116">Azure Diagnostics</span></span>

- <span data-ttu-id="9c671-117">Измененные hello поведение tooonly хранить частичную строку соединения с ключом hello заменяется маркер для строки подключения к хранилищу диагностики облачных служб.</span><span class="sxs-lookup"><span data-stu-id="9c671-117">Changed hello behavior tooonly store a partial connection string with hello key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="9c671-118">ключ фактического хранения Hello теперь хранится в папке профиля пользователя hello, можно контролировать доступ к нему.</span><span class="sxs-lookup"><span data-stu-id="9c671-118">hello actual storage key is now stored in hello user profile folder so its access can be controlled.</span></span> <span data-ttu-id="9c671-119">Visual Studio прочитает hello ключ хранилища из папке профиля пользователя для локальной отладки и процесс публикации.</span><span class="sxs-lookup"><span data-stu-id="9c671-119">Visual Studio will read hello storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="9c671-120">В ответ toohello изменений, описанных выше Visual Studio Online team улучшенные hello шаблона задачи развертывания облачных служб Azure, пользователи могут указать hello ключ хранилища для настройки расширения системы диагностики при публикации tooAzure в непрерывной интеграции и развертывания.</span><span class="sxs-lookup"><span data-stu-id="9c671-120">In response toohello change described above, Visual Studio Online team enhanced hello Azure Cloud Services deployment task template so users could specify hello storage key for setting diagnostics extension when publishing tooAzure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="9c671-121">Мы уже сделали возможных toostore строку безопасного соединения и разметки для Azure Diagnostics (WAD), toohelp через environements устранить проблемы с конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="9c671-121">We’ve made it possible toostore secure connection string and tokenization for Azure Diagnostics (WAD), toohelp you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="9c671-122">Виртуальные машины Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="9c671-122">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="9c671-123">Visual Studio теперь поддерживает развертывание облачных служб tooOS семейство 5 (Windows Server 2016) виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="9c671-123">Visual Studio now supports deploying Cloud Services tooOS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="9c671-124">Для существующих облачных служб можно изменить ваш tootarget параметры hello новое семейство ОС.</span><span class="sxs-lookup"><span data-stu-id="9c671-124">For existing cloud services, you can change your settings tootarget hello new OS Family.</span></span> <span data-ttu-id="9c671-125">Если при создании новых облачных служб, выберите службу hello toocreate, с помощью .net 4.6 или более поздней версии, то по умолчанию hello службы toouse 5 семейства ОС.</span><span class="sxs-lookup"><span data-stu-id="9c671-125">When creating new cloud services, if you choose toocreate hello service using .net 4.6 or higher, it will default hello service toouse OS Family 5.</span></span>  <span data-ttu-id="9c671-126">Дополнительные сведения можно просмотреть hello [семейства гостевых ОС поддерживает таблицу](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="9c671-126">For more information, you can review hello [Guest OS Family support table](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span>

### <a name="known-issues"></a><span data-ttu-id="9c671-127">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="9c671-127">Known issues</span></span>

- <span data-ttu-id="9c671-128">В пакете SDK Azure 3.0 для .NET возникала проблема при удалении Visual Studio 2017 в параллельной конфигурации с Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="9c671-128">Azure .NET SDK 3.0 introduced an issue when removing Visual Studio 2017 in a side by side configuration with Visual Studio 2015.</span></span>  <span data-ttu-id="9c671-129">При наличии hello пакет Azure SDK для Visual Studio 2015 hello эмулятор хранилища Microsoft Azure и эмулятор вычислений Microsoft Azure будут удалены при удалении Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="9c671-129">If you have hello Azure SDK installed for Visual Studio 2015, hello Microsoft Azure Storage Emulator and Microsoft Azure Compute Emulator will be removed if you uninstall Visual Studio 2017.</span></span>  <span data-ttu-id="9c671-130">Это приведет к ошибке при создании и отладке новых проектов облачных служб в Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="9c671-130">This will produce an error when creating and debugging new Cloud services projects in Visual Studio 2015.</span></span> <span data-ttu-id="9c671-131">В заказ toofix эту проблему, переустановите hello Azure SDK из hello установщика веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="9c671-131">In order toofix this issue,  reinstall hello Azure SDK from hello Web Platform Installer.</span></span>  <span data-ttu-id="9c671-132">Hello проблема будет устранена в следующей версии Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="9c671-132">hello issue will be resolved in a future Visual Studio 2017 update.</span></span>  <span data-ttu-id="9c671-133">.</span><span class="sxs-lookup"><span data-stu-id="9c671-133">.</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="9c671-134">Кэш роли Azure</span><span class="sxs-lookup"><span data-stu-id="9c671-134">Azure In-Role Cache</span></span> 

- <span data-ttu-id="9c671-135">Поддержка кэша роли Azure завершилась 30 ноября 2016 года.</span><span class="sxs-lookup"><span data-stu-id="9c671-135">Support for Azure In-Role Cache ended on November 30, 2016.</span></span> <span data-ttu-id="9c671-136">Дополнительные сведения см. [здесь](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="9c671-136">For more details, click [here](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>




