---
title: "Введение стек хранилища ключей aaaAzure | Документы Microsoft"
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
ms.openlocfilehash: 12bf9c219c4b2bba37467cafca721a632caa9f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tookey-vault-in-azure-stack"></a><span data-ttu-id="494e1-103">Введение tooKey хранилища Azure стека</span><span class="sxs-lookup"><span data-stu-id="494e1-103">Introduction tooKey Vault in Azure Stack</span></span>

## <a name="before-you-start"></a><span data-ttu-id="494e1-104">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="494e1-104">Before you start</span></span>
<span data-ttu-id="494e1-105">В этой статье предполагается hello следующее:</span><span class="sxs-lookup"><span data-stu-id="494e1-105">This article assumes hello following:</span></span>

* <span data-ttu-id="494e1-106">Администраторов облака Azure стек должен иметь [создать предложение](azure-stack-create-offer.md) , включающего службы хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="494e1-106">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Key Vault service.</span></span>  
* <span data-ttu-id="494e1-107">Пользователи должны [подписаться предложение tooan](azure-stack-subscribe-plan-provision-vm.md) , включающего службы хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="494e1-107">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
* [<span data-ttu-id="494e1-108">PowerShell была настроена для использования с стек Azure</span><span class="sxs-lookup"><span data-stu-id="494e1-108">PowerShell is configured for use with Azure Stack</span></span>](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a><span data-ttu-id="494e1-109">Основные сведения о хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="494e1-109">Key Vault basics</span></span>
<span data-ttu-id="494e1-110">Хранилище ключей Azure стека помогает защитить ключи шифрования и использовать секретные данные, что облачные приложения и службы.</span><span class="sxs-lookup"><span data-stu-id="494e1-110">Key Vault in Azure Stack helps safeguard cryptographic keys and secrets that cloud applications and services use.</span></span> <span data-ttu-id="494e1-111">С помощью хранилища ключей, вы можете зашифровать ключи и секретные данные (например, ключей проверки подлинности, ключи учетной записи хранения, ключи шифрования данных, PFX-файлы и пароли).</span><span class="sxs-lookup"><span data-stu-id="494e1-111">By using Key Vault, you can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .pfx files, and passwords).</span></span>

<span data-ttu-id="494e1-112">Хранилище ключей упрощает процесс управления ключами hello и позволяет toomaintain управление ключами, которые обращаются к и шифрование данных.</span><span class="sxs-lookup"><span data-stu-id="494e1-112">Key Vault streamlines hello key management process and enables you toomaintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="494e1-113">Разработчики могут создавать ключи для разработки и тестирования в минутах и легко перенести их tooproduction ключей.</span><span class="sxs-lookup"><span data-stu-id="494e1-113">Developers can create keys for development and testing in minutes, and then seamlessly migrate them tooproduction keys.</span></span> <span data-ttu-id="494e1-114">Администраторы безопасности можно предоставить (и отменять) tookeys разрешение, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="494e1-114">Security administrators can grant (and revoke) permission tookeys, as needed.</span></span>

<span data-ttu-id="494e1-115">Любой пользователь с подпиской Azure стека можно создавать и использовать хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="494e1-115">Anybody with an Azure Stack subscription can create and use key vaults.</span></span> <span data-ttu-id="494e1-116">Несмотря на то, что хранилище ключей преимущества разработчики и Администраторы безопасности, он позволяет реализовывать и управляется облака Здравствуйте, администратор, ответственный за управление другими службами Azure стека в организации.</span><span class="sxs-lookup"><span data-stu-id="494e1-116">Although Key Vault benefits developers and security administrators, it can be implemented and managed by hello cloud administrator who manages other Azure Stack services for an organization.</span></span> <span data-ttu-id="494e1-117">Например администратор облака hello можно вход с подпиской Azure стека, создать хранилище для организации hello в какие ключи toostore и затем быть ответственным за эти задачи:</span><span class="sxs-lookup"><span data-stu-id="494e1-117">For example, hello cloud administrator can sign in with an Azure Stack subscription, create a vault for hello organization in which toostore keys, and then be responsible for these operational tasks:</span></span>

* <span data-ttu-id="494e1-118">создание или импорт ключа или секрета;</span><span class="sxs-lookup"><span data-stu-id="494e1-118">Create or import a key or secret</span></span>
* <span data-ttu-id="494e1-119">отзыв или удаление ключа или секрета;</span><span class="sxs-lookup"><span data-stu-id="494e1-119">Revoke or delete a key or secret</span></span>
* <span data-ttu-id="494e1-120">Авторизация пользователей или tooaccess приложения hello хранилища ключей, поэтому они могут затем управления или использовать его ключи и секретные коды</span><span class="sxs-lookup"><span data-stu-id="494e1-120">Authorize users or applications tooaccess hello key vault, so they can   then manage or use its keys and secrets</span></span>
* <span data-ttu-id="494e1-121">настройка использования ключей (например, подписи и шифрования);</span><span class="sxs-lookup"><span data-stu-id="494e1-121">Configure key usage (for example, sign or encrypt)</span></span>

<span data-ttu-id="494e1-122">Здравствуйте, администратор облака можно предоставлять разработчикам toocall идентификаторы URI из своих приложений и предоставлять сведения о ведении журнала использования ключа администратора безопасности.</span><span class="sxs-lookup"><span data-stu-id="494e1-122">hello cloud administrator can then provide developers with URIs toocall from their applications, and provide a security administrator with key usage logging information.</span></span>

