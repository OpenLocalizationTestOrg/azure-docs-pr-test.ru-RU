---
title: "aaaUsing сертификатов с помощью пакет интеграции Enterprise | Документы Microsoft"
description: "Узнайте, как toouse сертификаты с hello пакет интеграции Enterprise | Приложения логики Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="7f062-103">Узнайте о сертификатах и пакете интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="7f062-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="7f062-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="7f062-104">Overview</span></span>
<span data-ttu-id="7f062-105">Интеграция предприятия использует сертификаты toosecure B2B связи.</span><span class="sxs-lookup"><span data-stu-id="7f062-105">Enterprise integration uses certificates toosecure B2B communications.</span></span> <span data-ttu-id="7f062-106">В приложениях интеграции Enterprise можно использовать два типа сертификатов.</span><span class="sxs-lookup"><span data-stu-id="7f062-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="7f062-107">Открытые сертификаты, которые необходимо приобрести в центре сертификации (ЦС).</span><span class="sxs-lookup"><span data-stu-id="7f062-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="7f062-108">Закрытые сертификаты, которые можно выдать самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="7f062-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="7f062-109">Эти сертификаты являются иногда ссылка tooas самозаверяющие сертификаты.</span><span class="sxs-lookup"><span data-stu-id="7f062-109">These certificates are sometimes referred tooas self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="7f062-110">Что такое сертификаты?</span><span class="sxs-lookup"><span data-stu-id="7f062-110">What are certificates?</span></span>
<span data-ttu-id="7f062-111">Сертификаты представляют собой цифровые документы, проверьте идентификатор hello участников hello электронного обмена данными и, для защиты электронных связи.</span><span class="sxs-lookup"><span data-stu-id="7f062-111">Certificates are digital documents that verify hello identity of hello participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="7f062-112">Зачем нужны сертификаты?</span><span class="sxs-lookup"><span data-stu-id="7f062-112">Why use certificates?</span></span>
<span data-ttu-id="7f062-113">Иногда обмен данными "бизнес-бизнес" требует конфиденциальности.</span><span class="sxs-lookup"><span data-stu-id="7f062-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="7f062-114">Интеграции предприятия использует сертификаты toosecure этих сообщений двумя способами:</span><span class="sxs-lookup"><span data-stu-id="7f062-114">Enterprise integration uses certificates toosecure these communications in two ways:</span></span>

* <span data-ttu-id="7f062-115">Шифрование содержимого сообщений hello</span><span class="sxs-lookup"><span data-stu-id="7f062-115">By encrypting hello contents of messages</span></span>
* <span data-ttu-id="7f062-116">для добавления цифровых подписей в сообщения.</span><span class="sxs-lookup"><span data-stu-id="7f062-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="7f062-117">Передача общего сертификата</span><span class="sxs-lookup"><span data-stu-id="7f062-117">Upload a public certificate</span></span>

<span data-ttu-id="7f062-118">toouse *открытый сертификат* в приложениях для логики с возможностями B2B, необходимо сначала tooupload hello сертификата в учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="7f062-118">toouse a *public certificate* in your logic apps with B2B capabilities, you first need tooupload hello certificate into your integration account.</span></span>  

<span data-ttu-id="7f062-119">После отправки сертификата будет доступен toohelp обеспечения безопасности сообщений B2B при определении свойств в hello [соглашения](logic-apps-enterprise-integration-agreements.md) созданного вами.</span><span class="sxs-lookup"><span data-stu-id="7f062-119">After you upload a certificate, it's available toohelp you secure your B2B messages when you define their properties in hello [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="7f062-120">Ниже приведены подробные инструкции для передачи открытых сертификатов в вашу учетную запись интеграции, после входа в toohello портал Azure hello:</span><span class="sxs-lookup"><span data-stu-id="7f062-120">Here are hello detailed steps for uploading your public certificates into your integration account after you sign in toohello Azure portal:</span></span>

