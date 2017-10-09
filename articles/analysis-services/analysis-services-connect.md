---
title: "aaaConnect tooAzure служб Analysis Services | Документы Microsoft"
description: "Узнайте, как tooconnect tooand получить данные с сервера служб Analysis Services в Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 5df94492feb48034f156b72e83e1009683988fc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-analysis-services-server"></a><span data-ttu-id="71f4b-103">Подключение сервера tooan Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="71f4b-103">Connect tooan Azure Analysis Services server</span></span>

<span data-ttu-id="71f4b-104">В этой статье описан подключающегося tooa сервера с помощью моделирования данных и управления приложениями, например SQL Server Management Studio (SSMS) или SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="71f4b-104">This article describes connecting tooa server by using data modeling and management applications like SQL Server Management Studio (SSMS) or SQL Server Data Tools (SSDT).</span></span> <span data-ttu-id="71f4b-105">Для этого также можно использовать клиентские приложения создания отчетов, такие как Microsoft Excel, Power BI Desktop или пользовательские приложения.</span><span class="sxs-lookup"><span data-stu-id="71f4b-105">Or, with client reporting applications like Microsoft Excel, Power BI Desktop, or custom applications.</span></span> <span data-ttu-id="71f4b-106">Службы Analysis Services tooAzure подключений использования протокола HTTPS.</span><span class="sxs-lookup"><span data-stu-id="71f4b-106">Connections tooAzure Analysis Services use HTTPS.</span></span>

## <a name="client-libraries"></a><span data-ttu-id="71f4b-107">Клиентские библиотеки</span><span class="sxs-lookup"><span data-stu-id="71f4b-107">Client libraries</span></span>
[<span data-ttu-id="71f4b-108">Получить последние клиентские библиотеки hello</span><span class="sxs-lookup"><span data-stu-id="71f4b-108">Get hello latest Client libraries</span></span>](analysis-services-data-providers.md)

<span data-ttu-id="71f4b-109">Все server tooa подключений, независимо от типа требуются обновленные объекты AMO, ADOMD.NET и OLEDB библиотеки tooconnect tooand интерфейс клиента с сервером служб Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="71f4b-109">All connections tooa server, regardless of type, require updated AMO, ADOMD.NET, and OLEDB client libraries tooconnect tooand interface with an Analysis Services server.</span></span> <span data-ttu-id="71f4b-110">Для SSMS, SSDT, Excel 2016 и Power BI последние клиентские библиотеки hello установлены или обновляется ежемесячные выпуски.</span><span class="sxs-lookup"><span data-stu-id="71f4b-110">For SSMS, SSDT, Excel 2016, and Power BI, hello latest client libraries are installed or updated with monthly releases.</span></span> <span data-ttu-id="71f4b-111">Однако в некоторых случаях возможна приложения не имеют последние hello.</span><span class="sxs-lookup"><span data-stu-id="71f4b-111">However, in some cases, it's possible an application may not have hello latest.</span></span> <span data-ttu-id="71f4b-112">Например, при обновлении политики задержки или обновления Office 365 находятся на hello отложенный канала.</span><span class="sxs-lookup"><span data-stu-id="71f4b-112">For example, when policies delay updates, or Office 365 updates are on hello Deferred Channel.</span></span>

## <a name="server-name"></a><span data-ttu-id="71f4b-113">имя сервера;</span><span class="sxs-lookup"><span data-stu-id="71f4b-113">Server name</span></span>

<span data-ttu-id="71f4b-114">При создании сервера служб Analysis Services в Azure, необходимо указать уникальное имя и hello региона, где будет создан toobe сервер hello.</span><span class="sxs-lookup"><span data-stu-id="71f4b-114">When you create an Analysis Services server in Azure, you specify a unique name and hello region where hello server is toobe created.</span></span> <span data-ttu-id="71f4b-115">При указании имени сервера hello в соединении, является схема именования hello server:</span><span class="sxs-lookup"><span data-stu-id="71f4b-115">When specifying hello server name in a connection, hello server naming scheme is:</span></span>

```
<protocol>://<region>/<servername>
```
 <span data-ttu-id="71f4b-116">Где протокола — строка **asazure**, регион — hello Uri, где был создан сервер hello (например, westus.asazure.windows.net) и имя_сервера — hello имя вашего сервера, уникальный в пределах области hello.</span><span class="sxs-lookup"><span data-stu-id="71f4b-116">Where protocol is string **asazure**, region is hello Uri where hello server was created (for example, westus.asazure.windows.net) and servername is hello name of your unique server within hello region.</span></span>

