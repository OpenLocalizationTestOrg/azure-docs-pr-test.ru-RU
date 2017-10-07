---
title: "заметки о выпуске aaaAzure данных каталога | Документы Microsoft"
description: "Заметки о выпуске каталога данных Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 661826f66020ba72a885c6b14522b53c8b469d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-release-notes"></a><span data-ttu-id="b5dd5-103">Заметки о выпуске каталога данных Azure</span><span class="sxs-lookup"><span data-stu-id="b5dd5-103">Azure Data Catalog release notes</span></span>
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a><span data-ttu-id="b5dd5-104">Заметки о выпуске 20 ноября 2015 г. hello каталога данных Azure</span><span class="sxs-lookup"><span data-stu-id="b5dd5-104">Notes for hello November 20, 2015 release of Azure Data Catalog</span></span>
### <a name="opening-data-sources-in-power-bi-desktop"></a><span data-ttu-id="b5dd5-105">Открытие источников данных в Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="b5dd5-105">Opening Data Sources in Power BI Desktop</span></span>
<span data-ttu-id="b5dd5-106">При использовании параметра «Открыть в Power BI Desktop» hello из hello **каталога данных Azure** портала, пользователей может возникнуть одна из двух проблем в hello приложения Power BI Desktop:</span><span class="sxs-lookup"><span data-stu-id="b5dd5-106">When using hello "Open in Power BI Desktop" option from hello **Azure Data Catalog** portal, users may encounter one of two problems in hello Power BI Desktop application:</span></span>

* <span data-ttu-id="b5dd5-107">Откроется диалоговое окно с заголовком hello «Не удается tooOpen документа»</span><span class="sxs-lookup"><span data-stu-id="b5dd5-107">A dialog box with hello title "Unable tooOpen Document" is displayed</span></span>
* <span data-ttu-id="b5dd5-108">Открывает Hello приложения Power BI Desktop, но файл hello появится пустой toobe</span><span class="sxs-lookup"><span data-stu-id="b5dd5-108">hello Power BI Desktop application opens, but hello file appears toobe empty</span></span>

