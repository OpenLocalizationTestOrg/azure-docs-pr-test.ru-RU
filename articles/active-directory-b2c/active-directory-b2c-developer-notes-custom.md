---
title: "Azure Active Directory B2C. Примечания по использованию настраиваемых политик для разработчиков | Документация Майкрософт"
description: "Примечания для разработчиков по настройке и обслуживанию Azure AD B2C с помощью настраиваемых политик"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="ef778-103">Заметки о выпуске общедоступной предварительной версии настраиваемой политики Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="ef778-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="ef778-104">Hello набор функций для настраиваемой политики теперь доступен для оценки в общедоступной предварительной версии для всех Azure Active Directory B2C клиентов (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="ef778-104">hello custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="ef778-105">Этот набор компонентов ориентирована на дополнительные удостоверения разработчиков, создающих самые сложные решения по управлению удостоверениями hello.</span><span class="sxs-lookup"><span data-stu-id="ef778-105">This feature set is targeted at advanced identity developers building hello most complex identity solutions.</span></span>  

<span data-ttu-id="ef778-106">В настоящее время этот набор компонентов требует hello tooconfigure разработчикам возможности платформы идентификации непосредственно через редактирования XML-файла.</span><span class="sxs-lookup"><span data-stu-id="ef778-106">Today, this feature set requires developers tooconfigure hello Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="ef778-107">Этот метод конфигурации очень эффективный и сложный.</span><span class="sxs-lookup"><span data-stu-id="ef778-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="ef778-108">Дополнительные удостоверения разработчики, использующие hello Identity Framework качества следует запланировать tooinvest некоторое время прохождения руководства пользователя и чтение справочные документы.</span><span class="sxs-lookup"><span data-stu-id="ef778-108">Advanced identity developers using hello Identity Experience Framework should plan tooinvest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="ef778-109">Возможности общедоступной предварительной версии</span><span class="sxs-lookup"><span data-stu-id="ef778-109">Features included in this public preview</span></span>
<span data-ttu-id="ef778-110">Hello новых возможностей, представленных в общедоступной предварительной версии hello разработчики позволяют выполнять следующие задачи hello.</span><span class="sxs-lookup"><span data-stu-id="ef778-110">With hello new features introduced in hello public preview, developers can perform hello following tasks:</span></span><br>

* <span data-ttu-id="ef778-111">Создавать и отправлять пользовательские процедуры проверки подлинности с помощью настраиваемых политик.</span><span class="sxs-lookup"><span data-stu-id="ef778-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="ef778-112">Поэтапно описывать пути взаимодействия пользователя для обмена данными между поставщиками удостоверений.</span><span class="sxs-lookup"><span data-stu-id="ef778-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="ef778-113">Определять условные ветвления путей взаимодействия пользователей.</span><span class="sxs-lookup"><span data-stu-id="ef778-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="ef778-114">Интегрировать службы с поддержкой REST API в пользовательские процедуры проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ef778-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="ef778-115">Добавьте федерации с поставщиками удостоверений, совместимые с hello OpenIDConnect standard.</span><span class="sxs-lookup"><span data-stu-id="ef778-115">Add federation with identity providers that are compliant with hello OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="ef778-116">Добавьте федерации с поставщиками удостоверений, которые соответствуют протокола toohello SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="ef778-116">Add federation with identity providers that adhere toohello SAML 2.0 protocol.</span></span> 

## <a name="terms-of-hello-public-preview"></a><span data-ttu-id="ef778-117">Условия hello общедоступной предварительной версии</span><span class="sxs-lookup"><span data-stu-id="ef778-117">Terms of hello public preview</span></span>

