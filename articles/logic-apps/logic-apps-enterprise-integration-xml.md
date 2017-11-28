---
title: "сообщения о aaaWorking с XML в рабочие процессы — приложения логики Azure | Документы Microsoft"
description: "Обработка, проверка, преобразования и обогащения XML сообщения в логику приложения и с помощью бизнес tooscenarios hello пакет интеграции Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 02/27/2017
ms.author: LADocs; mandia
ms.openlocfilehash: f90ae89fef0a4bd17286adbce398e573940bb790
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="bd9d0-103">Проверка и преобразование XML, кодирование и декодирование неструктурированных файлов и обогащение сообщений в приложениях логики</span><span class="sxs-lookup"><span data-stu-id="bd9d0-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="bd9d0-104">С помощью приложения логики, имеется XML-сообщения hello возможность tooprocess, которые отправляют и получают.</span><span class="sxs-lookup"><span data-stu-id="bd9d0-104">Using logic apps, you have hello ability tooprocess XML messages that you send and receive.</span></span> <span data-ttu-id="bd9d0-105">Этот компонент входит в состав hello пакет интеграции Enterprise.</span><span class="sxs-lookup"><span data-stu-id="bd9d0-105">This feature is included with hello Enterprise Integration Pack.</span></span> <span data-ttu-id="bd9d0-106">Для этих пользователей на фоне BizTalk Server hello пакет интеграции Enterprise предоставляет аналогичные возможности tootransform и проверки сообщений, работать с плоскими файлами и даже использовать XPath tooenrich или извлечения определенного свойства из сообщения.</span><span class="sxs-lookup"><span data-stu-id="bd9d0-106">For those users with a BizTalk Server background, hello Enterprise Integration Pack gives you similar abilities tootransform and validate messages, work with flat files, and even use XPath tooenrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="bd9d0-107">Для пользователей, которым новые toothis места на диске эти функции разверните обработку сообщений в рамках рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="bd9d0-107">For those users who are new toothis space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="bd9d0-108">Например если вы являетесь в бизнес-сценарии и работать с определенной схемы XML, можно использовать пакет интеграции Enterprise tooenhance hello как компании обрабатывает эти сообщения.</span><span class="sxs-lookup"><span data-stu-id="bd9d0-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use hello Enterprise Integration Pack tooenhance how your company processes these messages.</span></span> 

<span data-ttu-id="bd9d0-109">Hello пакет интеграции Enterprise включает в себя:</span><span class="sxs-lookup"><span data-stu-id="bd9d0-109">hello Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="bd9d0-110">[Проверка XML](logic-apps-enterprise-integration-xml-validation.md "Узнайте о проверке сообщений XML") позволяет проверить входящее или исходящее сообщение XML на соответствие указанной схеме.</span><span class="sxs-lookup"><span data-stu-id="bd9d0-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="bd9d0-111">[Преобразование XML](../logic-apps/logic-apps-enterprise-integration-transform.md "Дополнительные сведения о преобразования сообщений XML и карт") - преобразования или настроить на основе требований или требований hello участника XML-сообщения.</span><span class="sxs-lookup"><span data-stu-id="bd9d0-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or hello requirements of a partner.</span></span>
* <span data-ttu-id="bd9d0-112">[Кодирование и декодирование неструктурированных файлов](logic-apps-enterprise-integration-flatfile.md "См. дополнительные сведения о кодировании и декодировании неструктурированных файлов") позволяет кодировать и декодировать неструктурированный файл.</span><span class="sxs-lookup"><span data-stu-id="bd9d0-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="bd9d0-113">Например, SAP принимает и отправляет IDOC-файлы в виде неструктурированных файлов.</span><span class="sxs-lookup"><span data-stu-id="bd9d0-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="bd9d0-114">Многие платформы интеграции создают сообщения XML, включая Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="bd9d0-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="bd9d0-115">Таким образом можно создать приложение логики, что кодировщик неструктурированных файлов использует hello слишком «преобразование» tooflat файлы XML-файлов.</span><span class="sxs-lookup"><span data-stu-id="bd9d0-115">So, you can create a logic app that uses hello flat file encoder too"convert" XML files tooflat files.</span></span> 
* <span data-ttu-id="bd9d0-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - обогатить сообщение и извлечения определенного свойства из сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="bd9d0-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from hello message.</span></span> <span data-ttu-id="bd9d0-117">После этого можно hello использования извлеченных назначения tooa сообщения hello tooroute свойства или промежуточной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="bd9d0-117">You can then use hello extracted properties tooroute hello message tooa destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="bd9d0-118">Попробуйте сейчас</span><span class="sxs-lookup"><span data-stu-id="bd9d0-118">Try it out</span></span>
<span data-ttu-id="bd9d0-119">[Развертывание приложения, полностью логику ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (пример использования GitHub) с помощью функции hello XML в логику приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9d0-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using hello XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="bd9d0-120">Подробнее</span><span class="sxs-lookup"><span data-stu-id="bd9d0-120">Learn more</span></span>
[<span data-ttu-id="bd9d0-121">Дополнительные сведения о hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="bd9d0-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise")
