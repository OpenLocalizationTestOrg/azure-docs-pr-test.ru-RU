---
title: "Заметки о выпуске каталога данных Azure | Документация Майкрософт"
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
ms.openlocfilehash: d3db9bee0558cac5fb4f5b8fb4ab67a35ce0f141
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-release-notes"></a><span data-ttu-id="28d81-103">Заметки о выпуске каталога данных Azure</span><span class="sxs-lookup"><span data-stu-id="28d81-103">Azure Data Catalog release notes</span></span>
## <a name="notes-for-the-november-20-2015-release-of-azure-data-catalog"></a><span data-ttu-id="28d81-104">Заметки о выпуске каталога данных Azure от 20 ноября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="28d81-104">Notes for the November 20, 2015 release of Azure Data Catalog</span></span>
### <a name="opening-data-sources-in-power-bi-desktop"></a><span data-ttu-id="28d81-105">Открытие источников данных в Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="28d81-105">Opening Data Sources in Power BI Desktop</span></span>
<span data-ttu-id="28d81-106">При использовании параметра «Открыть в Power BI Desktop» на портале **каталога данных Azure** у пользователей может возникнуть одна из двух проблем в приложении Power BI Desktop:</span><span class="sxs-lookup"><span data-stu-id="28d81-106">When using the "Open in Power BI Desktop" option from the **Azure Data Catalog** portal, users may encounter one of two problems in the Power BI Desktop application:</span></span>

* <span data-ttu-id="28d81-107">Отображается диалоговое окно с заголовком «Не удается в открыть документ».</span><span class="sxs-lookup"><span data-stu-id="28d81-107">A dialog box with the title "Unable to Open Document" is displayed</span></span>
* <span data-ttu-id="28d81-108">Приложение Power BI Desktop открывается, но файл отображается пустым.</span><span class="sxs-lookup"><span data-stu-id="28d81-108">The Power BI Desktop application opens, but the file appears to be empty</span></span>

