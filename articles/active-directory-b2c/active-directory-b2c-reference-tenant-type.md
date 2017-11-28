---
title: "Azure Active Directory B2C: доступность в регионах и местонахождение данных | Документы Майкрософт"
description: "Раздел о типах hello клиентов Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="ec318-103">Azure Active Directory B2C: доступность в регионах и местонахождение данных</span><span class="sxs-lookup"><span data-stu-id="ec318-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="ec318-104">Область доступности и объемом данных являются двух очень понятий, применимые по-разному tooAzure AD B2C остальных hello Azure.</span><span class="sxs-lookup"><span data-stu-id="ec318-104">Region availability and data residency are two very different concepts that apply differently tooAzure AD B2C from hello rest of Azure.</span></span> <span data-ttu-id="ec318-105">В этой статье будет объясните hello различия этих двух основных понятиях и сравнить их воздействия на tooAzure и Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ec318-105">This article will explain hello differences between these two concepts and compare how they apply tooAzure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="ec318-106">Сводка</span><span class="sxs-lookup"><span data-stu-id="ec318-106">Summary</span></span>
<span data-ttu-id="ec318-107">Azure AD B2C — **общедоступной по всему миру** с помощью параметра hello **объемом данных в США и Европе**.</span><span class="sxs-lookup"><span data-stu-id="ec318-107">Azure AD B2C is **generally available worldwide** with hello option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="ec318-108">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="ec318-108">Concepts</span></span>
* <span data-ttu-id="ec318-109">**Область доступности** ссылается toowhere доступен для использования.</span><span class="sxs-lookup"><span data-stu-id="ec318-109">**Region availability** refers toowhere a service is available for use.</span></span>
* <span data-ttu-id="ec318-110">**Размещение данных** ссылается toowhere пользователя хранятся данные.</span><span class="sxs-lookup"><span data-stu-id="ec318-110">**Data residency** refers toowhere user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="ec318-111">Регионы доступности</span><span class="sxs-lookup"><span data-stu-id="ec318-111">Region availability</span></span>
<span data-ttu-id="ec318-112">Azure AD B2C доступна по всему миру через hello общедоступное облако Azure.</span><span class="sxs-lookup"><span data-stu-id="ec318-112">Azure AD B2C is available worldwide via hello Azure public cloud.</span></span> 

<span data-ttu-id="ec318-113">Это отличается от модели hello выполните большинства других служб Azure, которая привязать доступности с объемом данных.</span><span class="sxs-lookup"><span data-stu-id="ec318-113">This differs from hello model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="ec318-114">Вы увидите примеры, приведенные в обоих Azure [продукты доступны по областям](https://azure.microsoft.com/regions/services/) страницы и hello [Active Directory B2C калькулятор](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="ec318-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and hello [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="ec318-115">Местонахождение данных</span><span class="sxs-lookup"><span data-stu-id="ec318-115">Data residency</span></span>
<span data-ttu-id="ec318-116">Служба Azure AD B2C сохраняет данные пользователей в США или Европе.</span><span class="sxs-lookup"><span data-stu-id="ec318-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="ec318-117">Местонахождение данных зависит от страны или региона, выбранных при [создании клиента Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ec318-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Снимок экрана: предварительная версия клиента](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="ec318-119">Данные находятся в США hello для следующих странах и регионах hello:</span><span class="sxs-lookup"><span data-stu-id="ec318-119">Data resides in hello United States for hello following countries/regions:</span></span>

> <span data-ttu-id="ec318-120">Гватемала, Доминиканская Республика, Канада, Коста-Рика, Мексика, Панама, Пуэрто-Рико, США, Тринидад и Тобаго, Эль-Сальвадор.</span><span class="sxs-lookup"><span data-stu-id="ec318-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="ec318-121">Данные хранятся в Европе для следующих странах и регионах hello:</span><span class="sxs-lookup"><span data-stu-id="ec318-121">Data resides in Europe for hello following countries/regions:</span></span>

> <span data-ttu-id="ec318-122">Алжир, Австрия, Азербайджан, Бахрейн, Беларусь, Бельгия, Болгария, Хорватия, Кипр, Чешская Республика, Дания, Египет, Эстония, Финляндия, Франция, Германия, Греция, Венгрия, Исландия, Ирландия, Израиль, Италия, Иордания, Казахстан, Кения, Кувейт, Латвия, Ливан, Лихтенштейн, Литва, Люксембург, Македония (БЮРМ), Мальта, Черногория, Марокко, Нидерланды, Нигерия, Норвегия, Оман, Пакистан, Польша, Португалия, Катар, Румыния, Россия, Саудовская Аравия, Сербия, Словакия, Словения, Южно-Африканская Республика, Испания, Швеция, Швейцария, Тунис, Турция, Украина, Объединенные Арабские Эмираты и Соединенное Королевство.</span><span class="sxs-lookup"><span data-stu-id="ec318-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="ec318-123">Оставшиеся Hello странах и регионах находятся в процесс добавляется список toohello hello.</span><span class="sxs-lookup"><span data-stu-id="ec318-123">hello remaining countries/regions are in hello process of being added toohello list.</span></span>  <span data-ttu-id="ec318-124">Теперь можно по-прежнему использовать Azure AD B2C приняв hello странах и регионах выше.</span><span class="sxs-lookup"><span data-stu-id="ec318-124">For now, you can still use Azure AD B2C by picking any of hello countries/regions above.</span></span>

> <span data-ttu-id="ec318-125">Афганистан, Аргентина, Австралия, Бразилия, Чили, Колумбия, Эквадор, Гонконг, САР, Индия, Индонезия, Ирак, Япония, Корея, Малайзия, Новая Зеландия, Парагвай, Перу, Филиппины, Сингапур, Шри-Ланка, Тайвань, Таиланд, Уругвай и Венесуэла.</span><span class="sxs-lookup"><span data-stu-id="ec318-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="ec318-126">Предварительная версия клиента</span><span class="sxs-lookup"><span data-stu-id="ec318-126">Preview tenant</span></span>
<span data-ttu-id="ec318-127">Если клиент B2C создан в течение периода действия предварительной версии Azure AD B2C, для параметра **Тип клиента** задано значение **Предварительная версия клиента**.</span><span class="sxs-lookup"><span data-stu-id="ec318-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="ec318-128">Если это так, hello вашего клиента необходимо использовать только для целей разработки и тестирования, а не для производственных приложений.</span><span class="sxs-lookup"><span data-stu-id="ec318-128">If this is hello case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec318-129">Отсутствует путь миграции с предварительной версии клиента B2C клиента tooa рабочей среде B2C.</span><span class="sxs-lookup"><span data-stu-id="ec318-129">There is no migration path from a preview B2C tenant tooa production-scale B2C tenant.</span></span> <span data-ttu-id="ec318-130">Здравствуйте, обратите внимание, что существуют известные проблемы при удалении клиента B2C предварительного просмотра и повторного создания B2C рабочей среде клиента с таким же именем домена.</span><span class="sxs-lookup"><span data-stu-id="ec318-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with hello same domain name.</span></span> <span data-ttu-id="ec318-131">У вас есть toocreate клиент B2C рабочей среде с именем другого домена.</span><span class="sxs-lookup"><span data-stu-id="ec318-131">You have toocreate a production-scale B2C tenant with a different domain name.</span></span>


![Снимок экрана: предварительная версия клиента](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
