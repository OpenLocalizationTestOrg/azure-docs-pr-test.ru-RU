---
title: "aaaHow toomigrate логику приложения tooschema версии 2015-08-01-preview | Документы Microsoft"
description: "Можно легко перенести на логику приложения toohello последнюю версию схемы. Просто следуйте приведенным здесь инструкциям."
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
ms.openlocfilehash: c7b42aaec547eddd28b0c649a3c0625047f9f805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a><span data-ttu-id="a6b7a-104">Как toomigrate логику приложения tooschema версии 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="a6b7a-104">How toomigrate logic apps tooschema version 2015-08-01-preview</span></span>
<span data-ttu-id="a6b7a-105">toomove существующего логику приложения toohello новой схемы, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a6b7a-105">toomove your existing logic apps toohello new schema, do hello following:</span></span>  

1. <span data-ttu-id="a6b7a-106">Откройте приложение логики в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a6b7a-106">Open your logic app in hello Azure portal</span></span>  
2. <span data-ttu-id="a6b7a-107">Нажмите кнопку "Обновить схему".</span><span class="sxs-lookup"><span data-stu-id="a6b7a-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="a6b7a-108">![Значок API][step1] </span><span class="sxs-lookup"><span data-stu-id="a6b7a-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="a6b7a-109">Страница приветствия обновления схемы содержит сведения, а также документа tooa ссылки, которые предоставляют сведения об улучшениях hello в новую схему hello: ![значок API][step2]</span><span class="sxs-lookup"><span data-stu-id="a6b7a-109">hello Update Schema page displays and provides a link tooa document that provide details on hello improvements in hello new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="a6b7a-110">При выборе **обновления схемы**, мы автоматическое выполнение шагов миграции hello и предоставить вывод кода hello для вас.</span><span class="sxs-lookup"><span data-stu-id="a6b7a-110">When you select **Update Schema**, we automatically run hello migration steps and provide hello code output for you.</span></span> <span data-ttu-id="a6b7a-111">Можно использовать этот tooupdate, ваше определение тем не менее, убедитесь, выполните рекомендованные методы программирования, например те, описанные в hello **рекомендации** ниже.</span><span class="sxs-lookup"><span data-stu-id="a6b7a-111">You can use this tooupdate your definition, however, ensure you follow good coding practices such as those outlined in hello **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a><span data-ttu-id="a6b7a-112">Рекомендации по переносу на логику приложения toohello последнюю версию схемы:</span><span class="sxs-lookup"><span data-stu-id="a6b7a-112">Best practices when migrating your Logic apps toohello latest schema version:</span></span>
* <span data-ttu-id="a6b7a-113">Сценарий миграции hello копирования tooa новая логика приложения — не перезаписывали hello старого один до завершения перенесенных подтверждена hello и тестирования приложения, работают нормально.</span><span class="sxs-lookup"><span data-stu-id="a6b7a-113">Copy hello migrated script tooa new Logic App - don't overwrite hello old one until you've completed your testing and confirmed hello migrated app works as expected.</span></span>
* <span data-ttu-id="a6b7a-114">Протестируйте приложение логики, **прежде** чем помещать его в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="a6b7a-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="a6b7a-115">После завершения миграции начало обновления вашей hello логику приложения toouse [управляемых API](apis-list.md) там, где это возможно.</span><span class="sxs-lookup"><span data-stu-id="a6b7a-115">After migration completes, start updating your Logic apps toouse hello [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="a6b7a-116">Например, вы можете теперь использовать Dropbox версии 2 там, где использовали Dropbox версии 1.</span><span class="sxs-lookup"><span data-stu-id="a6b7a-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="a6b7a-117">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="a6b7a-117">What's next</span></span>
* [<span data-ttu-id="a6b7a-118">Узнайте, как toomanually перенести свои приложения логики</span><span class="sxs-lookup"><span data-stu-id="a6b7a-118">Learn how toomanually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






