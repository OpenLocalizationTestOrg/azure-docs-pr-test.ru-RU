---
title: "aaaConnect tooAzure Excel в службах Analysis Services | Документы Microsoft"
description: "Узнайте, как tooconnect tooan Azure служб Analysis Services с помощью Excel."
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
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="7fb0d-103">Подключение с помощью Excel</span><span class="sxs-lookup"><span data-stu-id="7fb0d-103">Connect with Excel</span></span>

<span data-ttu-id="7fb0d-104">После создания сервера в Azure и развернуть tooit табличной модели, вы будете готовы tooconnect и приступить к изучению данных.</span><span class="sxs-lookup"><span data-stu-id="7fb0d-104">Once you've created a server in Azure, and deployed a tabular model tooit, you're ready tooconnect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="7fb0d-105">Подключение в Excel</span><span class="sxs-lookup"><span data-stu-id="7fb0d-105">Connect in Excel</span></span>

<span data-ttu-id="7fb0d-106">Соединение сервера tooa в Excel поддерживается с помощью получения данных в Excel 2016.</span><span class="sxs-lookup"><span data-stu-id="7fb0d-106">Connecting tooa server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="7fb0d-107">Подключение с помощью мастера импорта таблиц hello в PowerPivot не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="7fb0d-107">Connecting by using hello Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="7fb0d-108">**tooconnect в Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="7fb0d-108">**tooconnect in Excel 2016**</span></span>

1. <span data-ttu-id="7fb0d-109">В Excel 2016 hello **данные** ленты, нажмите кнопку **внешние данные** > **из других источников** > **из служб Analysis Services** .</span><span class="sxs-lookup"><span data-stu-id="7fb0d-109">In Excel 2016, on hello **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="7fb0d-110">В hello мастер подключения данных, в **имя сервера**, введите имя сервера hello, включая протокол и URI.</span><span class="sxs-lookup"><span data-stu-id="7fb0d-110">In hello Data Connection Wizard, in **Server name**, enter hello server name including protocol and URI.</span></span> <span data-ttu-id="7fb0d-111">Затем в **учетные данные входа в систему**выберите **hello используйте следующие имя пользователя и пароль**, а затем введите имя пользователя организации hello, например nancy@adventureworks.comи пароль.</span><span class="sxs-lookup"><span data-stu-id="7fb0d-111">Then, in **Logon credentials**, select **Use hello following User Name and Password**, and then type hello organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Подключение из Excel: вход](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="7fb0d-113">В **Выбор базы данных и таблицы**, выберите hello базы данных и модели или перспективе и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="7fb0d-113">In **Select Database and Table**, select hello database and model or perspective, and then click **Finish**.</span></span>
   
    ![Подключение из Excel: выбор модели](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="7fb0d-115">См. также</span><span class="sxs-lookup"><span data-stu-id="7fb0d-115">See also</span></span>
<span data-ttu-id="7fb0d-116">[Клиентские библиотеки](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="7fb0d-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="7fb0d-117">Управление службами Analysis Services</span><span class="sxs-lookup"><span data-stu-id="7fb0d-117">Manage your server</span></span>](analysis-services-manage.md)     


