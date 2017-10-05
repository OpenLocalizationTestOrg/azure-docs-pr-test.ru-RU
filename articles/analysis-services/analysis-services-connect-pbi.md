---
title: "Подключение к Azure Analysis Services с помощью Power BI | Документы Майкрософт"
description: "Сведения о подключении к серверу Azure Analysis Services с помощью Power BI."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3a2af043feddb4a1d6d63f50e838c8a39035449f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="15b72-103">Подключение с помощью Power BI</span><span class="sxs-lookup"><span data-stu-id="15b72-103">Connect with Power BI</span></span>

<span data-ttu-id="15b72-104">Когда вы создадите Azure сервер и развернете в него табличную модель, пользователи вашей организации смогут подключиться к нему для использования данных.</span><span class="sxs-lookup"><span data-stu-id="15b72-104">Once you've created a server in Azure, and deployed a tabular model to it, users in your organization are ready to connect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="15b72-105">Обязательно используйте последнюю версию [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="15b72-105">Be sure to use the latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="15b72-106">Подключение в Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="15b72-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="15b72-107">В Power BI Desktop выберите **Получить данные** > **Azure** > **База данных Azure Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="15b72-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="15b72-108">В поле **Сервер** укажите имя сервера.</span><span class="sxs-lookup"><span data-stu-id="15b72-108">In **Server**, enter the server name.</span></span> 
    
    <span data-ttu-id="15b72-109">Не забудьте включить полный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="15b72-109">Be sure to include the full URL.</span></span> <span data-ttu-id="15b72-110">Например, asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="15b72-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="15b72-111">В поле **База данных** вставьте имя базы данных табличной модели или перспективы, к которой нужно подключиться, если вы знаете это имя.</span><span class="sxs-lookup"><span data-stu-id="15b72-111">In **Database**, if you know the name of the tabular model database or perspective you want to connect to, paste it here.</span></span> <span data-ttu-id="15b72-112">В противном случае вы можете оставить это поле пустым и выбрать базу данных или перспективу позже.</span><span class="sxs-lookup"><span data-stu-id="15b72-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="15b72-113">Оставьте стандартное значение **Подключение в реальном времени**, а затем нажмите **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="15b72-113">Leave the default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="15b72-114">При отображении запроса введите свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="15b72-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="15b72-115">В разделе **Навигатор** разверните узел сервера и выберите модель или перспективу, к которой вы хотите подключиться, затем нажмите **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="15b72-115">In **Navigator**, expand the server, then select the model or perspective you want to connect to, then click **Connect**.</span></span> <span data-ttu-id="15b72-116">Щелкнув модель или перспективу, можно отобразить все объекты для этого представления.</span><span class="sxs-lookup"><span data-stu-id="15b72-116">Click  a model or perspective to show all the objects for that view.</span></span>

    <span data-ttu-id="15b72-117">Модель открывается в Power BI Desktop с пустым отчетом в представлении "Отчет".</span><span class="sxs-lookup"><span data-stu-id="15b72-117">The model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="15b72-118">Список "Поля" содержит все нескрытые объекты модели.</span><span class="sxs-lookup"><span data-stu-id="15b72-118">The Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="15b72-119">Состояние подключения отображается в правом нижнем углу.</span><span class="sxs-lookup"><span data-stu-id="15b72-119">Connection status is displayed in the lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="15b72-120">Подключение в Power BI (служба)</span><span class="sxs-lookup"><span data-stu-id="15b72-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="15b72-121">Создайте файл Power BI Desktop с возможностью активного подключения к нужной модели на сервере.</span><span class="sxs-lookup"><span data-stu-id="15b72-121">Create a Power BI Desktop file that has a live connection to your model on your server.</span></span>
2. <span data-ttu-id="15b72-122">В [Power BI](https://powerbi.microsoft.com) последовательно выберите **Получить данные** > **Файлы**.</span><span class="sxs-lookup"><span data-stu-id="15b72-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="15b72-123">Найдите и выберите созданный файл.</span><span class="sxs-lookup"><span data-stu-id="15b72-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="15b72-124">См. также</span><span class="sxs-lookup"><span data-stu-id="15b72-124">See also</span></span>
<span data-ttu-id="15b72-125">[Подключение к службам Azure Analysis Services](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="15b72-125">[Connect to Azure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="15b72-126">Клиентские библиотеки</span><span class="sxs-lookup"><span data-stu-id="15b72-126">Client libraries</span></span>](analysis-services-data-providers.md)