<span data-ttu-id="28d81-109">В каждом случае проблему можно устранить, скачав и установив последнюю версию Power BI Desktop с сайта [PowerBI.com](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="28d81-109">For each situation, the problem can be resolved by downloading and installing the latest version of Power BI Desktop from [PowerBI.com](https://powerbi.com).</span></span>

## <a name="notes-for-the-november-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="28d81-110">Заметки о выпуске каталога данных Azure от 13 ноября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="28d81-110">Notes for the November 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-teradata"></a><span data-ttu-id="28d81-111">Регистрация и подключение к Teradata</span><span class="sxs-lookup"><span data-stu-id="28d81-111">Registering and connecting to Teradata</span></span>
<span data-ttu-id="28d81-112">При подключении к источникам данных Teradata у пользователей должны быть установлен драйвер ODBC Teradata, соответствующий разрядности (32-разрядной или 64-разрядной версии) используемого программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="28d81-112">When connecting to Teradata data sources users must have installed the correct Teradata ODBC driver that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

<span data-ttu-id="28d81-113">На дату выпуска этого соединителя Active Directory самый последний [драйвер ODBC Teradata для Windows (вер. 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) совместим с Office 2013, но не с Office 2016.</span><span class="sxs-lookup"><span data-stu-id="28d81-113">As of this ADC release date, the most recent [Teradata ODBC driver for windows ( version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatible with Office 2013, but not with Office 2016.</span></span>

## <a name="notes-for-the-july-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="28d81-114">Заметки о выпуске каталога данных Azure от 13 июля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="28d81-114">Notes for the July 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-oracle-database"></a><span data-ttu-id="28d81-115">Регистрация и подключение к базе данных Oracle</span><span class="sxs-lookup"><span data-stu-id="28d81-115">Registering and connecting to Oracle Database</span></span>
<span data-ttu-id="28d81-116">При подключении к источникам данных базы данных Oracle у пользователей должны быть установлены правильные драйверы Oracle, которые соответствуют разрядности (32-разрядной или 64-разрядной версии) используемого программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="28d81-116">When connecting to Oracle Database data sources users must have installed the correct Oracle drivers that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

* <span data-ttu-id="28d81-117">При регистрации источников данных Oracle на компьютере под управлением 32-разрядной версии Windows будут использоваться 32-разрядные драйверы Oracle.</span><span class="sxs-lookup"><span data-stu-id="28d81-117">When registering Oracle data sources on a computer running 32-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="28d81-118">При регистрации источников данных Oracle на компьютере под управлением 64-разрядной версии Windows будут использоваться 64-разрядные драйверы Oracle.</span><span class="sxs-lookup"><span data-stu-id="28d81-118">When registering Oracle data sources on a computer running 64-bit Windows, the 64-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="28d81-119">При подключении к источникам данных Oracle с помощью Excel на компьютере с 32-разрядной версией Microsoft Office, в том числе под управлением 64-разрядной версии Windows, будут использоваться 32-разрядные драйверы Oracle.</span><span class="sxs-lookup"><span data-stu-id="28d81-119">When connecting to Oracle data sources using Excel on a computer running the 32-bit version of Microsoft Office, including on 64-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="28d81-120">При подключении к источникам данных Oracle с помощью Excel на компьютере с 64-разрядной версией Microsoft Office будут использоваться 64-разрядные драйверы Oracle.</span><span class="sxs-lookup"><span data-stu-id="28d81-120">When connecting to Oracle data sources using Excel on a computer running the 64-bit version of Microsoft Office, the 64-bit Oracle drivers will be used</span></span>

### <a name="registering-and-connecting-to-sql-server-reporting-services"></a><span data-ttu-id="28d81-121">Регистрация и подключение к SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="28d81-121">Registering and connecting to SQL Server Reporting Services</span></span>
<span data-ttu-id="28d81-122">Поддержка источников данных служб SQL Server Reporting Services (SSRS) в настоящее время ограничена только серверами в собственном режиме.</span><span class="sxs-lookup"><span data-stu-id="28d81-122">Support for SQL Server Reporting Services (SSRS) data sources is currently limited to Native Mode servers only.</span></span> <span data-ttu-id="28d81-123">Поддержка служб SSRS в режиме интеграции с SharePoint будет добавлена в более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="28d81-123">Support for SSRS in SharePoint mode will be added in a later release.</span></span>

### <a name="opening-data-assets-in-excel"></a><span data-ttu-id="28d81-124">Открытие ресурсов данных в Excel</span><span class="sxs-lookup"><span data-stu-id="28d81-124">Opening data assets in Excel</span></span>
<span data-ttu-id="28d81-125">При открытии ресурсов данных в Microsoft Excel на портале **каталога данных Azure** пользователям может быть отображено диалоговое окно **Microsoft Excel Security Notice** (Уведомление безопасности Microsoft Excel).</span><span class="sxs-lookup"><span data-stu-id="28d81-125">When opening data assets in Microsoft Excel from the **Azure Data Catalog** portal, users may be prompted with a **Microsoft Excel Security Notice** dialog box.</span></span> <span data-ttu-id="28d81-126">Это стандартное ожидаемое поведение, и пользователи могут выбрать **Включить** для продолжения.</span><span class="sxs-lookup"><span data-stu-id="28d81-126">This is standard, expected behavior, and users can select **Enable** to continue.</span></span>

<span data-ttu-id="28d81-127">Подробнее об этом см. в статье [Включение или отключение предупреждений системы безопасности о ссылках и файлах с подозрительных веб-сайтов](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span><span class="sxs-lookup"><span data-stu-id="28d81-127">For more information, see [Enable or disable security alerts about links and files from suspicious websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span></span>

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a><span data-ttu-id="28d81-128">Конфигурация прокси-сервера и политики, а также регистрация источника данных</span><span class="sxs-lookup"><span data-stu-id="28d81-128">Proxy and policy configuration and data source registration</span></span>
<span data-ttu-id="28d81-129">Пользователи могут столкнуться с ситуацией, когда они могут войти на портал каталога данных Azure, но при попытке входа на средство регистрации источника данных отображается сообщение об ошибке, которая запрещает вход в систему.</span><span class="sxs-lookup"><span data-stu-id="28d81-129">Users may encounter a situation where they can log on to the Azure Data Catalog portal, but when they attempt to log on to the data source registration tool they encounter an error message that prevents them from logging on.</span></span>

<span data-ttu-id="28d81-130">Существуют две возможные причины такого проблемного поведения.</span><span class="sxs-lookup"><span data-stu-id="28d81-130">There are two potential causes for this problem behavior:</span></span>

<span data-ttu-id="28d81-131">**Причина 1: конфигурация служб федерации Active Directory**. Инструмент регистрации источника данных использует аутентификацию с помощью форм для проверки входа пользователя, используя данные Active Directory.</span><span class="sxs-lookup"><span data-stu-id="28d81-131">**Cause 1: Active Directory Federation Services configuration** The data source registration tool uses Forms Authentication to validate user logons against Active Directory.</span></span> <span data-ttu-id="28d81-132">Для успешного входа в систему администратор Active Directory должен включить проверку подлинности форм в глобальную политику проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="28d81-132">For successful logon, Forms Authentication must be enabled in the Global Authentication Policy by an Active Directory administrator.</span></span>

<span data-ttu-id="28d81-133">В некоторых ситуациях эта ошибка может происходить только в том случае, если пользователь находится в локальной сети, или только в том случае, если пользователь подключается из-за пределов сети компании.</span><span class="sxs-lookup"><span data-stu-id="28d81-133">In some situations, this error behavior may occur only when the user is on the company network, or only when the user is connecting from outside the company network.</span></span> <span data-ttu-id="28d81-134">Глобальная политика проверки подлинности позволяет включить методы проверки подлинности отдельно для интрасети и экстрасети.</span><span class="sxs-lookup"><span data-stu-id="28d81-134">The Global Authentication Policy allows authentication methods to be enabled separately for intranet and extranet connections.</span></span> <span data-ttu-id="28d81-135">Ошибки входа в систему могут возникать, если не включена проверка подлинности форм для сети, из которой пользователь подключается.</span><span class="sxs-lookup"><span data-stu-id="28d81-135">Logon errors may occur if Forms Authentication is not enabled for the network from which the user is connecting.</span></span>

<span data-ttu-id="28d81-136">Подробнее: [Настройка политик проверки подлинности](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="28d81-136">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>

<span data-ttu-id="28d81-137">**Причина 2: конфигурация прокси-сервера сети**. Если в корпоративной сети используется прокси-сервер, инструмент регистрации не может подключиться к Azure Active Directory через прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="28d81-137">**Cause 2: Network proxy configuration** If the corporate network uses a proxy server, the registration tool may not be able to connect to Azure Active Directory through the proxy.</span></span> <span data-ttu-id="28d81-138">Пользователи могут проверить средство регистрации, изменив файл конфигурации средства и добавив в файл этот раздел.</span><span class="sxs-lookup"><span data-stu-id="28d81-138">Users can ensure that the registration tool by editing the tool’s configuration file, adding this section to the file:</span></span>

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


<span data-ttu-id="28d81-139">Чтобы найти файл RegistrationTool.exe.config, запустите средство регистрации и откройте программу диспетчера задач Windows.</span><span class="sxs-lookup"><span data-stu-id="28d81-139">To locate the RegistrationTool.exe.config file, launch the registration tool, and then open the Windows Task Manager utility.</span></span> <span data-ttu-id="28d81-140">На вкладке "Сведения" в диспетчере задач щелкните правой кнопкой мыши RegistrationTool.exe и выберите во всплывающем меню "Открыть расположение файла".</span><span class="sxs-lookup"><span data-stu-id="28d81-140">On the Details tab in Task manager, right-click on RegistrationTool.exe and choose Open file location from the pop-up menu.</span></span>
