---
title: "aaaEnterprise интеграции для B2B - приложения логики Azure | Документы Microsoft"
description: "Создавать рабочие процессы B2B и поддержки корпоративных сценариев интеграции для логики приложений с помощью hello пакет интеграции Enterprise"
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
ms.openlocfilehash: 8dc866533110b1d07f51cf446056d2ca5ce869ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a><span data-ttu-id="802c4-103">Обзор: Сценарии B2B и обмена данными с hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="802c4-103">Overview: B2B scenarios and communication with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="802c4-104">Для рабочих процессов в бизнес бизнес (B2B) и беспроблемную связь с приложениями логики Azure можно включить корпоративных сценариях интеграции с корпорации Майкрософт Облачное решение, hello пакет интеграции Enterprise.</span><span class="sxs-lookup"><span data-stu-id="802c4-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, hello Enterprise Integration Pack.</span></span> <span data-ttu-id="802c4-105">Организации могут обмениваться электронными сообщениями, даже если они используют разные протоколы и форматы.</span><span class="sxs-lookup"><span data-stu-id="802c4-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="802c4-106">пакет Hello преобразует различных форматах в формат, который систем организации могут распознавать и обрабатывать.</span><span class="sxs-lookup"><span data-stu-id="802c4-106">hello pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="802c4-107">Организации могут обмениваться сообщениями с помощью стандартных протоколов, в том числе [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) и [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="802c4-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="802c4-108">Сообщения можно защитить с помощью шифрования и цифровой подписи.</span><span class="sxs-lookup"><span data-stu-id="802c4-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="802c4-109">Если вы знакомы с BizTalk Server или служб BizTalk Microsoft Azure, компоненты интеграции предприятия hello, легко toouse, потому что большинство понятия похожи.</span><span class="sxs-lookup"><span data-stu-id="802c4-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, hello Enterprise Integration features are easy toouse because most concepts are similar.</span></span> <span data-ttu-id="802c4-110">Одно из основных отличий заключается в том, что интеграцию используется интеграции учетных записей toosimplify hello хранения и управления артефакты, используемые во взаимодействии B2B.</span><span class="sxs-lookup"><span data-stu-id="802c4-110">One major difference is that Enterprise Integration uses integration accounts toosimplify hello storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="802c4-111">С точки зрения архитектуры hello пакет интеграции Enterprise основывается на «интеграция учетных записей».</span><span class="sxs-lookup"><span data-stu-id="802c4-111">Architecturally, hello Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="802c4-112">Эти учетные записи являются облачными контейнерами, которые хранят все ваши артефакты, такие как схемы, партнеры, сертификаты, карты и соглашения.</span><span class="sxs-lookup"><span data-stu-id="802c4-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="802c4-113">Использовать эти артефакты toodesign, развертывать и поддерживать B2B приложениях и также toobuild B2B рабочих процессов для логики приложений.</span><span class="sxs-lookup"><span data-stu-id="802c4-113">You can use these artifacts toodesign, deploy, and maintain your B2B apps and also toobuild B2B workflows for logic apps.</span></span> <span data-ttu-id="802c4-114">Но прежде чем использовать эти артефакты, необходимо сначала связать логику приложения tooyour вашей учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="802c4-114">But before you can use these artifacts, you must first link your integration account tooyour logic app.</span></span> <span data-ttu-id="802c4-115">После этого приложение логики будет иметь доступ к артефактам учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="802c4-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="802c4-116">Для чего следует использовать интеграцию Enterprise?</span><span class="sxs-lookup"><span data-stu-id="802c4-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="802c4-117">Благодаря интеграции Enterprise можно хранить все артефакты в одном расположении — в своей учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="802c4-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="802c4-118">Можно создавать рабочие процессы B2B и интегрировать сторонние приложения для браузера программное обеспечение как услуга (SaaS), локальные приложения и пользовательские приложения с помощью подсистемы приложения логики Azure hello и все соединители.</span><span class="sxs-lookup"><span data-stu-id="802c4-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using hello Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="802c4-119">Вы можете создать пользовательский код для приложения логики с помощью функций Azure.</span><span class="sxs-lookup"><span data-stu-id="802c4-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-tooget-started-with-enterprise-integration"></a><span data-ttu-id="802c4-120">Как tooget работу с интеграции предприятия?</span><span class="sxs-lookup"><span data-stu-id="802c4-120">How tooget started with enterprise integration?</span></span>

<span data-ttu-id="802c4-121">Создавать и управлять приложениями B2B с hello пакет интеграции Enterprise через hello конструктор логику приложения в hello **портал Azure**.</span><span class="sxs-lookup"><span data-stu-id="802c4-121">You can build and manage B2B apps with hello Enterprise Integration Pack through hello Logic App Designer in hello **Azure portal**.</span></span> <span data-ttu-id="802c4-122">Вы также можете управлять приложениями логики с помощью [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Разделы о PowerShell, посвященные приложениям логики").</span><span class="sxs-lookup"><span data-stu-id="802c4-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="802c4-123">Ниже приведены hello высокоуровневые действия, которые необходимо выполнить перед созданием приложения hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="802c4-123">Here are hello high-level steps you must take before you can create apps in hello Azure portal:</span></span>

![Изображение для обзора](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="802c4-125">Каковы наиболее распространенные сценарии применения?</span><span class="sxs-lookup"><span data-stu-id="802c4-125">What are some common scenarios?</span></span>

<span data-ttu-id="802c4-126">Интеграция Enterprise поддерживает следующие отраслевые стандарты:</span><span class="sxs-lookup"><span data-stu-id="802c4-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="802c4-127">EDI — электронный обмен данными;</span><span class="sxs-lookup"><span data-stu-id="802c4-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="802c4-128">EAI — интеграция приложений.</span><span class="sxs-lookup"><span data-stu-id="802c4-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-tooget-started"></a><span data-ttu-id="802c4-129">Вот что нужно tooget работы</span><span class="sxs-lookup"><span data-stu-id="802c4-129">Here's what you need tooget started</span></span>

* <span data-ttu-id="802c4-130">Подписка Azure с учетной записью интеграции.</span><span class="sxs-lookup"><span data-stu-id="802c4-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="802c4-131">Visual Studio 2015 toocreate карты и схемы</span><span class="sxs-lookup"><span data-stu-id="802c4-131">Visual Studio 2015 toocreate maps and schemas</span></span>
* [<span data-ttu-id="802c4-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0.</span><span class="sxs-lookup"><span data-stu-id="802c4-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="802c4-133">Попробуйте сейчас</span><span class="sxs-lookup"><span data-stu-id="802c4-133">Try it now</span></span>

<span data-ttu-id="802c4-134">[Развертывание образца полностью AS2 send и получать приложение логики](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) , использующий функции hello B2B для логики приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="802c4-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses hello B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="802c4-135">Подробнее</span><span class="sxs-lookup"><span data-stu-id="802c4-135">Learn more</span></span>
* [<span data-ttu-id="802c4-136">Соглашения</span><span class="sxs-lookup"><span data-stu-id="802c4-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Узнайте о соглашениях интеграции Enterprise")
* [<span data-ttu-id="802c4-137">Бизнес-сценарии (B2B) tooBusiness</span><span class="sxs-lookup"><span data-stu-id="802c4-137">Business tooBusiness (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "сведения как toocreate логики приложения с функциями B2B")  
* [<span data-ttu-id="802c4-138">Сертификаты</span><span class="sxs-lookup"><span data-stu-id="802c4-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "Узнайте о сертификатах интеграции Enterprise")
* [<span data-ttu-id="802c4-139">Плоский файл кодирование и декодирование</span><span class="sxs-lookup"><span data-stu-id="802c4-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "сведения как tooencode и декодирование неструктурированного файла содержимого")  
* [<span data-ttu-id="802c4-140">Учетные записи интеграции</span><span class="sxs-lookup"><span data-stu-id="802c4-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "Узнайте больше об учетных записях интеграции")
* [<span data-ttu-id="802c4-141">Карты</span><span class="sxs-lookup"><span data-stu-id="802c4-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Узнайте о картах интеграции Enterprise")
* [<span data-ttu-id="802c4-142">Партнеры</span><span class="sxs-lookup"><span data-stu-id="802c4-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "Узнайте о партнерах интеграции Enterprise")
* [<span data-ttu-id="802c4-143">Схемы</span><span class="sxs-lookup"><span data-stu-id="802c4-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "Узнайте о схемах интеграции Enterprise")
* [<span data-ttu-id="802c4-144">Проверка XML-сообщение</span><span class="sxs-lookup"><span data-stu-id="802c4-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "узнать, как toovalidate XML сообщения с приложениями логики")
* [<span data-ttu-id="802c4-145">Преобразование XML-файла</span><span class="sxs-lookup"><span data-stu-id="802c4-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "Узнайте о картах интеграции Enterprise")
* [<span data-ttu-id="802c4-146">Корпоративные соединители интеграции</span><span class="sxs-lookup"><span data-stu-id="802c4-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "Узнайте о соединителях пакета интеграции Enterprise.")
* [<span data-ttu-id="802c4-147">Метаданные учетной записи интеграции</span><span class="sxs-lookup"><span data-stu-id="802c4-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "Узнайте о метаданных учетной записи интеграции")
* [<span data-ttu-id="802c4-148">Мониторинг сообщений "бизнес — бизнес"</span><span class="sxs-lookup"><span data-stu-id="802c4-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "Узнайте больше о мониторинге сообщений "бизнес — бизнес"")
* [<span data-ttu-id="802c4-149">Отслеживание сообщений "бизнес — бизнес" на портале OMS</span><span class="sxs-lookup"><span data-stu-id="802c4-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "Узнайте больше об отслеживании сообщений "бизнес — бизнес" на портале OMS")

