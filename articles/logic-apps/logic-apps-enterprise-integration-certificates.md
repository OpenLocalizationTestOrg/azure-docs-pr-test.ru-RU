---
title: "<span data-ttu-id=\"928f4-101\">Использование сертификатов с помощью Пакета интеграции Enterprise | Документация Майкрософт</span><span class=\"sxs-lookup\"><span data-stu-id=\"928f4-101\">Using certificates with Enterprise Integration Pack | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"928f4-102\">Узнайте, как использовать сертификаты с пакетом интеграции Enterprise | Azure Logic Apps</span><span class=\"sxs-lookup\"><span data-stu-id=\"928f4-102\">Learn how to use certificates with the Enterprise Integration Pack | Azure Logic Apps</span></span>"
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
ms.openlocfilehash: 0570aab14283b38f9efcc50636f0c0c1c8e3ed13
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="928f4-103">Узнайте о сертификатах и пакете интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="928f4-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="928f4-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="928f4-104">Overview</span></span>
<span data-ttu-id="928f4-105">В интеграции Enterprise сертификаты используются для защиты обмена данными "бизнес-бизнес".</span><span class="sxs-lookup"><span data-stu-id="928f4-105">Enterprise integration uses certificates to secure B2B communications.</span></span> <span data-ttu-id="928f4-106">В приложениях интеграции Enterprise можно использовать два типа сертификатов.</span><span class="sxs-lookup"><span data-stu-id="928f4-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="928f4-107">Открытые сертификаты, которые необходимо приобрести в центре сертификации (ЦС).</span><span class="sxs-lookup"><span data-stu-id="928f4-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="928f4-108">Закрытые сертификаты, которые можно выдать самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="928f4-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="928f4-109">Эти сертификаты иногда называются самозаверяющими сертификатами.</span><span class="sxs-lookup"><span data-stu-id="928f4-109">These certificates are sometimes referred to as self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="928f4-110">Что такое сертификаты?</span><span class="sxs-lookup"><span data-stu-id="928f4-110">What are certificates?</span></span>
<span data-ttu-id="928f4-111">Сертификаты представляют собой цифровые документы, используемые для проверки подлинности участников обмена электронными данными и защиты этих операций.</span><span class="sxs-lookup"><span data-stu-id="928f4-111">Certificates are digital documents that verify the identity of the participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="928f4-112">Зачем нужны сертификаты?</span><span class="sxs-lookup"><span data-stu-id="928f4-112">Why use certificates?</span></span>
<span data-ttu-id="928f4-113">Иногда обмен данными "бизнес-бизнес" требует конфиденциальности.</span><span class="sxs-lookup"><span data-stu-id="928f4-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="928f4-114">В интеграции Enterprise сертификаты используются для защиты обмена данными двумя способами:</span><span class="sxs-lookup"><span data-stu-id="928f4-114">Enterprise integration uses certificates to secure these communications in two ways:</span></span>

* <span data-ttu-id="928f4-115">для шифрования содержимого сообщений;</span><span class="sxs-lookup"><span data-stu-id="928f4-115">By encrypting the contents of messages</span></span>
* <span data-ttu-id="928f4-116">для добавления цифровых подписей в сообщения.</span><span class="sxs-lookup"><span data-stu-id="928f4-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="928f4-117">Передача общего сертификата</span><span class="sxs-lookup"><span data-stu-id="928f4-117">Upload a public certificate</span></span>

<span data-ttu-id="928f4-118">Чтобы использовать *открытый сертификат* в приложениях логики с возможностями "бизнес-бизнес", необходимо сначала передать его в учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="928f4-118">To use a *public certificate* in your logic apps with B2B capabilities, you first need to upload the certificate into your integration account.</span></span>  

<span data-ttu-id="928f4-119">После передачи сертификат можно будет использовать для защиты сообщений "бизнес-бизнес" при определении их свойств в создаваемых [соглашениях](logic-apps-enterprise-integration-agreements.md) .</span><span class="sxs-lookup"><span data-stu-id="928f4-119">After you upload a certificate, it's available to help you secure your B2B messages when you define their properties in the [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="928f4-120">Ниже приведены подробные инструкции по передаче открытых сертификатов в учетную запись интеграции после входа на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="928f4-120">Here are the detailed steps for uploading your public certificates into your integration account after you sign in to the Azure portal:</span></span>

