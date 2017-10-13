---
title: "Azure введение в хранилище ключей стек | Документы Microsoft"
description: "Узнайте, как хранилище ключей Azure стека управляет ключи и секретные коды"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 70f1684a-3fbb-4cd1-bf29-9f9882e98fe9
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/04/2017
ms.author: sngun
ms.openlocfilehash: ecb542e967669fc4e4465ae59b3e9c37e4a5c332
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="introduction-to-key-vault-in-azure-stack"></a><span data-ttu-id="5404a-103">Введение в хранилище ключей в стек Azure</span><span class="sxs-lookup"><span data-stu-id="5404a-103">Introduction to Key Vault in Azure Stack</span></span>

## <a name="before-you-start"></a><span data-ttu-id="5404a-104">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="5404a-104">Before you start</span></span>
<span data-ttu-id="5404a-105">В этой статье предполагается следующее:</span><span class="sxs-lookup"><span data-stu-id="5404a-105">This article assumes the following:</span></span>

* <span data-ttu-id="5404a-106">Необходимо необходимо подписаться на предложение, которая включает службу хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="5404a-106">You must must subscribe to an offer that includes the Key Vault service.</span></span>  
* [<span data-ttu-id="5404a-107">PowerShell была настроена для использования с стек Azure</span><span class="sxs-lookup"><span data-stu-id="5404a-107">PowerShell is configured for use with Azure Stack</span></span>](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a><span data-ttu-id="5404a-108">Основные сведения о хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="5404a-108">Key Vault basics</span></span>
<span data-ttu-id="5404a-109">Хранилище ключей Azure стека помогает защитить ключи шифрования и использовать секретные данные, что облачные приложения и службы.</span><span class="sxs-lookup"><span data-stu-id="5404a-109">Key Vault in Azure Stack helps safeguard cryptographic keys and secrets that cloud applications and services use.</span></span> <span data-ttu-id="5404a-110">С помощью хранилища ключей, вы можете зашифровать ключи и секретные данные (например, ключей проверки подлинности, ключи учетной записи хранения, ключи шифрования данных, PFX-файлы и пароли).</span><span class="sxs-lookup"><span data-stu-id="5404a-110">By using Key Vault, you can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .pfx files, and passwords).</span></span>

<span data-ttu-id="5404a-111">Хранилище ключей упрощает управление ключами и позволяет поддерживать контроль над ключами, которые предоставляют доступ к вашим данным и шифруют их.</span><span class="sxs-lookup"><span data-stu-id="5404a-111">Key Vault streamlines the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="5404a-112">Разработчики могут за считанные минуты создавать ключи для разработки и тестирования, а затем с легкостью использовать их в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5404a-112">Developers can create keys for development and testing in minutes, and then seamlessly migrate them to production keys.</span></span> <span data-ttu-id="5404a-113">По необходимости администраторы безопасности могут предоставлять (и отзывать) разрешения на использование ключей.</span><span class="sxs-lookup"><span data-stu-id="5404a-113">Security administrators can grant (and revoke) permission to keys, as needed.</span></span>

<span data-ttu-id="5404a-114">Любой пользователь с подпиской Azure стека можно создавать и использовать хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="5404a-114">Anybody with an Azure Stack subscription can create and use key vaults.</span></span> <span data-ttu-id="5404a-115">Несмотря на то, что хранилище ключей преимущества разработчики и Администраторы безопасности, можно реализовать и управляется оператор, ответственный за управление другими службами Azure стека в организации.</span><span class="sxs-lookup"><span data-stu-id="5404a-115">Although Key Vault benefits developers and security administrators, it can be implemented and managed by the operator who manages other Azure Stack services for an organization.</span></span> <span data-ttu-id="5404a-116">Например оператор могут выполнить вход с подпиской Azure стека стек Azure создайте хранилище для организации, в котором для хранения ключей и затем быть ответственным за эти задачи:</span><span class="sxs-lookup"><span data-stu-id="5404a-116">For example, the Azure Stack operator can sign in with an Azure Stack subscription, create a vault for the organization in which to store keys, and then be responsible for these operational tasks:</span></span>

* <span data-ttu-id="5404a-117">создание или импорт ключа или секрета;</span><span class="sxs-lookup"><span data-stu-id="5404a-117">Create or import a key or secret</span></span>
* <span data-ttu-id="5404a-118">отзыв или удаление ключа или секрета;</span><span class="sxs-lookup"><span data-stu-id="5404a-118">Revoke or delete a key or secret</span></span>
* <span data-ttu-id="5404a-119">Разрешить пользователям или приложениям получать доступ к хранилища ключей, поэтому они могут затем управления или использовать его ключи и секретные коды</span><span class="sxs-lookup"><span data-stu-id="5404a-119">Authorize users or applications to access the key vault, so they can   then manage or use its keys and secrets</span></span>
* <span data-ttu-id="5404a-120">настройка использования ключей (например, подписи и шифрования);</span><span class="sxs-lookup"><span data-stu-id="5404a-120">Configure key usage (for example, sign or encrypt)</span></span>

<span data-ttu-id="5404a-121">Оператор можно предоставить разработчикам с URI для вызова из своих приложений и предоставлять сведения о ведении журнала использования ключа администратора безопасности.</span><span class="sxs-lookup"><span data-stu-id="5404a-121">The operator can then provide developers with URIs to call from their applications, and provide a security administrator with key usage logging information.</span></span>

<span data-ttu-id="5404a-122">Разработчики также могут управлять ключами напрямую с помощью API.</span><span class="sxs-lookup"><span data-stu-id="5404a-122">Developers can also manage the keys directly, by using APIs.</span></span> <span data-ttu-id="5404a-123">Дополнительные сведения см. в руководстве для разработчиков хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="5404a-123">For more information, see the Key Vault developer's guide.</span></span>

