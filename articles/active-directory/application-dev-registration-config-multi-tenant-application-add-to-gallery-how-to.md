---
title: "Добавление мультитенантного приложения в коллекцию приложений Azure AD | Документы Майкрософт"
description: "В этой статье объясняется, как включить специально разработанное мультитенантное приложение в коллекцию приложений Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 208f0d40bd7a8e8f35f16e1fcb09c305d833dbb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-add-a-multi-tenant-application-to-the-azure-ad-application-gallery"></a><span data-ttu-id="652e1-103">Добавление мультитенантного приложения в коллекцию приложений Azure AD</span><span class="sxs-lookup"><span data-stu-id="652e1-103">How to add a multi-tenant application to the Azure AD application gallery</span></span>

## <a name="what-is-the-azure-ad-application-gallery"></a><span data-ttu-id="652e1-104">Что такое коллекция приложений Azure AD?</span><span class="sxs-lookup"><span data-stu-id="652e1-104">What is the Azure AD Application Gallery?</span></span>

<span data-ttu-id="652e1-105">Коллекция приложений Azure AD является отличным способом представить приложение миллионам пользователей Azure Active Directory, что увеличивает сферу его влияния и позволяет расширить аудиторию приложения в магазине.</span><span class="sxs-lookup"><span data-stu-id="652e1-105">The Azure AD Application Gallery is a great way to get your application in front of all the millions of Azure Active Directory customers to broaden the impact and reach of your application in the marketplace.</span></span> <span data-ttu-id="652e1-106">Ниже показано, как добавить приложение в коллекцию приложений Azure AD.</span><span class="sxs-lookup"><span data-stu-id="652e1-106">The below steps explain how you can list your application in the Azure AD Application Gallery.</span></span>

## <a name="if-your-application-supports-saml-or-openidconnect"></a><span data-ttu-id="652e1-107">Если приложение поддерживает SAML или OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="652e1-107">If your application supports SAML or OpenIDConnect</span></span>
<span data-ttu-id="652e1-108">Если у вас есть многопользовательское приложение, которые вы хотите включить в коллекцию приложений Azure AD, сначала убедитесь, что оно поддерживает одну из следующих технологий единого входа:</span><span class="sxs-lookup"><span data-stu-id="652e1-108">If you have a multi-tenant application you'd like to list in the Azure AD Application Gallery, you must first make sure that your application supports one of the following single sign-on technologies:</span></span>

1. <span data-ttu-id="652e1-109">**OpenID Connect.** Прямая интеграция с Azure AD с помощью OpenID Connect для проверки подлинности и API согласия Azure AD для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="652e1-109">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="652e1-110">Этот режим является рекомендуемым, если вы только начали интеграцию и ваше приложение не поддерживает SAML.</span><span class="sxs-lookup"><span data-stu-id="652e1-110">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
2. <span data-ttu-id="652e1-111">**SAML.** Приложение уже имеет возможность настройки сторонних поставщиков удостоверений с помощью протокола SAML.</span><span class="sxs-lookup"><span data-stu-id="652e1-111">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="652e1-112">Если ваше мультитенантное приложение поддерживает один из этих режимов единого входа и вы бы хотели включить его в коллекцию приложений Azure AD, выполните действия, описанные в документе ниже.</span><span class="sxs-lookup"><span data-stu-id="652e1-112">If your application supports one of these single sign-on modes and you'd like to list your multi-tenant application in the Azure AD Application Gallery, you can follow the steps in the document below.</span></span> <span data-ttu-id="652e1-113">Чтобы быстро начать, отправьте электронное сообщение по адресу **waadpartners@microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="652e1-113">To get started quickly send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="if-your-application-does-not-support-saml-or-openidconnect"></a><span data-ttu-id="652e1-114">Если приложение не поддерживает SAML или OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="652e1-114">If your application does not support SAML or OpenIDConnect</span></span>
<span data-ttu-id="652e1-115">Даже если приложение не поддерживает один из этих режимов, мы по-прежнему можем интегрировать его в свою коллекцию, применив технологию единого входа по паролю.</span><span class="sxs-lookup"><span data-stu-id="652e1-115">Even if your application does not support one of these modes, we can still integrate it into our gallery using our Password Single Sign-on technology.</span></span> <span data-ttu-id="652e1-116">Если вы хотите изучить эту возможность, отправьте электронное сообщение по адресу **waadpartners@microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="652e1-116">If you'd like to explore this option, you can send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="652e1-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="652e1-117">Next steps</span></span>
[<span data-ttu-id="652e1-118">Добавление приложения в коллекцию приложений Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="652e1-118">How to list your application in the Azure Active Directory application gallery</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)