* <span data-ttu-id="ef778-118">Мы рекомендуем вам toouse hello новые возможности только для ознакомительных целей.</span><span class="sxs-lookup"><span data-stu-id="ef778-118">We encourage you toouse hello new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="ef778-119">Новые функции не предназначены для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ef778-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="ef778-120">Новые возможности toohello не применяются соглашения об уровне обслуживания (SLA).</span><span class="sxs-lookup"><span data-stu-id="ef778-120">Service level agreements (SLAs) do not apply toohello new features.</span></span> <br>
* <span data-ttu-id="ef778-121">Запросы в службу поддержки можно отправить по обычным каналам поддержки.</span><span class="sxs-lookup"><span data-stu-id="ef778-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="ef778-122">Точная дата выхода общедоступной версии не установлена.</span><span class="sxs-lookup"><span data-stu-id="ef778-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="ef778-123">Нашему усмотрению и для какой-либо причине Майкрософт можно флаг и отклонить или запретить сценарии и пути пользователя, превышающие hello области tooserve сертификаты hello Azure AD B2C продукта как платформы (САЙЭМ) управления удостоверениями и доступом клиента.</span><span class="sxs-lookup"><span data-stu-id="ef778-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed hello scope of hello Azure AD B2C product charter tooserve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="ef778-124">Обязанности разработчиков набора функций настраиваемой политики</span><span class="sxs-lookup"><span data-stu-id="ef778-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="ef778-125">Конфигурация политики вручную предоставляет toohello более низкого уровня доступа к базовой платформе Azure AD B2C и приводит к созданию hello платформы уникальный, полностью настраиваемый доверия.</span><span class="sxs-lookup"><span data-stu-id="ef778-125">Manual policy configuration grants lower-level access toohello underlying platform of Azure AD B2C and results in hello creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="ef778-126">Возможных перестановок поставщики пользовательских удостоверений, доверительные отношения интеграции с внешних служб и рабочих процессов пошаговые помещать больше требования в hello advanced разработчиков, использующих их.</span><span class="sxs-lookup"><span data-stu-id="ef778-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on hello advanced developers consuming them.</span></span>

<span data-ttu-id="ef778-127">Преимущество toofully из общедоступной предварительной версии hello, рекомендуется придерживаться, разработчиков, использующих набор функций hello настраиваемой политики toohello следовать рекомендациям:</span><span class="sxs-lookup"><span data-stu-id="ef778-127">toofully benefit from hello public preview, we suggest that developers consuming hello custom policy feature set adhere toohello following guidelines:</span></span>
* <span data-ttu-id="ef778-128">Ознакомиться с язык конфигурации hello hello Engine взаимодействие удостоверений и управления ключ/секретные данные.</span><span class="sxs-lookup"><span data-stu-id="ef778-128">Become familiar with hello configuration language of hello Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="ef778-129">Станьте владельцем сценариев и настраиваемой интеграции.</span><span class="sxs-lookup"><span data-stu-id="ef778-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="ef778-130">Выполняйте систематическое тестирование сценария.</span><span class="sxs-lookup"><span data-stu-id="ef778-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="ef778-131">Выполните рекомендации по разработке программного обеспечения и промежуточному хранению, используя как минимум одну среду разработки или тестирования и одну рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="ef778-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="ef778-132">Быть в курсе новых проектах от поставщиков удостоверений hello и служб, которым предполагается интеграция.</span><span class="sxs-lookup"><span data-stu-id="ef778-132">Stay informed about new developments from hello identity providers and services you integrate with.</span></span> <span data-ttu-id="ef778-133">Например отслеживания изменений, связанных в секреты и изменения запланированных и незапланированных toohello службы.</span><span class="sxs-lookup"><span data-stu-id="ef778-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes toohello service.</span></span>
* <span data-ttu-id="ef778-134">Настройка мониторинга и отслеживать скорость реагирования hello рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="ef778-134">Set up active monitoring, and monitor hello responsiveness of production environments.</span></span>
* <span data-ttu-id="ef778-135">Регулярное обновление контактные адреса электронной почты, как и сообщения электронной почты узел live команды Microsoft toohello отвечать на запросы.</span><span class="sxs-lookup"><span data-stu-id="ef778-135">Keep contact email addresses current, and stay responsive toohello Microsoft live-site team emails.</span></span>
* <span data-ttu-id="ef778-136">Предпринять своевременно действия, когда желательно toodo поэтому hello Microsoft live сайта team.</span><span class="sxs-lookup"><span data-stu-id="ef778-136">Take timely action when advised toodo so by hello Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="ef778-137">Эти функции могут быть включены в конечном счете в Azure AD встроенных политик, становятся более доступными tooall разработчиков.</span><span class="sxs-lookup"><span data-stu-id="ef778-137">These features might eventually be included in Azure AD built-in policies, making them more accessible tooall developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef778-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ef778-138">Next steps</span></span>
<span data-ttu-id="ef778-139">[Azure Active Directory B2C. Приступая к работе с настраиваемыми политиками](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ef778-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>