### <a name="get-hello-server-name"></a><span data-ttu-id="71f4b-117">Получить имя сервера hello</span><span class="sxs-lookup"><span data-stu-id="71f4b-117">Get hello server name</span></span>
<span data-ttu-id="71f4b-118">В **портал Azure** > сервера > **Обзор** > **имя сервера**, копировать hello всего сервера имя.</span><span class="sxs-lookup"><span data-stu-id="71f4b-118">In **Azure portal** > server > **Overview** > **Server name**, copy hello entire server name.</span></span> <span data-ttu-id="71f4b-119">Если другим пользователям в организации слишком подключении toothis сервера, можно предоставить это имя сервера с ними.</span><span class="sxs-lookup"><span data-stu-id="71f4b-119">If other users in your organization are connecting toothis server too, you can share this server name with them.</span></span> <span data-ttu-id="71f4b-120">При указании имени сервера, необходимо использовать весь путь hello.</span><span class="sxs-lookup"><span data-stu-id="71f4b-120">When specifying a server name, hello entire path must be used.</span></span>

![Получение имени сервера в Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a><span data-ttu-id="71f4b-122">Строка подключения</span><span class="sxs-lookup"><span data-stu-id="71f4b-122">Connection string</span></span>

<span data-ttu-id="71f4b-123">При подключении tooAzure Analysis Services с помощью hello табличной объектной модели, используйте hello следующие форматы строк подключения:</span><span class="sxs-lookup"><span data-stu-id="71f4b-123">When connecting tooAzure Analysis Services using hello Tabular Object Model, use hello following connection string formats:</span></span>

###### <a name="integrated-azure-active-directory-authentication"></a><span data-ttu-id="71f4b-124">Встроенная проверка подлинности Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71f4b-124">Integrated Azure Active Directory authentication</span></span>
<span data-ttu-id="71f4b-125">Встроенная проверка подлинности продолжается hello кэш учетных данных Azure Active Directory, если он доступен.</span><span class="sxs-lookup"><span data-stu-id="71f4b-125">Integrated authentication picks up hello Azure Active Directory credential cache if available.</span></span> <span data-ttu-id="71f4b-126">В противном случае отображается окно входа Azure hello.</span><span class="sxs-lookup"><span data-stu-id="71f4b-126">If not, hello Azure login window is shown.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a><span data-ttu-id="71f4b-127">Проверка подлинности Azure Active Directory с использованием имени пользователя и пароля</span><span class="sxs-lookup"><span data-stu-id="71f4b-127">Azure Active Directory authentication with username and password</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a><span data-ttu-id="71f4b-128">Проверка подлинности Windows (встроенный механизм безопасности)</span><span class="sxs-lookup"><span data-stu-id="71f4b-128">Windows authentication (Integrated security)</span></span>
<span data-ttu-id="71f4b-129">Используйте учетную запись Windows hello работают hello текущего процесса.</span><span class="sxs-lookup"><span data-stu-id="71f4b-129">Use hello Windows account running hello current process.</span></span>

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a><span data-ttu-id="71f4b-130">Подключение с помощью ODC-файла</span><span class="sxs-lookup"><span data-stu-id="71f4b-130">Connect using an .odc file</span></span>
<span data-ttu-id="71f4b-131">Более старые версии Excel позволяет пользователям подключаться tooan сервера Azure Analysis Services с помощью файла подключения к данным Office (ODC).</span><span class="sxs-lookup"><span data-stu-id="71f4b-131">With older versions of Excel, users can connect tooan Azure Analysis Services server by using an Office Data Connection (.odc) file.</span></span> <span data-ttu-id="71f4b-132">toolearn более, в разделе [создайте файл подключения к данным Office (ODC)](analysis-services-odc.md).</span><span class="sxs-lookup"><span data-stu-id="71f4b-132">toolearn more, see [Create an Office Data Connection (.odc) file](analysis-services-odc.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="71f4b-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="71f4b-133">Next steps</span></span>
<span data-ttu-id="71f4b-134">[Подключение с помощью Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="71f4b-134">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
<span data-ttu-id="71f4b-135">[Подключение с помощью Power BI](analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="71f4b-135">[Connect with Power BI](analysis-services-connect-pbi.md) </span></span>  
[<span data-ttu-id="71f4b-136">Управление службами Analysis Services</span><span class="sxs-lookup"><span data-stu-id="71f4b-136">Manage your server</span></span>](analysis-services-manage.md)   