<span data-ttu-id="b5dd5-109">В каждом случае hello проблему можно устранить, загрузив и установив последнюю версию Power BI Desktop из hello [PowerBI.com](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="b5dd5-109">For each situation, hello problem can be resolved by downloading and installing hello latest version of Power BI Desktop from [PowerBI.com](https://powerbi.com).</span></span>

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="b5dd5-110">Заметки о выпуске 13 ноября 2015 г. hello каталога данных Azure</span><span class="sxs-lookup"><span data-stu-id="b5dd5-110">Notes for hello November 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-tooteradata"></a><span data-ttu-id="b5dd5-111">Регистрация и подключении tooTeradata</span><span class="sxs-lookup"><span data-stu-id="b5dd5-111">Registering and connecting tooTeradata</span></span>
<span data-ttu-id="b5dd5-112">При подключении tooTeradata источники данных пользователям необходимо установить правильный драйвер Teradata ODBC hello, соответствующих hello разрядности (32-разрядной или 64-разрядной) используемого программного hello.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-112">When connecting tooTeradata data sources users must have installed hello correct Teradata ODBC driver that match hello bitness (32-bit or 64-bit) of hello software being used.</span></span>

<span data-ttu-id="b5dd5-113">На момент написания этой ADC Дата выпуска, hello последней [Teradata ODBC-драйвер для windows (версия 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) совместим с Office 2013, но не с Office 2016.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-113">As of this ADC release date, hello most recent [Teradata ODBC driver for windows ( version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatible with Office 2013, but not with Office 2016.</span></span>

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="b5dd5-114">Заметки о выпуске 13 июля 2015 г. hello каталога данных Azure</span><span class="sxs-lookup"><span data-stu-id="b5dd5-114">Notes for hello July 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-toooracle-database"></a><span data-ttu-id="b5dd5-115">Регистрация и подключении tooOracle базы данных</span><span class="sxs-lookup"><span data-stu-id="b5dd5-115">Registering and connecting tooOracle Database</span></span>
<span data-ttu-id="b5dd5-116">При подключении пользователей источников данных tooOracle базы данных необходимо установить hello правильный Oracle драйверы, которые соответствуют hello разрядности (32-разрядной или 64-разрядной) hello программном обеспечении, используемом.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-116">When connecting tooOracle Database data sources users must have installed hello correct Oracle drivers that match hello bitness (32-bit or 64-bit) of hello software being used.</span></span>

* <span data-ttu-id="b5dd5-117">При регистрации источников данных Oracle на компьютере под управлением 32-разрядной версии Windows, будет использоваться hello 32-разрядные драйверы Oracle</span><span class="sxs-lookup"><span data-stu-id="b5dd5-117">When registering Oracle data sources on a computer running 32-bit Windows, hello 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="b5dd5-118">При регистрации источников данных Oracle на компьютере под управлением 64-разрядной версии Windows, будет использоваться hello 64-разрядные драйверы Oracle</span><span class="sxs-lookup"><span data-stu-id="b5dd5-118">When registering Oracle data sources on a computer running 64-bit Windows, hello 64-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="b5dd5-119">При подключении tooOracle источники данных, с помощью Excel на компьютере под управлением hello 32-разрядной версии Microsoft Office, включая на 64-разрядной Windows hello 32-разрядные драйверы Oracle будет использоваться</span><span class="sxs-lookup"><span data-stu-id="b5dd5-119">When connecting tooOracle data sources using Excel on a computer running hello 32-bit version of Microsoft Office, including on 64-bit Windows, hello 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="b5dd5-120">При подключении tooOracle источники данных, с помощью Excel на компьютере под управлением hello 64-разрядная версия Microsoft Office, будут использоваться hello 64-разрядные драйверы Oracle</span><span class="sxs-lookup"><span data-stu-id="b5dd5-120">When connecting tooOracle data sources using Excel on a computer running hello 64-bit version of Microsoft Office, hello 64-bit Oracle drivers will be used</span></span>

### <a name="registering-and-connecting-toosql-server-reporting-services"></a><span data-ttu-id="b5dd5-121">Регистрация и подключении tooSQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="b5dd5-121">Registering and connecting tooSQL Server Reporting Services</span></span>
<span data-ttu-id="b5dd5-122">Для источников данных службы SQL Server Reporting Services (SSRS) поддерживается только в настоящее время составляет tooNative режиме серверы.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-122">Support for SQL Server Reporting Services (SSRS) data sources is currently limited tooNative Mode servers only.</span></span> <span data-ttu-id="b5dd5-123">Поддержка служб SSRS в режиме интеграции с SharePoint будет добавлена в более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-123">Support for SSRS in SharePoint mode will be added in a later release.</span></span>

### <a name="opening-data-assets-in-excel"></a><span data-ttu-id="b5dd5-124">Открытие ресурсов данных в Excel</span><span class="sxs-lookup"><span data-stu-id="b5dd5-124">Opening data assets in Excel</span></span>
<span data-ttu-id="b5dd5-125">При открытии ресурсов данных в Microsoft Excel из hello **каталога данных Azure** портала, пользователям может предлагаться с **уведомление безопасности Microsoft Excel** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-125">When opening data assets in Microsoft Excel from hello **Azure Data Catalog** portal, users may be prompted with a **Microsoft Excel Security Notice** dialog box.</span></span> <span data-ttu-id="b5dd5-126">Это стандартный, ожидаемое поведение и пользователи могут выбирать **включить** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-126">This is standard, expected behavior, and users can select **Enable** toocontinue.</span></span>

<span data-ttu-id="b5dd5-127">Подробнее об этом см. в статье [Включение или отключение предупреждений системы безопасности о ссылках и файлах с подозрительных веб-сайтов](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span><span class="sxs-lookup"><span data-stu-id="b5dd5-127">For more information, see [Enable or disable security alerts about links and files from suspicious websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span></span>

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a><span data-ttu-id="b5dd5-128">Конфигурация прокси-сервера и политики, а также регистрация источника данных</span><span class="sxs-lookup"><span data-stu-id="b5dd5-128">Proxy and policy configuration and data source registration</span></span>
<span data-ttu-id="b5dd5-129">Пользователи могут столкнуться с ситуацией, где они могут войти на портал toohello каталога данных Azure, но при попытке toolog на точках сообщение об ошибке, которая запрещает вход в систему регистрации инструмента toohello данных источника.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-129">Users may encounter a situation where they can log on toohello Azure Data Catalog portal, but when they attempt toolog on toohello data source registration tool they encounter an error message that prevents them from logging on.</span></span>

<span data-ttu-id="b5dd5-130">Существуют две возможные причины такого проблемного поведения.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-130">There are two potential causes for this problem behavior:</span></span>

<span data-ttu-id="b5dd5-131">**Причина 1: Конфигурации служб федерации Active Directory** средство регистрации источника данных hello использует проверку подлинности форм toovalidate входа пользователей в систему с данными Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-131">**Cause 1: Active Directory Federation Services configuration** hello data source registration tool uses Forms Authentication toovalidate user logons against Active Directory.</span></span> <span data-ttu-id="b5dd5-132">Для успешного входа в систему необходимо включить проверку подлинности форм в hello глобальной политики проверки подлинности администратором Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-132">For successful logon, Forms Authentication must be enabled in hello Global Authentication Policy by an Active Directory administrator.</span></span>

<span data-ttu-id="b5dd5-133">В некоторых ситуациях это ошибка может происходить только в том случае, если пользователь hello находится в сети компании hello, или только при подключении пользователя hello с hello вне корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-133">In some situations, this error behavior may occur only when hello user is on hello company network, or only when hello user is connecting from outside hello company network.</span></span> <span data-ttu-id="b5dd5-134">Hello глобальной политики проверки подлинности позволяет toobe методы проверки подлинности включен отдельно для интрасети и экстрасети.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-134">hello Global Authentication Policy allows authentication methods toobe enabled separately for intranet and extranet connections.</span></span> <span data-ttu-id="b5dd5-135">Ошибки входа может возникнуть, если для сети hello, из какой hello подключении не включена проверка подлинности форм.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-135">Logon errors may occur if Forms Authentication is not enabled for hello network from which hello user is connecting.</span></span>

<span data-ttu-id="b5dd5-136">Подробнее: [Настройка политик проверки подлинности](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5dd5-136">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>

<span data-ttu-id="b5dd5-137">**Причина 2: Конфигурация прокси-сервера сети** Если hello корпоративной сети используются прокси-сервера, средство регистрации hello может оказаться tooAzure может tooconnect Active Directory через прокси-сервер hello.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-137">**Cause 2: Network proxy configuration** If hello corporate network uses a proxy server, hello registration tool may not be able tooconnect tooAzure Active Directory through hello proxy.</span></span> <span data-ttu-id="b5dd5-138">Пользователи гарантирует этого инструмента регистрации hello, изменив файл конфигурации средства hello, добавление файла toohello этого раздела:</span><span class="sxs-lookup"><span data-stu-id="b5dd5-138">Users can ensure that hello registration tool by editing hello tool’s configuration file, adding this section toohello file:</span></span>

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


<span data-ttu-id="b5dd5-139">файл RegistrationTool.exe.config toolocate hello, запустите средство регистрации hello, а затем откройте диспетчер задач Windows программа hello.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-139">toolocate hello RegistrationTool.exe.config file, launch hello registration tool, and then open hello Windows Task Manager utility.</span></span> <span data-ttu-id="b5dd5-140">На вкладке сведения hello в диспетчере задач щелкните правой кнопкой мыши на RegistrationTool.exe и выберите Открыть расположение файла hello во всплывающем меню.</span><span class="sxs-lookup"><span data-stu-id="b5dd5-140">On hello Details tab in Task manager, right-click on RegistrationTool.exe and choose Open file location from hello pop-up menu.</span></span>
