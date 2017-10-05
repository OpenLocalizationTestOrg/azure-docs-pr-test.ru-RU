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
ms.openlocfilehash: dc8b5cb299da74c88aa5ae82636dc345ddd45a2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-key-vault-in-azure-stack"></a><span data-ttu-id="9abf9-103">Введение в хранилище ключей в стек Azure</span><span class="sxs-lookup"><span data-stu-id="9abf9-103">Introduction to Key Vault in Azure Stack</span></span>

## <a name="before-you-start"></a><span data-ttu-id="9abf9-104">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9abf9-104">Before you start</span></span>
<span data-ttu-id="9abf9-105">В этой статье предполагается следующее:</span><span class="sxs-lookup"><span data-stu-id="9abf9-105">This article assumes the following:</span></span>

* <span data-ttu-id="9abf9-106">Администраторов облака Azure стек должен иметь [создать предложение](azure-stack-create-offer.md) , включающего службы хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9abf9-106">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes the Key Vault service.</span></span>  
* <span data-ttu-id="9abf9-107">Пользователи должны [подписаться на предложение](azure-stack-subscribe-plan-provision-vm.md) , включающего службы хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9abf9-107">Users must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span></span>  
* [<span data-ttu-id="9abf9-108">PowerShell была настроена для использования с стек Azure</span><span class="sxs-lookup"><span data-stu-id="9abf9-108">PowerShell is configured for use with Azure Stack</span></span>](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a><span data-ttu-id="9abf9-109">Основные сведения о хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="9abf9-109">Key Vault basics</span></span>
<span data-ttu-id="9abf9-110">Хранилище ключей Azure стека помогает защитить ключи шифрования и использовать секретные данные, что облачные приложения и службы.</span><span class="sxs-lookup"><span data-stu-id="9abf9-110">Key Vault in Azure Stack helps safeguard cryptographic keys and secrets that cloud applications and services use.</span></span> <span data-ttu-id="9abf9-111">С помощью хранилища ключей, вы можете зашифровать ключи и секретные данные (например, ключей проверки подлинности, ключи учетной записи хранения, ключи шифрования данных, PFX-файлы и пароли).</span><span class="sxs-lookup"><span data-stu-id="9abf9-111">By using Key Vault, you can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .pfx files, and passwords).</span></span>

<span data-ttu-id="9abf9-112">Хранилище ключей упрощает управление ключами и позволяет поддерживать контроль над ключами, которые предоставляют доступ к вашим данным и шифруют их.</span><span class="sxs-lookup"><span data-stu-id="9abf9-112">Key Vault streamlines the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="9abf9-113">Разработчики могут за считанные минуты создавать ключи для разработки и тестирования, а затем с легкостью использовать их в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="9abf9-113">Developers can create keys for development and testing in minutes, and then seamlessly migrate them to production keys.</span></span> <span data-ttu-id="9abf9-114">По необходимости администраторы безопасности могут предоставлять (и отзывать) разрешения на использование ключей.</span><span class="sxs-lookup"><span data-stu-id="9abf9-114">Security administrators can grant (and revoke) permission to keys, as needed.</span></span>

<span data-ttu-id="9abf9-115">Любой пользователь с подпиской Azure стека можно создавать и использовать хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9abf9-115">Anybody with an Azure Stack subscription can create and use key vaults.</span></span> <span data-ttu-id="9abf9-116">Несмотря на то, что хранилище ключей преимущества разработчики и Администраторы безопасности, можно реализовать и управляется администратором облака, ответственный за управление другими службами Azure стека в организации.</span><span class="sxs-lookup"><span data-stu-id="9abf9-116">Although Key Vault benefits developers and security administrators, it can be implemented and managed by the cloud administrator who manages other Azure Stack services for an organization.</span></span> <span data-ttu-id="9abf9-117">Например администратор облака могут выполнить вход с подпиской Azure стека Создание хранилища для организации, в котором для хранения ключей и затем быть ответственным за эти задачи.</span><span class="sxs-lookup"><span data-stu-id="9abf9-117">For example, the cloud administrator can sign in with an Azure Stack subscription, create a vault for the organization in which to store keys, and then be responsible for these operational tasks:</span></span>

* <span data-ttu-id="9abf9-118">создание или импорт ключа или секрета;</span><span class="sxs-lookup"><span data-stu-id="9abf9-118">Create or import a key or secret</span></span>
* <span data-ttu-id="9abf9-119">отзыв или удаление ключа или секрета;</span><span class="sxs-lookup"><span data-stu-id="9abf9-119">Revoke or delete a key or secret</span></span>
* <span data-ttu-id="9abf9-120">Разрешить пользователям или приложениям получать доступ к хранилища ключей, поэтому они могут затем управления или использовать его ключи и секретные коды</span><span class="sxs-lookup"><span data-stu-id="9abf9-120">Authorize users or applications to access the key vault, so they can   then manage or use its keys and secrets</span></span>
* <span data-ttu-id="9abf9-121">настройка использования ключей (например, подписи и шифрования);</span><span class="sxs-lookup"><span data-stu-id="9abf9-121">Configure key usage (for example, sign or encrypt)</span></span>

<span data-ttu-id="9abf9-122">Администратору облака можно предоставить разработчикам с URI для вызова из своих приложений и предоставлять сведения о ведении журнала использования ключа администратора безопасности.</span><span class="sxs-lookup"><span data-stu-id="9abf9-122">The cloud administrator can then provide developers with URIs to call from their applications, and provide a security administrator with key usage logging information.</span></span>

