---
title: "Azure Active Directory B2C: доступность в регионах и местонахождение данных | Документы Майкрософт"
description: "Статья о типах клиентов Azure Active Directory B2C"
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
ms.openlocfilehash: facd66f0324e382ea7609a035de8129ba433846f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="bf9cd-103">Azure Active Directory B2C: доступность в регионах и местонахождение данных</span><span class="sxs-lookup"><span data-stu-id="bf9cd-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="bf9cd-104">Доступность в регионах и местонахождение данных — это два разных понятия, которые применяются к Azure AD B2C не так, как к другим службам Azure.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-104">Region availability and data residency are two very different concepts that apply differently to Azure AD B2C from the rest of Azure.</span></span> <span data-ttu-id="bf9cd-105">В этой статье рассматриваются различия между этими двумя понятиями и сравнивается то, как они применяются к Azure AD B2C и к Azure в целом.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-105">This article will explain the differences between these two concepts and compare how they apply to Azure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="bf9cd-106">Сводка</span><span class="sxs-lookup"><span data-stu-id="bf9cd-106">Summary</span></span>
<span data-ttu-id="bf9cd-107">Служба Azure AD B2C **доступна во всем мире**, но **данные могут находиться в США или Европе**.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-107">Azure AD B2C is **generally available worldwide** with the option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="bf9cd-108">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="bf9cd-108">Concepts</span></span>
* <span data-ttu-id="bf9cd-109">**Доступность в регионах** определяет то, где служба доступна для использования.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-109">**Region availability** refers to where a service is available for use.</span></span>
* <span data-ttu-id="bf9cd-110">**Местонахождение данных** определяет то, где хранятся данные пользователей.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-110">**Data residency** refers to where user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="bf9cd-111">Регионы доступности</span><span class="sxs-lookup"><span data-stu-id="bf9cd-111">Region availability</span></span>
<span data-ttu-id="bf9cd-112">Служба Azure AD B2C доступна во всем мире посредством общедоступного облака Azure.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-112">Azure AD B2C is available worldwide via the Azure public cloud.</span></span> 

<span data-ttu-id="bf9cd-113">Для большинства других служб Azure используется другая модель, в соответствии с которой доступность связана с местонахождением данных.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-113">This differs from the model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="bf9cd-114">Примеры этого можно увидеть на странице [Доступность продуктов по регионам](https://azure.microsoft.com/regions/services/) и в [калькуляторе цен Azure Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="bf9cd-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and the [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="bf9cd-115">Местонахождение данных</span><span class="sxs-lookup"><span data-stu-id="bf9cd-115">Data residency</span></span>
<span data-ttu-id="bf9cd-116">Служба Azure AD B2C сохраняет данные пользователей в США или Европе.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="bf9cd-117">Местонахождение данных зависит от страны или региона, выбранных при [создании клиента Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bf9cd-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Снимок экрана: предварительная версия клиента](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="bf9cd-119">Данные находятся в США при выборе следующих стран или регионов:</span><span class="sxs-lookup"><span data-stu-id="bf9cd-119">Data resides in the United States for the following countries/regions:</span></span>

> <span data-ttu-id="bf9cd-120">Гватемала, Доминиканская Республика, Канада, Коста-Рика, Мексика, Панама, Пуэрто-Рико, США, Тринидад и Тобаго, Эль-Сальвадор.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="bf9cd-121">Данные находятся в Европе при выборе следующих стран или регионов:</span><span class="sxs-lookup"><span data-stu-id="bf9cd-121">Data resides in Europe for the following countries/regions:</span></span>

> <span data-ttu-id="bf9cd-122">Алжир, Австрия, Азербайджан, Бахрейн, Беларусь, Бельгия, Болгария, Хорватия, Кипр, Чешская Республика, Дания, Египет, Эстония, Финляндия, Франция, Германия, Греция, Венгрия, Исландия, Ирландия, Израиль, Италия, Иордания, Казахстан, Кения, Кувейт, Латвия, Ливан, Лихтенштейн, Литва, Люксембург, Македония (БЮРМ), Мальта, Черногория, Марокко, Нидерланды, Нигерия, Норвегия, Оман, Пакистан, Польша, Португалия, Катар, Румыния, Россия, Саудовская Аравия, Сербия, Словакия, Словения, Южно-Африканская Республика, Испания, Швеция, Швейцария, Тунис, Турция, Украина, Объединенные Арабские Эмираты и Соединенное Королевство.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="bf9cd-123">Остальные страны и регионы будут постепенно добавляться в список.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-123">The remaining countries/regions are in the process of being added to the list.</span></span>  <span data-ttu-id="bf9cd-124">Пока же вы можете использовать Azure AD B2C, выбрав любую из стран или регионов, приведенных выше.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-124">For now, you can still use Azure AD B2C by picking any of the countries/regions above.</span></span>

> <span data-ttu-id="bf9cd-125">Афганистан, Аргентина, Австралия, Бразилия, Чили, Колумбия, Эквадор, Гонконг, САР, Индия, Индонезия, Ирак, Япония, Корея, Малайзия, Новая Зеландия, Парагвай, Перу, Филиппины, Сингапур, Шри-Ланка, Тайвань, Таиланд, Уругвай и Венесуэла.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="bf9cd-126">Предварительная версия клиента</span><span class="sxs-lookup"><span data-stu-id="bf9cd-126">Preview tenant</span></span>
<span data-ttu-id="bf9cd-127">Если клиент B2C создан в течение периода действия предварительной версии Azure AD B2C, для параметра **Тип клиента** задано значение **Предварительная версия клиента**.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="bf9cd-128">В этом случае клиент НЕОБХОДИМО использовать для разработки и тестирования, а НЕ для рабочих приложений.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-128">If this is the case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf9cd-129">Способа перехода с предварительной версии клиента B2C на рабочую не существует.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-129">There is no migration path from a preview B2C tenant to a production-scale B2C tenant.</span></span> <span data-ttu-id="bf9cd-130">Обратите внимание, что при удалении существующего клиента B2C предварительной версии и повторном создании клиента B2C рабочей версии с тем же доменным именем могут возникнуть известные проблемы.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with the same domain name.</span></span> <span data-ttu-id="bf9cd-131">Создавайте клиент B2C рабочей версии с другим доменным именем.</span><span class="sxs-lookup"><span data-stu-id="bf9cd-131">You have to create a production-scale B2C tenant with a different domain name.</span></span>


![Снимок экрана: предварительная версия клиента](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