1. <span data-ttu-id="928f4-121">Выберите **Больше служб** и в поле фильтра поиска введите **интеграции**.</span><span class="sxs-lookup"><span data-stu-id="928f4-121">Select **More services** and enter **integration** in the filter search box.</span></span> <span data-ttu-id="928f4-122">В списке результатов выберите **Учетные записи интеграции**.</span><span class="sxs-lookup"><span data-stu-id="928f4-122">Select **Integration Accounts** from the results list</span></span>     
<span data-ttu-id="928f4-123">![Щелкните "Обзор"](media/logic-apps-enterprise-integration-certificates/overview-1.png).</span><span class="sxs-lookup"><span data-stu-id="928f4-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="928f4-124">Выберите учетную запись интеграции, в которую необходимо добавить сертификат.</span><span class="sxs-lookup"><span data-stu-id="928f4-124">Select the integration account to which you want to add the certificate.</span></span>  
![Выберите учетную запись интеграции, в которую необходимо добавить сертификат.](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="928f4-126">Выберите элемент **Сертификаты** .</span><span class="sxs-lookup"><span data-stu-id="928f4-126">Select the **Certificates** tile.</span></span>  
<span data-ttu-id="928f4-127">![Выберите элемент "Сертификаты".](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="928f4-127">![Select the Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="928f4-128">В открывшейся колонке **Сертификаты** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="928f4-128">In the **Certificates** blade that opens, select the **Add** button.</span></span>   
<span data-ttu-id="928f4-129">![Нажмите кнопку "Добавить".](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="928f4-129">![Select the Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="928f4-130">Введите **имя** своего сертификата, а затем в раскрывающемся списке выберите тип **общий**.</span><span class="sxs-lookup"><span data-stu-id="928f4-130">Enter a **Name** for your certificate, and then select the certificate type as **public** from the dropdown.</span></span>  
6. <span data-ttu-id="928f4-131">Выберите значок папки справа от текстового поля **Сертификат**.</span><span class="sxs-lookup"><span data-stu-id="928f4-131">Select the folder icon on the right side of the **Certificate** text box.</span></span> <span data-ttu-id="928f4-132">Когда откроется средство выбора файлов, найдите и выберите файл сертификата, который следует передать в учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="928f4-132">When the file picker opens, find and select the certificate file that you want to upload to your integration account.</span></span>
7. <span data-ttu-id="928f4-133">Выберите этот сертификат и нажмите кнопку **ОК** в средстве выбора файлов.</span><span class="sxs-lookup"><span data-stu-id="928f4-133">Select the certificate, and then select **OK** in the file picker.</span></span> <span data-ttu-id="928f4-134">Сертификат будет проверен и передан в учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="928f4-134">This validates and uploads the certificate to your integration account.</span></span>
8. <span data-ttu-id="928f4-135">Наконец, в колонке **Добавление сертификата** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="928f4-135">Finally, back on the **Add certificate** blade, select the **OK** button.</span></span>  
<span data-ttu-id="928f4-136">![Нажмите кнопку "ОК"](media/logic-apps-enterprise-integration-certificates/certificate-3.png).</span><span class="sxs-lookup"><span data-stu-id="928f4-136">![Select the OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="928f4-137">Выберите элемент **Сертификаты** .</span><span class="sxs-lookup"><span data-stu-id="928f4-137">Select the **Certificates** tile.</span></span> <span data-ttu-id="928f4-138">Вы увидите только что добавленный сертификат.</span><span class="sxs-lookup"><span data-stu-id="928f4-138">You should see the newly added certificate.</span></span>  
<span data-ttu-id="928f4-139">![Просмотрите новый сертификат.](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="928f4-139">![See the new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="928f4-140">Передача закрытого сертификата</span><span class="sxs-lookup"><span data-stu-id="928f4-140">Upload a private certificate</span></span>

<span data-ttu-id="928f4-141">Чтобы использовать *закрытый сертификат* в приложениях логики с использованием возможностей B2B, можно загрузить закрытый сертификат в учетную запись интеграции, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="928f4-141">To use a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate to your integration account by taking the following steps</span></span>

1. <span data-ttu-id="928f4-142">[Передайте закрытый ключ в Key Vault](../key-vault/key-vault-get-started.md "Сведения о Key Vault") и введите **имя ключа**.</span><span class="sxs-lookup"><span data-stu-id="928f4-142">[Upload your private key to Key Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="928f4-143">Logic Apps необходимо авторизовать для выполнения операций в Key Vault.</span><span class="sxs-lookup"><span data-stu-id="928f4-143">You must authorize Logic Apps to perform operations on Key Vault.</span></span> <span data-ttu-id="928f4-144">Субъекту-службе Logic Apps можно предоставить доступ с помощью следующей команды PowerShell: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="928f4-144">You can grant access to the Logic Apps service principal by using the following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="928f4-145">После выполнения описанного выше действия добавьте закрытый сертификат в учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="928f4-145">After you've taken the previous step, add a private certificate to integration account.</span></span>

<span data-ttu-id="928f4-146">Ниже приведены подробные инструкции по передаче закрытых сертификатов в учетную запись интеграции после входа на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="928f4-146">Following are the detailed steps for uploading your private certificates into your integration account after you sign in to the Azure portal:</span></span>  
 
1. <span data-ttu-id="928f4-147">Выберите учетную запись интеграции, в которую необходимо добавить сертификат, и выберите элемент **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="928f4-147">Select the integration account to which you want to add the certificate and select the **Certificates** tile.</span></span>  
<span data-ttu-id="928f4-148">![Выберите элемент "Сертификаты".](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="928f4-148">![Select the Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="928f4-149">В открывшейся колонке **Сертификаты** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="928f4-149">In the **Certificates** blade that opens, select the **Add** button.</span></span>   
<span data-ttu-id="928f4-150">![Нажмите кнопку "Добавить".](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="928f4-150">![Select the Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="928f4-151">Введите **имя** своего сертификата, а затем в раскрывающемся списке выберите тип **закрытый**.</span><span class="sxs-lookup"><span data-stu-id="928f4-151">Enter a **Name** for your certificate, and select the certificate type as **private** from the dropdown.</span></span>   
4. <span data-ttu-id="928f4-152">Выберите значок папки справа от текстового поля **Сертификат**.</span><span class="sxs-lookup"><span data-stu-id="928f4-152">select the folder icon on the right side of the **Certificate** text box.</span></span> <span data-ttu-id="928f4-153">Когда откроется средство выбора файлов, найдите общий сертификат, который необходимо передать в учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="928f4-153">When the file picker opens, find the corresponding public certificate that you want to upload to your integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="928f4-154">При добавлении закрытого сертификата важно добавить соответствующий общий сертификат для отображения в параметрах получения и отправки [соглашения AS2](logic-apps-enterprise-integration-as2.md) для подписания и шифрования сообщений.</span><span class="sxs-lookup"><span data-stu-id="928f4-154">While adding a private certificate it is important to add corresponding public certificate to show in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting the messages.</span></span>
   > 
   >   

5. <span data-ttu-id="928f4-155">Последовательно выберите пункты **Группа ресурсов**, **Хранилище ключей**, **Имя ключа** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="928f4-155">Select the **Resource Group**, **Key Vault**, **Key Name** and select the **OK** button.</span></span>  
<span data-ttu-id="928f4-156">![Добавьте сертификат](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png).</span><span class="sxs-lookup"><span data-stu-id="928f4-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="928f4-157">Выберите элемент **Сертификаты** .</span><span class="sxs-lookup"><span data-stu-id="928f4-157">Select the **Certificates** tile.</span></span> <span data-ttu-id="928f4-158">Вы увидите только что добавленный сертификат.</span><span class="sxs-lookup"><span data-stu-id="928f4-158">You should see the newly added certificate.</span></span>
<span data-ttu-id="928f4-159">![Просмотрите новый сертификат.](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="928f4-159">![See the new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="928f4-160">Создание соглашения "бизнес-бизнес"</span><span class="sxs-lookup"><span data-stu-id="928f4-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="928f4-161">Узнайте больше о хранилище ключей Azure</span><span class="sxs-lookup"><span data-stu-id="928f4-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "Сведения о хранилище ключей")  