## <a name="scenarios"></a><span data-ttu-id="5404a-124">Сценарии</span><span class="sxs-lookup"><span data-stu-id="5404a-124">Scenarios</span></span>
<span data-ttu-id="5404a-125">В следующей таблице описывается некоторые сценарии, где хранилище ключей может удовлетворить потребности разработчиков и администраторов безопасности:</span><span class="sxs-lookup"><span data-stu-id="5404a-125">The following table depicts some of the scenarios where Key Vault can help meet the needs of developers and security administrators:</span></span>

### <a name="developer-for-an-azure-stack-application"></a><span data-ttu-id="5404a-126">Разработчик приложения стек Azure</span><span class="sxs-lookup"><span data-stu-id="5404a-126">Developer for an Azure Stack application</span></span>
<span data-ttu-id="5404a-127">**Проблема**: я хочу написать приложение для Azure стека, который использует ключи для подписывания и шифрования, но они должны быть внешним из приложения, чтобы решение подходит для приложения, географически распределенных требуется.</span><span class="sxs-lookup"><span data-stu-id="5404a-127">**Problem**: I want to write an application for Azure Stack that uses keys for signing and encryption, but I want these to be external from my application so that the solution is suitable for an application that is geographically distributed.</span></span>

<span data-ttu-id="5404a-128">**Инструкция**: ключи хранятся в хранилище и вызываемая URI, если это требуется.</span><span class="sxs-lookup"><span data-stu-id="5404a-128">**Statement**: Keys are stored in a vault and invoked by URI when needed.</span></span>

### <a name="developer-for-software-as-a-service-saas"></a><span data-ttu-id="5404a-129">Разработчик программное обеспечение как услуга (SaaS)</span><span class="sxs-lookup"><span data-stu-id="5404a-129">Developer for software as a service (SaaS)</span></span>
<span data-ttu-id="5404a-130">**Проблема:** для ли клиент ключи и секретные коды не требуется ответственности или потенциальная ответственность.</span><span class="sxs-lookup"><span data-stu-id="5404a-130">**Problem:** I don’t want the responsibility or potential liability for my customer's keys and secrets.</span></span>

<span data-ttu-id="5404a-131">**Инструкции:** клиентов можно импортировать свои собственные ключи в стек Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="5404a-131">**Statement:** Customers can import their own keys into Azure Stack, and manage them.</span></span> <span data-ttu-id="5404a-132">Я хочу клиентов для владения и управления ключами, чтобы позволяет сосредоточить усилия на это, что делать лучше всего, который предоставляет основные функции программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="5404a-132">I want customers to own and manage their keys so that I can concentrate on doing what I do best, which is providing the core software features.</span></span>

### <a name="chief-security-officer-cso"></a><span data-ttu-id="5404a-133">Руководитель отдела безопасности (CSO)</span><span class="sxs-lookup"><span data-stu-id="5404a-133">Chief Security Officer (CSO)</span></span>
<span data-ttu-id="5404a-134">**Проблема:** требуется, чтобы убедиться в том, что Моя организация управляет жизненным циклом ключа и можно отслеживать использование ключа.</span><span class="sxs-lookup"><span data-stu-id="5404a-134">**Problem:** I want to make sure that my organization is in control of the key life cycle and can monitor key usage.</span></span>

<span data-ttu-id="5404a-135">**Инструкция** хранилища ключей является разработано таким образом, чтобы корпорация Майкрософт не см или извлечь ключи.</span><span class="sxs-lookup"><span data-stu-id="5404a-135">**Statement** Key Vault is designed so that Microsoft does not see or extract your keys.</span></span>  <span data-ttu-id="5404a-136">Если приложению для выполнения криптографических операций с помощью ключей клиентов, хранилище ключей делает это от имени приложения.</span><span class="sxs-lookup"><span data-stu-id="5404a-136">When an application needs to perform cryptographic operations by using customers’ keys, Key Vault does this on behalf of the application.</span></span> <span data-ttu-id="5404a-137">Приложение не видит ключи клиентов.</span><span class="sxs-lookup"><span data-stu-id="5404a-137">The application does not see the customers’ keys.</span></span>  <span data-ttu-id="5404a-138">Несмотря на то, что мы используем несколько служб Azure стека и ресурсы, необходимо управлять с помощью клавиш из одного расположения в стеке Azure.</span><span class="sxs-lookup"><span data-stu-id="5404a-138">Although we use multiple Azure Stack services and resources, I want to manage the keys from a single location in Azure Stack.</span></span> <span data-ttu-id="5404a-139">Хранилище предоставляет единый интерфейс, независимо от того, сколько хранилищ Azure стека, какие регионы они поддержки и приложений, использующих их.</span><span class="sxs-lookup"><span data-stu-id="5404a-139">The vault provides a single interface, regardless of how many vaults you have in Azure Stack, which regions they support, and which applications use them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5404a-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5404a-140">Next Steps</span></span>

* [<span data-ttu-id="5404a-141">Хранилище ключей Azure стека с помощью портала управления</span><span class="sxs-lookup"><span data-stu-id="5404a-141">Manage Key Vault in Azure Stack using the portal</span></span>](azure-stack-kv-manage-portal.md)  
* [<span data-ttu-id="5404a-142">Управление хранилищем ключей Azure стека с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="5404a-142">Manage Key Vault in Azure Stack using PowerShell</span></span>](azure-stack-kv-manage-powershell.md)