<span data-ttu-id="9abf9-123">Разработчики также могут управлять ключами напрямую с помощью API.</span><span class="sxs-lookup"><span data-stu-id="9abf9-123">Developers can also manage the keys directly, by using APIs.</span></span> <span data-ttu-id="9abf9-124">Дополнительные сведения см. в руководстве для разработчиков хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="9abf9-124">For more information, see the Key Vault developer's guide.</span></span>

## <a name="scenarios"></a><span data-ttu-id="9abf9-125">Сценарии</span><span class="sxs-lookup"><span data-stu-id="9abf9-125">Scenarios</span></span>
<span data-ttu-id="9abf9-126">В следующей таблице описывается некоторые сценарии, где хранилище ключей может удовлетворить потребности разработчиков и администраторов безопасности:</span><span class="sxs-lookup"><span data-stu-id="9abf9-126">The following table depicts some of the scenarios where Key Vault can help meet the needs of developers and security administrators:</span></span>

### <a name="developer-for-an-azure-stack-application"></a><span data-ttu-id="9abf9-127">Разработчик приложения стек Azure</span><span class="sxs-lookup"><span data-stu-id="9abf9-127">Developer for an Azure Stack application</span></span>
<span data-ttu-id="9abf9-128">**Проблема**: я хочу написать приложение для Azure стека, который использует ключи для подписывания и шифрования, но они должны быть внешним из приложения, чтобы решение подходит для приложения, географически распределенных требуется.</span><span class="sxs-lookup"><span data-stu-id="9abf9-128">**Problem**: I want to write an application for Azure Stack that uses keys for signing and encryption, but I want these to be external from my application so that the solution is suitable for an application that is geographically distributed.</span></span>

<span data-ttu-id="9abf9-129">**Инструкция**: ключи хранятся в хранилище и вызываемая URI, если это требуется.</span><span class="sxs-lookup"><span data-stu-id="9abf9-129">**Statement**: Keys are stored in a vault and invoked by URI when needed.</span></span>

### <a name="developer-for-software-as-a-service-saas"></a><span data-ttu-id="9abf9-130">Разработчик программное обеспечение как услуга (SaaS)</span><span class="sxs-lookup"><span data-stu-id="9abf9-130">Developer for software as a service (SaaS)</span></span>
<span data-ttu-id="9abf9-131">**Проблема:** для ли клиент ключи и секретные коды не требуется ответственности или потенциальная ответственность.</span><span class="sxs-lookup"><span data-stu-id="9abf9-131">**Problem:** I don’t want the responsibility or potential liability for my customer's keys and secrets.</span></span>

<span data-ttu-id="9abf9-132">**Инструкции:** клиентов можно импортировать свои собственные ключи в стек Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="9abf9-132">**Statement:** Customers can import their own keys into Azure Stack, and manage them.</span></span> <span data-ttu-id="9abf9-133">Я хочу клиентов для владения и управления ключами, чтобы позволяет сосредоточить усилия на это, что делать лучше всего, который предоставляет основные функции программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="9abf9-133">I want customers to own and manage their keys so that I can concentrate on doing what I do best, which is providing the core software features.</span></span>

### <a name="chief-security-officer-cso"></a><span data-ttu-id="9abf9-134">Руководитель отдела безопасности (CSO)</span><span class="sxs-lookup"><span data-stu-id="9abf9-134">Chief Security Officer (CSO)</span></span>
<span data-ttu-id="9abf9-135">**Проблема:** требуется, чтобы убедиться в том, что Моя организация управляет жизненным циклом ключа и можно отслеживать использование ключа.</span><span class="sxs-lookup"><span data-stu-id="9abf9-135">**Problem:** I want to make sure that my organization is in control of the key life cycle and can monitor key usage.</span></span>

<span data-ttu-id="9abf9-136">**Инструкция** хранилища ключей является разработано таким образом, чтобы корпорация Майкрософт не см или извлечь ключи.</span><span class="sxs-lookup"><span data-stu-id="9abf9-136">**Statement** Key Vault is designed so that Microsoft does not see or extract your keys.</span></span>  <span data-ttu-id="9abf9-137">Если приложению для выполнения криптографических операций с помощью ключей клиентов, хранилище ключей делает это от имени приложения.</span><span class="sxs-lookup"><span data-stu-id="9abf9-137">When an application needs to perform cryptographic operations by using customers’ keys, Key Vault does this on behalf of the application.</span></span> <span data-ttu-id="9abf9-138">Приложение не видит ключи клиентов.</span><span class="sxs-lookup"><span data-stu-id="9abf9-138">The application does not see the customers’ keys.</span></span>  <span data-ttu-id="9abf9-139">Несмотря на то, что мы используем несколько служб Azure стека и ресурсы, необходимо управлять с помощью клавиш из одного расположения в стеке Azure.</span><span class="sxs-lookup"><span data-stu-id="9abf9-139">Although we use multiple Azure Stack services and resources, I want to manage the keys from a single location in Azure Stack.</span></span> <span data-ttu-id="9abf9-140">Хранилище предоставляет единый интерфейс, независимо от того, сколько хранилищ Azure стека, какие регионы они поддержки и приложений, использующих их.</span><span class="sxs-lookup"><span data-stu-id="9abf9-140">The vault provides a single interface, regardless of how many vaults you have in Azure Stack, which regions they support, and which applications use them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9abf9-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9abf9-141">Next Steps</span></span>

* [<span data-ttu-id="9abf9-142">Хранилище ключей Azure стека с помощью портала управления</span><span class="sxs-lookup"><span data-stu-id="9abf9-142">Manage Key Vault in Azure Stack using the portal</span></span>](azure-stack-kv-manage-portal.md)  
* [<span data-ttu-id="9abf9-143">Управление хранилищем ключей Azure стека с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="9abf9-143">Manage Key Vault in Azure Stack using PowerShell</span></span>](azure-stack-kv-manage-powershell.md)
