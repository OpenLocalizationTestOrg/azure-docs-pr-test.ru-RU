---
title: "Работа с сообщениями XML в рабочих процессах с помощью Azure Logic Apps | Документация Майкрософт"
description: "Обработка, проверка, преобразование и обогащение сообщений XML в приложениях логики и сценариях B2B с помощью Пакета интеграции Enterprise."
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
ms.openlocfilehash: 3fec4935f5317be4bf8c9e05f1c24a7c05381b1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="d9d0d-103">Проверка и преобразование XML, кодирование и декодирование неструктурированных файлов и обогащение сообщений в приложениях логики</span><span class="sxs-lookup"><span data-stu-id="d9d0d-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="d9d0d-104">С помощью приложений логики можно обрабатывать отправляемые и получаемые сообщения XML.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-104">Using logic apps, you have the ability to process XML messages that you send and receive.</span></span> <span data-ttu-id="d9d0d-105">Эта функция в состав Пакета интеграции Enterprise.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-105">This feature is included with the Enterprise Integration Pack.</span></span> <span data-ttu-id="d9d0d-106">Для пользователей, работавших с BizTalk Server, Пакет интеграции Enterprise обеспечит аналогичные возможности по преобразованию и проверке сообщений, работе с неструктурированными файлами и даже использованию XPath для обогащения сообщений или извлечения из них свойств.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-106">For those users with a BizTalk Server background, the Enterprise Integration Pack gives you similar abilities to transform and validate messages, work with flat files, and even use XPath to enrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="d9d0d-107">Пользователи, не знакомые с этой областью, с помощью данных функций смогут расширить возможности обработки сообщений в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-107">For those users who are new to this space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="d9d0d-108">Например, если в сценарии B2B вы работаете с конкретными схемами XML, то можете использовать Пакет интеграции Enterprise для улучшения обработки этих сообщений в организации.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use the Enterprise Integration Pack to enhance how your company processes these messages.</span></span> 

<span data-ttu-id="d9d0d-109">Пакет интеграции Enterprise включает в себя следующее:</span><span class="sxs-lookup"><span data-stu-id="d9d0d-109">The Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="d9d0d-110">[Проверка XML](logic-apps-enterprise-integration-xml-validation.md "Узнайте о проверке сообщений XML") позволяет проверить входящее или исходящее сообщение XML на соответствие указанной схеме.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="d9d0d-111">[Преобразование XML](../logic-apps/logic-apps-enterprise-integration-transform.md "Узнайте о преобразованиях сообщений XML и сопоставлениях") позволяет преобразовать или настроить сообщение XML в соответствии с вашими требованиями или требованиями партнера.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or the requirements of a partner.</span></span>
* <span data-ttu-id="d9d0d-112">[Кодирование и декодирование неструктурированных файлов](logic-apps-enterprise-integration-flatfile.md "См. дополнительные сведения о кодировании и декодировании неструктурированных файлов") позволяет кодировать и декодировать неструктурированный файл.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="d9d0d-113">Например, SAP принимает и отправляет IDOC-файлы в виде неструктурированных файлов.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="d9d0d-114">Многие платформы интеграции создают сообщения XML, включая Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="d9d0d-115">Поэтому можно создать приложение логики, которое использует кодировщик неструктурированных файлов для преобразования XML-файлов в неструктурированные файлы.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-115">So, you can create a logic app that uses the flat file encoder to "convert" XML files to flat files.</span></span> 
* <span data-ttu-id="d9d0d-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) позволяет дополнить сообщение и извлечь из него определенные свойства.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from the message.</span></span> <span data-ttu-id="d9d0d-117">Эти извлеченные свойства можно затем использовать для перенаправления сообщения в целевую или промежуточную конечную точку.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-117">You can then use the extracted properties to route the message to a destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="d9d0d-118">Попробуйте сейчас</span><span class="sxs-lookup"><span data-stu-id="d9d0d-118">Try it out</span></span>
<span data-ttu-id="d9d0d-119">[Разверните полностью работоспособное приложение логики](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (пример с GitHub) с помощью функций XML в Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="d9d0d-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using the XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="d9d0d-120">Подробнее</span><span class="sxs-lookup"><span data-stu-id="d9d0d-120">Learn more</span></span>
[<span data-ttu-id="d9d0d-121">Обзор пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="d9d0d-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Обзор пакета интеграции Enterprise")