1. <span data-ttu-id="7f062-121">Выберите **дополнительные службы** и введите **интеграции** в поле поиска hello фильтра.</span><span class="sxs-lookup"><span data-stu-id="7f062-121">Select **More services** and enter **integration** in hello filter search box.</span></span> <span data-ttu-id="7f062-122">Выберите **учетные записи службы интеграции** из списка результатов hello</span><span class="sxs-lookup"><span data-stu-id="7f062-122">Select **Integration Accounts** from hello results list</span></span>     
<span data-ttu-id="7f062-123">![Щелкните "Обзор"](media/logic-apps-enterprise-integration-certificates/overview-1.png).</span><span class="sxs-lookup"><span data-stu-id="7f062-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="7f062-124">Выберите toowhich учетной записи интеграции hello, требуется сертификат tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="7f062-124">Select hello integration account toowhich you want tooadd hello certificate.</span></span>  
![Выбор учетной записи toowhich hello интеграции, требуется сертификат tooadd hello](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="7f062-126">Выберите hello **сертификаты** плитки.</span><span class="sxs-lookup"><span data-stu-id="7f062-126">Select hello **Certificates** tile.</span></span>  
<span data-ttu-id="7f062-127">![Плитка приветствия выберите сертификаты](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="7f062-127">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="7f062-128">В hello **сертификаты** колонки, откроется, выберите hello **добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="7f062-128">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="7f062-129">![Нажмите кнопку Добавить hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="7f062-129">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="7f062-130">Введите **имя** сертификата и hello, а затем выберите тип сертификата как **открытый** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="7f062-130">Enter a **Name** for your certificate, and then select hello certificate type as **public** from hello dropdown.</span></span>  
6. <span data-ttu-id="7f062-131">Значок папки выберите hello hello правой части hello **сертификат** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="7f062-131">Select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="7f062-132">При открытии средства выбора файлов для hello, найдите и выберите файл сертификата hello, что требуется учетной записи интеграции tooyour tooupload.</span><span class="sxs-lookup"><span data-stu-id="7f062-132">When hello file picker opens, find and select hello certificate file that you want tooupload tooyour integration account.</span></span>
7. <span data-ttu-id="7f062-133">Выберите сертификат hello, а затем выберите **ОК** в средство выбора файлов hello.</span><span class="sxs-lookup"><span data-stu-id="7f062-133">Select hello certificate, and then select **OK** in hello file picker.</span></span> <span data-ttu-id="7f062-134">Это проверяет и загружает tooyour интеграции hello сертификата учетной записи.</span><span class="sxs-lookup"><span data-stu-id="7f062-134">This validates and uploads hello certificate tooyour integration account.</span></span>
8. <span data-ttu-id="7f062-135">И, наконец, включите hello **добавить сертификат** колонки, выберите hello **ОК** кнопки.</span><span class="sxs-lookup"><span data-stu-id="7f062-135">Finally, back on hello **Add certificate** blade, select hello **OK** button.</span></span>  
<span data-ttu-id="7f062-136">![Нажмите кнопку OK hello](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="7f062-136">![Select hello OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="7f062-137">Выберите hello **сертификаты** плитки.</span><span class="sxs-lookup"><span data-stu-id="7f062-137">Select hello **Certificates** tile.</span></span> <span data-ttu-id="7f062-138">Вы увидите, что hello добавленный сертификат.</span><span class="sxs-lookup"><span data-stu-id="7f062-138">You should see hello newly added certificate.</span></span>  
<span data-ttu-id="7f062-139">![В разделе hello новый сертификат](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="7f062-139">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="7f062-140">Передача закрытого сертификата</span><span class="sxs-lookup"><span data-stu-id="7f062-140">Upload a private certificate</span></span>

<span data-ttu-id="7f062-141">toouse *закрытый сертификат* в свои приложения логики с возможностями B2B учетной записи интеграции tooyour закрытый сертификат можно отправить с созданием hello следующие шаги</span><span class="sxs-lookup"><span data-stu-id="7f062-141">toouse a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate tooyour integration account by taking hello following steps</span></span>

1. <span data-ttu-id="7f062-142">[Отправка частного хранилища ключей tooKey](../key-vault/key-vault-get-started.md "Дополнительные сведения о хранилище ключей") и предоставить **имя ключа**</span><span class="sxs-lookup"><span data-stu-id="7f062-142">[Upload your private key tooKey Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="7f062-143">Необходимо авторизовать операций tooperform логику приложения в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="7f062-143">You must authorize Logic Apps tooperform operations on Key Vault.</span></span> <span data-ttu-id="7f062-144">Участника-службы приложения логики toohello доступ можно предоставить с помощью hello следующую команду PowerShell:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="7f062-144">You can grant access toohello Logic Apps service principal by using hello following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="7f062-145">После предыдущего шага hello, добавьте учетную запись toointegration закрытый сертификат.</span><span class="sxs-lookup"><span data-stu-id="7f062-145">After you've taken hello previous step, add a private certificate toointegration account.</span></span>

<span data-ttu-id="7f062-146">Подробное описание действий для передачи закрытого сертификатов в вашу учетную запись интеграции, после входа в toohello портал Azure Здравствуйте, следующие:</span><span class="sxs-lookup"><span data-stu-id="7f062-146">Following are hello detailed steps for uploading your private certificates into your integration account after you sign in toohello Azure portal:</span></span>  
 
1. <span data-ttu-id="7f062-147">Выбор учетной записи toowhich hello интеграции tooadd hello сертификат и выберите hello **сертификаты** плитки.</span><span class="sxs-lookup"><span data-stu-id="7f062-147">Select hello integration account toowhich you want tooadd hello certificate and select hello **Certificates** tile.</span></span>  
<span data-ttu-id="7f062-148">![Плитка приветствия выберите сертификаты](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="7f062-148">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="7f062-149">В hello **сертификаты** колонки, откроется, выберите hello **добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="7f062-149">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="7f062-150">![Нажмите кнопку Добавить hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="7f062-150">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="7f062-151">Введите **имя** сертификата и тип сертификата выберите hello как **закрытый** из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="7f062-151">Enter a **Name** for your certificate, and select hello certificate type as **private** from hello dropdown.</span></span>   
4. <span data-ttu-id="7f062-152">Выберите значок папки hello hello правой части hello **сертификат** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="7f062-152">select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="7f062-153">При открытии средства выбора файлов для hello найти hello соответствующий открытый сертификат, который учетной записи tooupload tooyour интеграции.</span><span class="sxs-lookup"><span data-stu-id="7f062-153">When hello file picker opens, find hello corresponding public certificate that you want tooupload tooyour integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="7f062-154">При добавлении сертификата закрытого важно tooadd соответствующий открытый сертификат tooshow в [соглашение AS2](logic-apps-enterprise-integration-as2.md) параметров получения и отправки для подписания и шифрования сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="7f062-154">While adding a private certificate it is important tooadd corresponding public certificate tooshow in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting hello messages.</span></span>
   > 
   >   

5. <span data-ttu-id="7f062-155">Выберите hello **группы ресурсов**, **хранилище ключей**, **имя ключа** и выберите hello **ОК** кнопки.</span><span class="sxs-lookup"><span data-stu-id="7f062-155">Select hello **Resource Group**, **Key Vault**, **Key Name** and select hello **OK** button.</span></span>  
<span data-ttu-id="7f062-156">![Добавьте сертификат](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png).</span><span class="sxs-lookup"><span data-stu-id="7f062-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="7f062-157">Выберите hello **сертификаты** плитки.</span><span class="sxs-lookup"><span data-stu-id="7f062-157">Select hello **Certificates** tile.</span></span> <span data-ttu-id="7f062-158">Вы увидите, что hello добавленный сертификат.</span><span class="sxs-lookup"><span data-stu-id="7f062-158">You should see hello newly added certificate.</span></span>
<span data-ttu-id="7f062-159">![В разделе hello новый сертификат](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="7f062-159">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="7f062-160">Создание соглашения "бизнес-бизнес"</span><span class="sxs-lookup"><span data-stu-id="7f062-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="7f062-161">Узнайте больше о хранилище ключей Azure</span><span class="sxs-lookup"><span data-stu-id="7f062-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "Сведения о хранилище ключей")  

