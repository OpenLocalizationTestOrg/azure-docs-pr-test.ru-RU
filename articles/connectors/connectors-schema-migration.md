---
title: "Перенос приложений логики в версию схемы 2015-08-01-preview | Документация Майкрософт"
description: "Вы можете легко перенести приложения логики в последнюю версию схемы. Просто следуйте приведенным здесь инструкциям."
services: logic-apps
documentationcenter: 
author: MSFTMAN
manager: erikre
editor: 
tags: connectors
ms.assetid: 3e177e49-fd69-43e9-9b9b-218abb250c31
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: deonhe
ms.openlocfilehash: a5a73a9f124e5339b61dbc49021444a208a471f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-logic-apps-to-schema-version-2015-08-01-preview"></a><span data-ttu-id="71d50-104">Перенос приложений логики в версию схемы 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="71d50-104">How to migrate logic apps to schema version 2015-08-01-preview</span></span>
<span data-ttu-id="71d50-105">Чтобы переместить существующие приложения логики в новую схему, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="71d50-105">To move your existing logic apps to the new schema, do the following:</span></span>  

1. <span data-ttu-id="71d50-106">Откройте приложение логики на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="71d50-106">Open your logic app in the Azure portal</span></span>  
2. <span data-ttu-id="71d50-107">Нажмите кнопку "Обновить схему".</span><span class="sxs-lookup"><span data-stu-id="71d50-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="71d50-108">![Значок API][step1] </span><span class="sxs-lookup"><span data-stu-id="71d50-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="71d50-109">На странице "Обновление схемы" отобразятся ссылки на документ, который содержит сведения об улучшениях в новой схеме. ![Значок API][step2]</span><span class="sxs-lookup"><span data-stu-id="71d50-109">The Update Schema page displays and provides a link to a document that provide details on the improvements in the new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="71d50-110">Когда вы нажмете кнопку **Обновить схему**, автоматически запустится процесс миграции и отобразится вывод кода.</span><span class="sxs-lookup"><span data-stu-id="71d50-110">When you select **Update Schema**, we automatically run the migration steps and provide the code output for you.</span></span> <span data-ttu-id="71d50-111">Вы можете использовать эти возможности для обновления своего определения. Но обязательно придерживайтесь рекомендуемых методов программирования, описанных в разделе с **рекомендациями** ниже.</span><span class="sxs-lookup"><span data-stu-id="71d50-111">You can use this to update your definition, however, ensure you follow good coding practices such as those outlined in the **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-to-the-latest-schema-version"></a><span data-ttu-id="71d50-112">Рекомендации по переносу приложений логики в последнюю версию схемы</span><span class="sxs-lookup"><span data-stu-id="71d50-112">Best practices when migrating your Logic apps to the latest schema version:</span></span>
* <span data-ttu-id="71d50-113">Скопируйте перенесенный сценарий в новое приложение логики. Не перезаписывайте старое приложение, пока не завершите тестирование и не убедитесь, что перенесенное приложение работает правильно.</span><span class="sxs-lookup"><span data-stu-id="71d50-113">Copy the migrated script to a new Logic App - don't overwrite the old one until you've completed your testing and confirmed the migrated app works as expected.</span></span>
* <span data-ttu-id="71d50-114">Протестируйте приложение логики, **прежде** чем помещать его в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="71d50-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="71d50-115">Завершив перенос, приступайте к обновлению приложений логики, чтобы использовать [управляемые интерфейсы API](apis-list.md) там, где это возможно.</span><span class="sxs-lookup"><span data-stu-id="71d50-115">After migration completes, start updating your Logic apps to use the [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="71d50-116">Например, вы можете теперь использовать Dropbox версии 2 там, где использовали Dropbox версии 1.</span><span class="sxs-lookup"><span data-stu-id="71d50-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="71d50-117">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="71d50-117">What's next</span></span>
* [<span data-ttu-id="71d50-118">Новая версия схемы 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="71d50-118">Learn how to manually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






