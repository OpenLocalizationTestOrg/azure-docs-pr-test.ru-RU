---
title: "Интеграция Enterprise для B2B — Azure Logic Apps | Документация Майкрософт"
description: "Создание рабочих процессов для B2B и поддержка сценариев интеграции Enterprise для приложений логики с помощью пакета интеграции Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 9462707db03ecfcc3d5186ce7ded8655ad3bdcc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-the-enterprise-integration-pack"></a><span data-ttu-id="66d1f-103">Обзор: сценарии B2B и обмен данными с использованием пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="66d1f-103">Overview: B2B scenarios and communication with the Enterprise Integration Pack</span></span>

<span data-ttu-id="66d1f-104">Для выполнения рабочих процессов "бизнес — бизнес" (B2B) и бесперебойного взаимодействия с Azure Logic Apps можно включить сценарии интеграции с помощью облачного решения корпорации Майкрософт, пакета интеграции Enterprise.</span><span class="sxs-lookup"><span data-stu-id="66d1f-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, the Enterprise Integration Pack.</span></span> <span data-ttu-id="66d1f-105">Организации могут обмениваться электронными сообщениями, даже если они используют разные протоколы и форматы.</span><span class="sxs-lookup"><span data-stu-id="66d1f-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="66d1f-106">Пакет преобразует разные форматы в единый формат, который корпоративные системы могут распознавать и обрабатывать.</span><span class="sxs-lookup"><span data-stu-id="66d1f-106">The pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="66d1f-107">Организации могут обмениваться сообщениями с помощью стандартных протоколов, в том числе [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) и [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="66d1f-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="66d1f-108">Сообщения можно защитить с помощью шифрования и цифровой подписи.</span><span class="sxs-lookup"><span data-stu-id="66d1f-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="66d1f-109">Если вы уже работали с BizTalk Server или службами BizTalk Microsoft Azure, вам будет легко использовать функции интеграции Enterprise, так как принципы их работы похожи.</span><span class="sxs-lookup"><span data-stu-id="66d1f-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, the Enterprise Integration features are easy to use because most concepts are similar.</span></span> <span data-ttu-id="66d1f-110">Одно из основных отличий — в интеграции Enterprise используются учетные записи интеграции, которые упрощают хранение артефактов, используемых при обмене данными "бизнес-бизнес", и управление ими.</span><span class="sxs-lookup"><span data-stu-id="66d1f-110">One major difference is that Enterprise Integration uses integration accounts to simplify the storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="66d1f-111">В контексте архитектуры пакет интеграции Enterprise основывается на интеграции учетных записей.</span><span class="sxs-lookup"><span data-stu-id="66d1f-111">Architecturally, the Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="66d1f-112">Эти учетные записи являются облачными контейнерами, которые хранят все ваши артефакты, такие как схемы, партнеры, сертификаты, карты и соглашения.</span><span class="sxs-lookup"><span data-stu-id="66d1f-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="66d1f-113">Эти артефакты можно использовать для проектирования, развертывания и обслуживания приложений B2B, а также создания рабочих процессов B2B для приложений логики.</span><span class="sxs-lookup"><span data-stu-id="66d1f-113">You can use these artifacts to design, deploy, and maintain your B2B apps and also to build B2B workflows for logic apps.</span></span> <span data-ttu-id="66d1f-114">Прежде чем использовать артефакты, необходимо связать свою учетную запись интеграции с приложением логики.</span><span class="sxs-lookup"><span data-stu-id="66d1f-114">But before you can use these artifacts, you must first link your integration account to your logic app.</span></span> <span data-ttu-id="66d1f-115">После этого приложение логики будет иметь доступ к артефактам учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="66d1f-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="66d1f-116">Для чего следует использовать интеграцию Enterprise?</span><span class="sxs-lookup"><span data-stu-id="66d1f-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="66d1f-117">Благодаря интеграции Enterprise можно хранить все артефакты в одном расположении — в своей учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="66d1f-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="66d1f-118">Вы можете создавать рабочие процессы B2B и реализовать интеграцию с приложениями SaaS сторонних поставщиков, локальными приложениями или пользовательскими приложениями, используя ядро Azure Logic Apps и все его соединители.</span><span class="sxs-lookup"><span data-stu-id="66d1f-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using the Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="66d1f-119">Вы можете создать пользовательский код для приложения логики с помощью функций Azure.</span><span class="sxs-lookup"><span data-stu-id="66d1f-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-to-get-started-with-enterprise-integration"></a><span data-ttu-id="66d1f-120">Как приступить к работе с интеграцией Enterprise?</span><span class="sxs-lookup"><span data-stu-id="66d1f-120">How to get started with enterprise integration?</span></span>

<span data-ttu-id="66d1f-121">Создавать приложения B2B и управлять ими с помощью пакета интеграции Enterprise можно в конструкторе приложений логики на **портале Azure**.</span><span class="sxs-lookup"><span data-stu-id="66d1f-121">You can build and manage B2B apps with the Enterprise Integration Pack through the Logic App Designer in the **Azure portal**.</span></span> <span data-ttu-id="66d1f-122">Вы также можете управлять приложениями логики с помощью [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Разделы о PowerShell, посвященные приложениям логики").</span><span class="sxs-lookup"><span data-stu-id="66d1f-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="66d1f-123">Ниже описаны действия, которые необходимо выполнить перед созданием приложений на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="66d1f-123">Here are the high-level steps you must take before you can create apps in the Azure portal:</span></span>

![Изображение для обзора](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="66d1f-125">Каковы наиболее распространенные сценарии применения?</span><span class="sxs-lookup"><span data-stu-id="66d1f-125">What are some common scenarios?</span></span>

<span data-ttu-id="66d1f-126">Интеграция Enterprise поддерживает следующие отраслевые стандарты:</span><span class="sxs-lookup"><span data-stu-id="66d1f-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="66d1f-127">EDI — электронный обмен данными;</span><span class="sxs-lookup"><span data-stu-id="66d1f-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="66d1f-128">EAI — интеграция приложений.</span><span class="sxs-lookup"><span data-stu-id="66d1f-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-to-get-started"></a><span data-ttu-id="66d1f-129">Вот что необходимо для немедленного начала работы.</span><span class="sxs-lookup"><span data-stu-id="66d1f-129">Here's what you need to get started</span></span>

* <span data-ttu-id="66d1f-130">Подписка Azure с учетной записью интеграции.</span><span class="sxs-lookup"><span data-stu-id="66d1f-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="66d1f-131">Visual Studio 2015 для создания карт и схем.</span><span class="sxs-lookup"><span data-stu-id="66d1f-131">Visual Studio 2015 to create maps and schemas</span></span>
* [<span data-ttu-id="66d1f-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0.</span><span class="sxs-lookup"><span data-stu-id="66d1f-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="66d1f-133">Попробуйте сейчас</span><span class="sxs-lookup"><span data-stu-id="66d1f-133">Try it now</span></span>

<span data-ttu-id="66d1f-134">[Разверните полностью работоспособный пример приложения логики для обмена данными AS2](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive), который использует функции B2B Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="66d1f-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses the B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="66d1f-135">Подробнее</span><span class="sxs-lookup"><span data-stu-id="66d1f-135">Learn more</span></span>
* [<span data-ttu-id="66d1f-136">Соглашения</span><span class="sxs-lookup"><span data-stu-id="66d1f-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Узнайте о соглашениях интеграции Enterprise")
* [<span data-ttu-id="66d1f-137">Сценарии "бизнес — бизнес"</span><span class="sxs-lookup"><span data-stu-id="66d1f-137">Business to Business (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "Узнайте, как создавать приложения логики с возможностями "бизнес — бизнес"")  
* [<span data-ttu-id="66d1f-138">Сертификаты</span><span class="sxs-lookup"><span data-stu-id="66d1f-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "Узнайте о сертификатах интеграции Enterprise")
* [<span data-ttu-id="66d1f-139">Кодирование и декодирование неструктурированных файлов</span><span class="sxs-lookup"><span data-stu-id="66d1f-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "Узнайте, как кодировать и декодировать содержимое неструктурированных файлов")  
* [<span data-ttu-id="66d1f-140">Учетные записи интеграции</span><span class="sxs-lookup"><span data-stu-id="66d1f-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "Узнайте больше об учетных записях интеграции")
* [<span data-ttu-id="66d1f-141">Карты</span><span class="sxs-lookup"><span data-stu-id="66d1f-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Узнайте о картах интеграции Enterprise")
* [<span data-ttu-id="66d1f-142">Партнеры</span><span class="sxs-lookup"><span data-stu-id="66d1f-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "Узнайте о партнерах интеграции Enterprise")
* [<span data-ttu-id="66d1f-143">Схемы</span><span class="sxs-lookup"><span data-stu-id="66d1f-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "Узнайте о схемах интеграции Enterprise")
* [<span data-ttu-id="66d1f-144">Проверка сообщений XML</span><span class="sxs-lookup"><span data-stu-id="66d1f-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "Узнайте, как проверять сообщения XML с помощью приложений логики")
* [<span data-ttu-id="66d1f-145">Преобразование XML-файла</span><span class="sxs-lookup"><span data-stu-id="66d1f-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "Узнайте о картах интеграции Enterprise")
* [<span data-ttu-id="66d1f-146">Корпоративные соединители интеграции</span><span class="sxs-lookup"><span data-stu-id="66d1f-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "Узнайте о соединителях пакета интеграции Enterprise.")
* [<span data-ttu-id="66d1f-147">Метаданные учетной записи интеграции</span><span class="sxs-lookup"><span data-stu-id="66d1f-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "Узнайте о метаданных учетной записи интеграции")
* [<span data-ttu-id="66d1f-148">Мониторинг сообщений "бизнес — бизнес"</span><span class="sxs-lookup"><span data-stu-id="66d1f-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "Узнайте больше о мониторинге сообщений "бизнес — бизнес"")
* [<span data-ttu-id="66d1f-149">Отслеживание сообщений "бизнес — бизнес" на портале OMS</span><span class="sxs-lookup"><span data-stu-id="66d1f-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "Узнайте больше об отслеживании сообщений "бизнес — бизнес" на портале OMS")

