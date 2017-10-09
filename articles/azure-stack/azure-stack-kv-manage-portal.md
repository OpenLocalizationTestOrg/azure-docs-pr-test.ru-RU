---
title: "aaaManage хранилище ключей Azure стека с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как toomanage хранилище ключей Azure стека с помощью PowerShell."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 0a3aa6eb0b2c2976935d995a0bf6f226dc4eac84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-in-azure-stack-using-hello-portal"></a><span data-ttu-id="301f0-103">Управление хранилищем ключей Azure стека с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="301f0-103">Manage Key Vault in Azure Stack using hello portal</span></span>

<span data-ttu-id="301f0-104">Хранилище ключей Azure стека можно управлять с помощью портала Azure стека hello.</span><span class="sxs-lookup"><span data-stu-id="301f0-104">You can manage Key Vault in Azure Stack by using hello Azure Stack portal.</span></span> <span data-ttu-id="301f0-105">Эта статья поможет вам получить toocreate работы и управление хранилищем ключей Azure стека.</span><span class="sxs-lookup"><span data-stu-id="301f0-105">This article helps you get started toocreate and manage Key Vault in Azure Stack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="301f0-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="301f0-106">Prerequisites</span></span>  

* <span data-ttu-id="301f0-107">Администраторов облака Azure стек должен иметь [создать предложение](azure-stack-create-offer.md) , включающего службы хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="301f0-107">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Key Vault service.</span></span>  
* <span data-ttu-id="301f0-108">Пользователи должны [подписаться предложение tooan](azure-stack-subscribe-plan-provision-vm.md) , включающего службы хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="301f0-108">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
 
## <a name="create-a-key-vault"></a><span data-ttu-id="301f0-109">Создайте хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="301f0-109">Create a key vault</span></span> 

