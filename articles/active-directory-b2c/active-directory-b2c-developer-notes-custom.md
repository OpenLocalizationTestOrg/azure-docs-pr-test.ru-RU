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
ms.openlocfilehash: a5f222e5b11e05286152a9f1cc55d2c3fc27a9dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a><span data-ttu-id="aaa01-103">Заметки о выпуске общедоступной предварительной версии настраиваемой политики Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="aaa01-103">Release notes for Azure Active Directory B2C custom policy public preview</span></span>
<span data-ttu-id="aaa01-104">Набор функций настраиваемой политики теперь доступен для оценки в общедоступной предварительной версии для всех клиентов Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="aaa01-104">The custom policy feature set is now available for evaluation under public preview for all Azure Active Directory B2C (Azure AD B2C) customers.</span></span> <span data-ttu-id="aaa01-105">Этот набор функций предназначен для опытных разработчиков удостоверений, создающих самые сложные решения удостоверений.</span><span class="sxs-lookup"><span data-stu-id="aaa01-105">This feature set is targeted at advanced identity developers building the most complex identity solutions.</span></span>  

<span data-ttu-id="aaa01-106">На сегодняшний день, чтобы использовать этот набор функций, разработчикам требуется настроить инфраструктуру процедур идентификации напрямую, внеся изменения в XML-файл.</span><span class="sxs-lookup"><span data-stu-id="aaa01-106">Today, this feature set requires developers to configure the Identity Experience Framework directly via XML file editing.</span></span> <span data-ttu-id="aaa01-107">Этот метод конфигурации очень эффективный и сложный.</span><span class="sxs-lookup"><span data-stu-id="aaa01-107">This method of configuration is powerful and complex.</span></span> <span data-ttu-id="aaa01-108">Опытным разработчикам удостоверений, использующим инфраструктуру процедур идентификации, необходимо ознакомиться с комплексными пошаговыми руководствами и справочными материалами.</span><span class="sxs-lookup"><span data-stu-id="aaa01-108">Advanced identity developers using the Identity Experience Framework should plan to invest some time completing walk-throughs and reading reference documents.</span></span> 

## <a name="features-included-in-this-public-preview"></a><span data-ttu-id="aaa01-109">Возможности общедоступной предварительной версии</span><span class="sxs-lookup"><span data-stu-id="aaa01-109">Features included in this public preview</span></span>
<span data-ttu-id="aaa01-110">Новые функции, предоставленные в общедоступной предварительной версии, позволяют разработчикам выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="aaa01-110">With the new features introduced in the public preview, developers can perform the following tasks:</span></span><br>

* <span data-ttu-id="aaa01-111">Создавать и отправлять пользовательские процедуры проверки подлинности с помощью настраиваемых политик.</span><span class="sxs-lookup"><span data-stu-id="aaa01-111">Author and upload custom authentication user journeys by using custom policies.</span></span> 
   * <span data-ttu-id="aaa01-112">Поэтапно описывать пути взаимодействия пользователя для обмена данными между поставщиками удостоверений.</span><span class="sxs-lookup"><span data-stu-id="aaa01-112">Describe user journeys step-by-step as exchanges between claims providers.</span></span> 
   * <span data-ttu-id="aaa01-113">Определять условные ветвления путей взаимодействия пользователей.</span><span class="sxs-lookup"><span data-stu-id="aaa01-113">Define conditional branching in user journeys.</span></span> 
* <span data-ttu-id="aaa01-114">Интегрировать службы с поддержкой REST API в пользовательские процедуры проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="aaa01-114">Integrate REST API-enabled services in your custom authentication user journeys.</span></span>  
* <span data-ttu-id="aaa01-115">Добавлять федерацию с помощью поставщиков удостоверений, соответствующих стандарту OpenIDConnect.</span><span class="sxs-lookup"><span data-stu-id="aaa01-115">Add federation with identity providers that are compliant with the OpenIDConnect standard.</span></span> <br>
* <span data-ttu-id="aaa01-116">Добавлять федерацию с помощью поставщиков удостоверений в соответствии с протоколом SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="aaa01-116">Add federation with identity providers that adhere to the SAML 2.0 protocol.</span></span> 

## <a name="terms-of-the-public-preview"></a><span data-ttu-id="aaa01-117">Условия использования общедоступной предварительной версии</span><span class="sxs-lookup"><span data-stu-id="aaa01-117">Terms of the public preview</span></span>

