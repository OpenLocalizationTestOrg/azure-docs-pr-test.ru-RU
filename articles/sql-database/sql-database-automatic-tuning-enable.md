---
title: "aaaEnable автоматической настройки для базы данных SQL Azure | Документы Microsoft"
description: "Вы можете легко включить автоматическую настройку для базы данных SQL Azure."
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="bf542-103">Включение автоматической настройки</span><span class="sxs-lookup"><span data-stu-id="bf542-103">Enable automatic tuning</span></span>

<span data-ttu-id="bf542-104">База данных SQL Azure — это служба автоматически управляемых данных, которая постоянно отслеживает запросы и определяет действие hello, что вы сможете выполнять tooimprove производительность рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="bf542-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies hello action that you can perform tooimprove performance of your workload.</span></span> <span data-ttu-id="bf542-105">Вы можете просматривать рекомендации и вручную применять их, или позволить базе данных SQL Azure автоматически применять действия по исправлению, что известно как **режим автоматической настройки**.</span><span class="sxs-lookup"><span data-stu-id="bf542-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="bf542-106">Можно включить автоматическую настройку на приветствия сервера или базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="bf542-106">Automatic tuning can be enabled at hello server or hello database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="bf542-107">Включение автоматической настройки на сервере</span><span class="sxs-lookup"><span data-stu-id="bf542-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="bf542-108">tooenable автоматической настройки на сервере базы данных SQL Azure перейдите toohello server в Azure, портала и затем выберите **автоматической настройки** в меню hello.</span><span class="sxs-lookup"><span data-stu-id="bf542-108">tooenable automatic tuning on Azure SQL Database server, navigate toohello server in Azure portal and then select **Automatic tuning** in hello menu.</span></span> <span data-ttu-id="bf542-109">Здравствуйте, выберите параметры автоматической настройки tooenable и выберите **применить**:</span><span class="sxs-lookup"><span data-stu-id="bf542-109">Select hello automatic tuning options you want tooenable and select **Apply**:</span></span>

![сервер;](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="bf542-111">Автоматической настройки параметров на сервере базы данных применяются tooall на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="bf542-111">Automatic tuning options on server are applied tooall databases on hello server.</span></span> <span data-ttu-id="bf542-112">По умолчанию все базы данных наследуют конфигурацию hello их родительский сервер, но это можно переопределить и указанные отдельно для каждой базы данных.</span><span class="sxs-lookup"><span data-stu-id="bf542-112">By default, all databases inherit hello configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="bf542-113">Настройка автоматических параметров для базы данных</span><span class="sxs-lookup"><span data-stu-id="bf542-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="bf542-114">Hello Azure портала позволяет вам tooindividually укажите hello автоматической настройки конфигурации для каждой базы данных.</span><span class="sxs-lookup"><span data-stu-id="bf542-114">hello Azure portal enables you tooindividually specify hello automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="bf542-115">общая рекомендация Hello — toomanage hello автоматической настройки конфигурации на уровне сервера так hello одинаковые параметры конфигурации могут применяться для всех баз данных автоматически.</span><span class="sxs-lookup"><span data-stu-id="bf542-115">hello general recommendation is toomanage hello automatic tuning configuration at server level so hello same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="bf542-116">Настройка автоматической настройки для отдельной базы данных, если hello базы данных отличается, что другие участники hello того же сервера.</span><span class="sxs-lookup"><span data-stu-id="bf542-116">Configure automatic tuning on an individual database if hello database is different that others on hello same server.</span></span>
>

<span data-ttu-id="bf542-117">toohello базы данных в hello портал Azure перейдите tooenable автоматической настройки в одной базе данных, а затем выберите **автоматической настройки**.</span><span class="sxs-lookup"><span data-stu-id="bf542-117">tooenable automatic tuning on a single database, navigate toohello database in hello Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="bf542-118">Можно настроить параметры hello tooinherit одной базы данных, из базы данных hello, выбрав флажок hello или hello конфигурации для базы данных можно задать по отдельности.</span><span class="sxs-lookup"><span data-stu-id="bf542-118">You can configure a single database tooinherit hello settings from hello database by selecting hello checkbox or you can specify hello configuration for a database individually.</span></span>

![База данных](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="bf542-120">После выбора соответствующей конфигурации щелкните **Применить**.</span><span class="sxs-lookup"><span data-stu-id="bf542-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf542-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bf542-121">Next steps</span></span>
* <span data-ttu-id="bf542-122">Чтение hello [автоматической настройки статьи](sql-database-automatic-tuning.md) toolearn Дополнительные сведения об автоматической настройки и как она может помочь вам повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="bf542-122">Read hello [Automatic tuning article](sql-database-automatic-tuning.md) toolearn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="bf542-123">Общие сведения о рекомендациях по производительности базы данных SQL Azure см. в статье [Помощник по работе с базами данных SQL](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="bf542-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="bf542-124">В разделе [подробных сведений о производительности запросов](sql-database-query-performance.md) toolearn о просмотре hello влияние на производительность запросов top.</span><span class="sxs-lookup"><span data-stu-id="bf542-124">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>
