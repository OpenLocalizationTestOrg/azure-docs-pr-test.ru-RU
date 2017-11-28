---
title: "aaaConnect tooAzure служб Analysis Services с помощью Power BI | Документы Microsoft"
description: "Узнайте, как tooconnect tooan Azure служб Analysis Services с помощью Power BI."
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
ms.openlocfilehash: f6c4cdec6edb92900ad2e552e23a4d9172ba9b84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-power-bi"></a><span data-ttu-id="41430-103">Подключение с помощью Power BI</span><span class="sxs-lookup"><span data-stu-id="41430-103">Connect with Power BI</span></span>

<span data-ttu-id="41430-104">После создания сервера в Azure и развернуть tooit табличной модели, пользователи в вашей организации будут готовы tooconnect и приступить к изучению данных.</span><span class="sxs-lookup"><span data-stu-id="41430-104">Once you've created a server in Azure, and deployed a tabular model tooit, users in your organization are ready tooconnect and begin exploring data.</span></span> 

> [!TIP]
> <span data-ttu-id="41430-105">Убедиться, что последняя версия toouse hello объекта [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="41430-105">Be sure toouse hello latest version of [Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span></span>
> 
> 
  
## <a name="connect-in-power-bi-desktop"></a><span data-ttu-id="41430-106">Подключение в Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="41430-106">Connect in Power BI Desktop</span></span>

1. <span data-ttu-id="41430-107">В Power BI Desktop выберите **Получить данные** > **Azure** > **База данных Azure Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="41430-107">In Power BI Desktop, click **Get Data** > **Azure** > **Azure Analysis Services database**.</span></span>

2. <span data-ttu-id="41430-108">В **сервера**, введите имя сервера hello.</span><span class="sxs-lookup"><span data-stu-id="41430-108">In **Server**, enter hello server name.</span></span> 
    
    <span data-ttu-id="41430-109">Быть убедиться, что tooinclude hello полный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="41430-109">Be sure tooinclude hello full URL.</span></span> <span data-ttu-id="41430-110">Например, asazure://westcentralus.asazure.windows.net/advworks.</span><span class="sxs-lookup"><span data-stu-id="41430-110">For example, asazure://westcentralus.asazure.windows.net/advworks.</span></span>

3. <span data-ttu-id="41430-111">В **базы данных**, если известно имя hello hello базы данных табличной модели или перспективы требуется tooconnect для, вставьте его здесь.</span><span class="sxs-lookup"><span data-stu-id="41430-111">In **Database**, if you know hello name of hello tabular model database or perspective you want tooconnect to, paste it here.</span></span> <span data-ttu-id="41430-112">В противном случае вы можете оставить это поле пустым и выбрать базу данных или перспективу позже.</span><span class="sxs-lookup"><span data-stu-id="41430-112">Otherwise, you can leave this field blank and select a database or perspective later.</span></span>

4. <span data-ttu-id="41430-113">Оставьте по умолчанию hello **Connect live** параметр, а затем нажмите клавишу **Connect**.</span><span class="sxs-lookup"><span data-stu-id="41430-113">Leave hello default **Connect live** option, then press **Connect**.</span></span> 

5. <span data-ttu-id="41430-114">При отображении запроса введите свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="41430-114">If prompted, enter your login credentials.</span></span> 

6. <span data-ttu-id="41430-115">В **Навигатор**, разверните сервер hello, а затем выберите hello модель или перспективу, нужно tooconnect для, нажмите кнопку **Connect**.</span><span class="sxs-lookup"><span data-stu-id="41430-115">In **Navigator**, expand hello server, then select hello model or perspective you want tooconnect to, then click **Connect**.</span></span> <span data-ttu-id="41430-116">Выберите модели или перспективы tooshow все объекты hello для этого представления.</span><span class="sxs-lookup"><span data-stu-id="41430-116">Click  a model or perspective tooshow all hello objects for that view.</span></span>

    <span data-ttu-id="41430-117">Hello модели в Power BI Desktop откроется пустой отчет в представлении отчета.</span><span class="sxs-lookup"><span data-stu-id="41430-117">hello model opens in Power BI Desktop with a blank report in Report view.</span></span> <span data-ttu-id="41430-118">Список полей Hello отображает все объекты модели не скрыты.</span><span class="sxs-lookup"><span data-stu-id="41430-118">hello Fields list displays all non-hidden model objects.</span></span> <span data-ttu-id="41430-119">Состояние подключения отображается в правом нижнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="41430-119">Connection status is displayed in hello lower-right corner.</span></span>

## <a name="connect-in-power-bi-service"></a><span data-ttu-id="41430-120">Подключение в Power BI (служба)</span><span class="sxs-lookup"><span data-stu-id="41430-120">Connect in Power BI (service)</span></span>

1. <span data-ttu-id="41430-121">Создайте файл Power BI Desktop, имеет модель tooyour активное подключение на сервере.</span><span class="sxs-lookup"><span data-stu-id="41430-121">Create a Power BI Desktop file that has a live connection tooyour model on your server.</span></span>
2. <span data-ttu-id="41430-122">В [Power BI](https://powerbi.microsoft.com) последовательно выберите **Получить данные** > **Файлы**.</span><span class="sxs-lookup"><span data-stu-id="41430-122">In [Power BI](https://powerbi.microsoft.com), click **Get Data** > **Files**.</span></span> <span data-ttu-id="41430-123">Найдите и выберите созданный файл.</span><span class="sxs-lookup"><span data-stu-id="41430-123">Locate and select your file.</span></span>



## <a name="see-also"></a><span data-ttu-id="41430-124">См. также</span><span class="sxs-lookup"><span data-stu-id="41430-124">See also</span></span>
<span data-ttu-id="41430-125">[Подключение tooAzure Analysis Services](analysis-services-connect.md) </span><span class="sxs-lookup"><span data-stu-id="41430-125">[Connect tooAzure Analysis Services](analysis-services-connect.md) </span></span>  
[<span data-ttu-id="41430-126">Клиентские библиотеки</span><span class="sxs-lookup"><span data-stu-id="41430-126">Client libraries</span></span>](analysis-services-data-providers.md)