<span data-ttu-id="494e1-123">Разработчики также можно управлять ключами hello напрямую, с помощью API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="494e1-123">Developers can also manage hello keys directly, by using APIs.</span></span> <span data-ttu-id="494e1-124">Дополнительные сведения см. в разделе руководства разработчика hello хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="494e1-124">For more information, see hello Key Vault developer's guide.</span></span>

## <a name="scenarios"></a><span data-ttu-id="494e1-125">Сценарии</span><span class="sxs-lookup"><span data-stu-id="494e1-125">Scenarios</span></span>
<span data-ttu-id="494e1-126">Hello следующей таблице показаны некоторые сценарии hello, где хранилище ключей может удовлетворить потребности hello разработчиков и администраторов безопасности:</span><span class="sxs-lookup"><span data-stu-id="494e1-126">hello following table depicts some of hello scenarios where Key Vault can help meet hello needs of developers and security administrators:</span></span>

### <a name="developer-for-an-azure-stack-application"></a><span data-ttu-id="494e1-127">Разработчик приложения стек Azure</span><span class="sxs-lookup"><span data-stu-id="494e1-127">Developer for an Azure Stack application</span></span>
<span data-ttu-id="494e1-128">**Проблема**: требуется toowrite приложения для Azure стека, который использует ключи для подписывания и шифрования, но мне нужно эти toobe внешних из приложения, чтобы решение hello подходит для приложения, географически распределены.</span><span class="sxs-lookup"><span data-stu-id="494e1-128">**Problem**: I want toowrite an application for Azure Stack that uses keys for signing and encryption, but I want these toobe external from my application so that hello solution is suitable for an application that is geographically distributed.</span></span>

<span data-ttu-id="494e1-129">**Инструкция**: ключи хранятся в хранилище и вызываемая URI, если это требуется.</span><span class="sxs-lookup"><span data-stu-id="494e1-129">**Statement**: Keys are stored in a vault and invoked by URI when needed.</span></span>

### <a name="developer-for-software-as-a-service-saas"></a><span data-ttu-id="494e1-130">Разработчик программное обеспечение как услуга (SaaS)</span><span class="sxs-lookup"><span data-stu-id="494e1-130">Developer for software as a service (SaaS)</span></span>
<span data-ttu-id="494e1-131">**Проблема:** для ли клиент ключи и секретные коды не требуется hello ответственности или потенциальная ответственности.</span><span class="sxs-lookup"><span data-stu-id="494e1-131">**Problem:** I don’t want hello responsibility or potential liability for my customer's keys and secrets.</span></span>

<span data-ttu-id="494e1-132">**Инструкции:** клиентов можно импортировать свои собственные ключи в стек Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="494e1-132">**Statement:** Customers can import their own keys into Azure Stack, and manage them.</span></span> <span data-ttu-id="494e1-133">Я требуется tooown клиентов и управление ключами, чтобы позволяет сосредоточить усилия на это, что делать лучше всего, который предоставляет hello основные возможности программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="494e1-133">I want customers tooown and manage their keys so that I can concentrate on doing what I do best, which is providing hello core software features.</span></span>

### <a name="chief-security-officer-cso"></a><span data-ttu-id="494e1-134">Руководитель отдела безопасности (CSO)</span><span class="sxs-lookup"><span data-stu-id="494e1-134">Chief Security Officer (CSO)</span></span>
<span data-ttu-id="494e1-135">**Проблема:** я требуется toomake том, что управление жизненным циклом ключа hello моей организации и можно отслеживать использование ключа.</span><span class="sxs-lookup"><span data-stu-id="494e1-135">**Problem:** I want toomake sure that my organization is in control of hello key life cycle and can monitor key usage.</span></span>

<span data-ttu-id="494e1-136">**Инструкция** хранилища ключей является разработано таким образом, чтобы корпорация Майкрософт не см или извлечь ключи.</span><span class="sxs-lookup"><span data-stu-id="494e1-136">**Statement** Key Vault is designed so that Microsoft does not see or extract your keys.</span></span>  <span data-ttu-id="494e1-137">Если приложению требуется tooperform криптографических операций с помощью ключей клиентов, хранилище ключей делает это от имени приложения hello.</span><span class="sxs-lookup"><span data-stu-id="494e1-137">When an application needs tooperform cryptographic operations by using customers’ keys, Key Vault does this on behalf of hello application.</span></span> <span data-ttu-id="494e1-138">приложение Hello не видит ключи hello клиентов.</span><span class="sxs-lookup"><span data-stu-id="494e1-138">hello application does not see hello customers’ keys.</span></span>  <span data-ttu-id="494e1-139">Несмотря на то, что мы используем несколько служб Azure стека и ресурсы, я хочу toomanage hello ключи из одного расположения в стеке Azure.</span><span class="sxs-lookup"><span data-stu-id="494e1-139">Although we use multiple Azure Stack services and resources, I want toomanage hello keys from a single location in Azure Stack.</span></span> <span data-ttu-id="494e1-140">хранилище Hello предоставляет единый интерфейс, независимо от того, сколько хранилищ Azure стека, какие регионы они поддержки и приложений, использующих их.</span><span class="sxs-lookup"><span data-stu-id="494e1-140">hello vault provides a single interface, regardless of how many vaults you have in Azure Stack, which regions they support, and which applications use them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="494e1-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="494e1-141">Next Steps</span></span>

* [<span data-ttu-id="494e1-142">Управление хранилищем ключей Azure стека с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="494e1-142">Manage Key Vault in Azure Stack using hello portal</span></span>](azure-stack-kv-manage-portal.md)  
* [<span data-ttu-id="494e1-143">Управление хранилищем ключей Azure стека с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="494e1-143">Manage Key Vault in Azure Stack using PowerShell</span></span>](azure-stack-kv-manage-powershell.md)