1. <span data-ttu-id="301f0-110">Войдите в портал пользователей toohello (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="301f0-110">Sign in toohello user portal(https://portal.local.azurestack.external).</span></span>  

2. <span data-ttu-id="301f0-111">Hello мониторинга, щелкните **Создать > Безопасность + удостоверения > хранилище ключей**.</span><span class="sxs-lookup"><span data-stu-id="301f0-111">From hello dashboard, click **New > Security + Identity > Key Vault**.</span></span>  

    ![Экран кв](media/azure-stack-kv-manage-portal/image1.png)  

3. <span data-ttu-id="301f0-113">На hello **Создание хранилища ключей** колонке назначить **имя** хранилища.</span><span class="sxs-lookup"><span data-stu-id="301f0-113">On hello **Create Key Vault** blade, assign a **Name** for your vault.</span></span> <span data-ttu-id="301f0-114">Имя хранилища может содержать только буквы, цифры, hello специальный символ дефиса (-), и он не должен начинаться с цифры.</span><span class="sxs-lookup"><span data-stu-id="301f0-114">Vault name can contain only alphanumeric characters, hello special character hyphen (-), and it shouldn’t start with a number.</span></span>  

4. <span data-ttu-id="301f0-115">Выберите **подписки** из списка доступных подписок hello.</span><span class="sxs-lookup"><span data-stu-id="301f0-115">Choose a **Subscription** from hello list of available subscriptions.</span></span> <span data-ttu-id="301f0-116">Все подписки, которые предоставляют службы хранилища ключей hello, отображаются в раскрывающемся списке hello.</span><span class="sxs-lookup"><span data-stu-id="301f0-116">All subscriptions that offer hello Key Vault service are displayed in hello drop-down.</span></span>  

5. <span data-ttu-id="301f0-117">Выберите существующую **группы ресурсов** или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="301f0-117">Select an existing **Resource Group** or create a new one.</span></span>  

6. <span data-ttu-id="301f0-118">Выберите hello **Ценовая категория**.</span><span class="sxs-lookup"><span data-stu-id="301f0-118">Select hello **Pricing tier**.</span></span>  
    >[!NOTE]
    > <span data-ttu-id="301f0-119">Ключ хранилища в Azure пакет средств разработки стека поддержки **Стандартная** только в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="301f0-119">Key vaults in Azure Stack Development Kit support **Standard** SKU only.</span></span>

7. <span data-ttu-id="301f0-120">Выберите существующую **политики доступа** или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="301f0-120">Choose an existing **Access policies** or create a new one.</span></span> <span data-ttu-id="301f0-121">Политика доступа позволяет toogrant разрешения для пользователя, приложения или безопасности tooperform операции группы в этом хранилище.</span><span class="sxs-lookup"><span data-stu-id="301f0-121">Access policy allows you toogrant permissions for a user, application, or a security group tooperform operations with this vault.</span></span>  

8. <span data-ttu-id="301f0-122">При необходимости выберите **политика расширенного доступа** tooenable hello функций, как получить доступ к компьютерам tooVirtual для развертывания, доступа tooResource Manager для развертывания шаблона и доступа tooAzure шифрование диска для тома шифрование.</span><span class="sxs-lookup"><span data-stu-id="301f0-122">Optionally, choose an **Advanced access policy** tooenable hello features like access tooVirtual Machines for deployment, access tooResource Manager for template deployment and access tooAzure Disk Encryption for volume encryption.</span></span> 
  
9.  <span data-ttu-id="301f0-123">После настройки параметров hello, нажмите кнопку **ОК** и затем **создать**.</span><span class="sxs-lookup"><span data-stu-id="301f0-123">After configuring hello settings, click **OK** and then **Create**.</span></span> <span data-ttu-id="301f0-124">При этом запустится развертывания hello хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="301f0-124">This starts hello key vault deployment.</span></span> 

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="301f0-125">Управление ключами и секретов</span><span class="sxs-lookup"><span data-stu-id="301f0-125">Manage keys and secrets</span></span>

<span data-ttu-id="301f0-126">После создания хранилища, используйте следующие шаги toocreate hello и управление ими ключи и секретные данные в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="301f0-126">After you create a vault, use hello following steps toocreate and manage keys and secrets within hello vault.</span></span>

## <a name="create-a-key"></a><span data-ttu-id="301f0-127">Создание ключа</span><span class="sxs-lookup"><span data-stu-id="301f0-127">Create a key</span></span>

1. <span data-ttu-id="301f0-128">Войдите в портал пользователей toohello (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="301f0-128">Sign in toohello user portal (https://portal.local.azurestack.external).</span></span>  

2. <span data-ttu-id="301f0-129">Hello мониторинга, щелкните **все ресурсы** > хранилища ключей hello выберите ранее созданную > щелкните hello **ключей** плитки.</span><span class="sxs-lookup"><span data-stu-id="301f0-129">From hello dashboard, click **All resources** > select hello key vault that you created earlier> click hello **Keys** tile.</span></span>  

3. <span data-ttu-id="301f0-130">Из hello **ключей** колонка, щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="301f0-130">From hello **Keys** blade, click **Add**.</span></span> 

4. <span data-ttu-id="301f0-131">На hello **создать ключ** колонки, список hello формы **параметры**, выберите метод hello, которые должны toouse toocreate ключа.</span><span class="sxs-lookup"><span data-stu-id="301f0-131">On hello **Create a key** blade, form hello list of **Options**, choose hello method that you want toouse toocreate a key.</span></span> <span data-ttu-id="301f0-132">Вы можете **формирования** новый ключ **отправить** существующего ключа, или **восстановление резервной копии** ключа.</span><span class="sxs-lookup"><span data-stu-id="301f0-132">You can **Generate** a new key, **Upload** an existing key, or **Restore Backup** key.</span></span>  

5. <span data-ttu-id="301f0-133">Введите **имя** для ключа.</span><span class="sxs-lookup"><span data-stu-id="301f0-133">Enter a **Name** for your key.</span></span> <span data-ttu-id="301f0-134">Имя ключа Hello может содержать только буквенно-цифровые символы и hello специальный символ дефиса (-).</span><span class="sxs-lookup"><span data-stu-id="301f0-134">hello key name can contain only alphanumeric characters and hello special character hyphen (-).</span></span>  

6. <span data-ttu-id="301f0-135">При необходимости настройте **задать дату активации** и **Дата истечения срока действия** значения ключа.</span><span class="sxs-lookup"><span data-stu-id="301f0-135">Optionally, configure **Set activation date** and **Set expiration date** values for your key.</span></span>  

7. <span data-ttu-id="301f0-136">Нажмите кнопку **создать** toostart hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="301f0-136">Click **Create** toostart hello deployment.</span></span>  

<span data-ttu-id="301f0-137">После успешного создания ключа hello, можно выбрать его из hello **ключей** колонки и просмотреть или изменить его свойства.</span><span class="sxs-lookup"><span data-stu-id="301f0-137">After hello key is successfully created, you can select it from hello **Keys** blade and view or modify its properties.</span></span> <span data-ttu-id="301f0-138">в разделе свойств Hello содержит hello **идентификатор ключа**, URI, по которому внешние приложения могут обращаться к этот ключ.</span><span class="sxs-lookup"><span data-stu-id="301f0-138">hello properties section contains hello **Key Identifier**, a URI by which external applications can access this key.</span></span> <span data-ttu-id="301f0-139">операции toolimit на этот ключ, настройте параметры в разделе **разрешенные операции**.</span><span class="sxs-lookup"><span data-stu-id="301f0-139">toolimit operations on this key, configure settings under **Permitted operations**.</span></span>

![Ключ URI](media/azure-stack-kv-manage-portal/image4.png)  

## <a name="create-a-secret"></a><span data-ttu-id="301f0-141">Создание секрета</span><span class="sxs-lookup"><span data-stu-id="301f0-141">Create a secret</span></span> 

1. <span data-ttu-id="301f0-142">Войдите в портал пользователей toohello (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="301f0-142">Sign in toohello user portal (https://portal.local.azurestack.external).</span></span>  
2. <span data-ttu-id="301f0-143">Hello мониторинга, щелкните **все ресурсы** > хранилища ключей hello выберите ранее созданную > щелкните hello **секреты** плитки.</span><span class="sxs-lookup"><span data-stu-id="301f0-143">From hello dashboard, click **All resources** > select hello key vault that you created earlier> click hello **Secrets** tile.</span></span>  

3. <span data-ttu-id="301f0-144">Из hello **секреты** колонка, щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="301f0-144">From hello **Secrets** blade, click **Add**.</span></span>  

4. <span data-ttu-id="301f0-145">На hello **Создание секрета** колонку из списка hello **параметры отправки**, выберите один из вариантов, по которому требуется toocreate секрета.</span><span class="sxs-lookup"><span data-stu-id="301f0-145">On hello **Create a secret** blade, from hello list of **Upload options**, choose an option by which you want toocreate a secret.</span></span> <span data-ttu-id="301f0-146">Можно создать секрет **вручную** путем ввода значения для секрет hello, или загрузить **сертификат** с локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="301f0-146">You can create a secret **Manually** by entering a value for hello secret, or by uploading a **Certificate** from your local machine.</span></span>  

5. <span data-ttu-id="301f0-147">Введите **имя** для hello секрета.</span><span class="sxs-lookup"><span data-stu-id="301f0-147">Enter a **Name** for hello secret.</span></span> <span data-ttu-id="301f0-148">Hello секретное имя может содержать только буквенно-цифровые символы и hello специальный символ дефиса (-).</span><span class="sxs-lookup"><span data-stu-id="301f0-148">hello secret name can contain only alphanumeric characters and hello special character hyphen (-).</span></span>  

6. <span data-ttu-id="301f0-149">При необходимости укажите hello **тип содержимого**и настройте значения для **задать дату активации** и **Дата истечения срока действия** значения для hello секрета.</span><span class="sxs-lookup"><span data-stu-id="301f0-149">Optionally, specify hello **Content type**, and configure values for **Set activation date** and **Set expiration date** values for hello secret.</span></span>  

7. <span data-ttu-id="301f0-150">Нажмите кнопку Создать toostart hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="301f0-150">Click Create toostart hello deployment.</span></span>  

<span data-ttu-id="301f0-151">После успешного создания hello секрет можно выбрать его из hello **секреты** колонки и просмотреть или изменить его свойства.</span><span class="sxs-lookup"><span data-stu-id="301f0-151">After hello secret is successfully created, you can select it from hello **Secrets** blade and view or modify its properties.</span></span> <span data-ttu-id="301f0-152">содержит свойства раздела Hello **идентификатор секрета**, URI, по которому внешние приложения могут обращаться к этот секрет.</span><span class="sxs-lookup"><span data-stu-id="301f0-152">hello properties section contains **Secret Identifier**, a URI by which external applications can access this secret.</span></span> 

![Секретный код URI](media/azure-stack-kv-manage-portal/image5.png) 


## <a name="next-steps"></a><span data-ttu-id="301f0-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="301f0-154">Next Steps</span></span>
* [<span data-ttu-id="301f0-155">Развертывание виртуальной Машины, получая hello пароль, которые хранятся в хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="301f0-155">Deploy a VM by retrieving hello password stored in a key vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)  
* [<span data-ttu-id="301f0-156">Развертывание виртуальной Машины с помощью сертификата, хранящегося в хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="301f0-156">Deploy a VM with certificate stored in a key vault</span></span>](azure-stack-kv-push-secret-into-vm.md)     