* <span data-ttu-id="aaa01-118">Мы рекомендуем использовать новые функции только для ознакомления.</span><span class="sxs-lookup"><span data-stu-id="aaa01-118">We encourage you to use the new features for evaluation purposes only.</span></span><br>
* <span data-ttu-id="aaa01-119">Новые функции не предназначены для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="aaa01-119">The new features are not intended for use in a production environment.</span></span><br>
* <span data-ttu-id="aaa01-120">К новым функциям не применяются соглашения об уровнях обслуживания.</span><span class="sxs-lookup"><span data-stu-id="aaa01-120">Service level agreements (SLAs) do not apply to the new features.</span></span> <br>
* <span data-ttu-id="aaa01-121">Запросы в службу поддержки можно отправить по обычным каналам поддержки.</span><span class="sxs-lookup"><span data-stu-id="aaa01-121">Support requests can be filed through regular support channels.</span></span> <br>
* <span data-ttu-id="aaa01-122">Точная дата выхода общедоступной версии не установлена.</span><span class="sxs-lookup"><span data-stu-id="aaa01-122">There is no promised date for general availability.</span></span><br>
* <span data-ttu-id="aaa01-123">В случае необходимости или по любой другой причине корпорация Майкрософт может помечать, отклонять или ограничивать сценарии и пути взаимодействия пользователя, выходящие за рамки разрешений продукта Azure AD B2C, который будет использоваться в качестве платформы управления удостоверениями и доступом клиентов.</span><span class="sxs-lookup"><span data-stu-id="aaa01-123">At our discretion, and for any reason, Microsoft can flag and reject or restrict scenarios and user journeys that exceed the scope of the Azure AD B2C product charter to serve as a customer identity and access management (CIAM) platform.</span></span>

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a><span data-ttu-id="aaa01-124">Обязанности разработчиков набора функций настраиваемой политики</span><span class="sxs-lookup"><span data-stu-id="aaa01-124">Responsibilities of custom policy feature-set developers</span></span>
<span data-ttu-id="aaa01-125">Ручная настройка политики предоставляет низкоуровневый доступ к базовой платформе Azure AD B2C и приводит к созданию уникальной, полностью настраиваемой инфраструктуры доверия.</span><span class="sxs-lookup"><span data-stu-id="aaa01-125">Manual policy configuration grants lower-level access to the underlying platform of Azure AD B2C and results in the creation of a unique, fully customizable trust framework.</span></span> <span data-ttu-id="aaa01-126">Возможность перестановки поставщиков пользовательских удостоверений, отношения доверия, интеграция с внешними службами и поэтапные рабочие процессы усложняют задачи для опытных разработчиков, которые их используют.</span><span class="sxs-lookup"><span data-stu-id="aaa01-126">The possible permutations of custom identity providers, trust relationships, integrations with external services, and step-by-step workflows place greater demands on the advanced developers consuming them.</span></span>

<span data-ttu-id="aaa01-127">Чтобы наиболее эффективно использовать общедоступную предварительную версию, мы рекомендуем разработчикам пользоваться набором функций настраиваемой политики в соответствии со следующими рекомендациями:</span><span class="sxs-lookup"><span data-stu-id="aaa01-127">To fully benefit from the public preview, we suggest that developers consuming the custom policy feature set adhere to the following guidelines:</span></span>
* <span data-ttu-id="aaa01-128">Ознакомьтесь с языком конфигурации подсистемы идентификации и сведениями об управлении ключами и секретами.</span><span class="sxs-lookup"><span data-stu-id="aaa01-128">Become familiar with the configuration language of the Identity Experience Engine and key/secrets management.</span></span>
* <span data-ttu-id="aaa01-129">Станьте владельцем сценариев и настраиваемой интеграции.</span><span class="sxs-lookup"><span data-stu-id="aaa01-129">Take ownership of scenarios and custom integrations.</span></span>
* <span data-ttu-id="aaa01-130">Выполняйте систематическое тестирование сценария.</span><span class="sxs-lookup"><span data-stu-id="aaa01-130">Perform methodical scenario testing.</span></span>
* <span data-ttu-id="aaa01-131">Выполните рекомендации по разработке программного обеспечения и промежуточному хранению, используя как минимум одну среду разработки или тестирования и одну рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="aaa01-131">Follow software development and staging best practices with a minimum of one development and testing environment and one production environment.</span></span>
* <span data-ttu-id="aaa01-132">Будьте в курсе последних разработок поставщика удостоверений и интегрируемых служб.</span><span class="sxs-lookup"><span data-stu-id="aaa01-132">Stay informed about new developments from the identity providers and services you integrate with.</span></span> <span data-ttu-id="aaa01-133">Например, получайте информацию об изменениях в секретах, запланированных и незапланированных изменениях в службах и т. д.</span><span class="sxs-lookup"><span data-stu-id="aaa01-133">For example, keep track of changes in secrets and of scheduled and unscheduled changes to the service.</span></span>
* <span data-ttu-id="aaa01-134">Настройте активный мониторинг и отслеживайте скорость реагирования рабочих сред.</span><span class="sxs-lookup"><span data-stu-id="aaa01-134">Set up active monitoring, and monitor the responsiveness of production environments.</span></span>
* <span data-ttu-id="aaa01-135">Используйте текущий контактный адрес электронной почты, чтобы реагировать на сообщения службы поддержки активного сайта Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="aaa01-135">Keep contact email addresses current, and stay responsive to the Microsoft live-site team emails.</span></span>
* <span data-ttu-id="aaa01-136">Принимайте своевременные меры, рекомендованные службой поддержки активного сайта Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="aaa01-136">Take timely action when advised to do so by the Microsoft live-site team.</span></span> 


>[!NOTE]
><span data-ttu-id="aaa01-137">Со временем эти функции могут быть включены во встроенные политики Azure AD, что делает их более доступными для всех разработчиков.</span><span class="sxs-lookup"><span data-stu-id="aaa01-137">These features might eventually be included in Azure AD built-in policies, making them more accessible to all developers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaa01-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aaa01-138">Next steps</span></span>
<span data-ttu-id="aaa01-139">[Azure Active Directory B2C. Приступая к работе с настраиваемыми политиками](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="aaa01-139">[Get started with custom policies](active-directory-b2c-get-started-custom.md).</span></span>
