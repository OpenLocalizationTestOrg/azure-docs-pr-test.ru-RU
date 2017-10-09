---
title: "aaaConfigure Secure LDAP (LDAPS) в доменные службы Azure AD | Документы Microsoft"
description: "Настройка защищенного протокола LDAP (LDAPS) для управляемого домена доменных служб Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="8a756-103">Настройка защищенного протокола LDAP (LDAPS) для управляемого домена доменных служб Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a756-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="8a756-104">В этой статье показано, как включить протокол LDAPS для управляемого домена доменных служб Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a756-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="8a756-105">Защищенный протокол LDAP также называется "LDAP через SSL или TLS".</span><span class="sxs-lookup"><span data-stu-id="8a756-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8a756-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="8a756-106">Before you begin</span></span>
<span data-ttu-id="8a756-107">tooperform hello задачи, перечисленные в этой статье, необходимо:</span><span class="sxs-lookup"><span data-stu-id="8a756-107">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="8a756-108">Действующая **подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="8a756-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="8a756-109">**Каталог Azure AD** — синхронизированный с локальным каталогом или каталогом только для облака.</span><span class="sxs-lookup"><span data-stu-id="8a756-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="8a756-110">**Доменные службы Azure AD** должна быть включена для каталога hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a756-110">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="8a756-111">Если вы еще не сделали этого, выполните все действия hello hello [руководство по началу работы](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="8a756-111">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="8a756-112">Объект **tooenable toobe используется сертификат защищенный LDAP**.</span><span class="sxs-lookup"><span data-stu-id="8a756-112">A **certificate toobe used tooenable secure LDAP**.</span></span>

   * <span data-ttu-id="8a756-113">**Рекомендуется** получить сертификат из доверенного общедоступного центра сертификации.</span><span class="sxs-lookup"><span data-stu-id="8a756-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="8a756-114">Этот параметр конфигурации обеспечивает повышенную безопасность.</span><span class="sxs-lookup"><span data-stu-id="8a756-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="8a756-115">Кроме того, можно также выбрать слишком[создать самозаверяющий сертификат](#task-1---obtain-a-certificate-for-secure-ldap) как показано далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="8a756-115">Alternately, you may also choose too[create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a><span data-ttu-id="8a756-116">Требования для безопасного LDAP сертификата hello</span><span class="sxs-lookup"><span data-stu-id="8a756-116">Requirements for hello secure LDAP certificate</span></span>
<span data-ttu-id="8a756-117">Получить действительный сертификат на hello инструкциями, прежде чем включать защищенного протокола LDAP.</span><span class="sxs-lookup"><span data-stu-id="8a756-117">Acquire a valid certificate per hello following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="8a756-118">Сбой при попытке tooenable защищенный LDAP для управляемого домена с неправильный или недопустимый сертификат.</span><span class="sxs-lookup"><span data-stu-id="8a756-118">You encounter failures if you try tooenable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="8a756-119">**Надежного издателя** -hello сертификат должен быть выдан центром сертификации, доверенным для компьютеров, подключающихся управляемого домена toohello использование защищенного протокола LDAP.</span><span class="sxs-lookup"><span data-stu-id="8a756-119">**Trusted issuer** - hello certificate must be issued by an authority trusted by computers connecting toohello managed domain using secure LDAP.</span></span> <span data-ttu-id="8a756-120">Это может быть общедоступный центр сертификации, который является доверенным для этих компьютеров.</span><span class="sxs-lookup"><span data-stu-id="8a756-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="8a756-121">**Время существования** -hello сертификат должен быть допустимым для по крайней мере hello следующие 3 – 6 месяцев.</span><span class="sxs-lookup"><span data-stu-id="8a756-121">**Lifetime** - hello certificate must be valid for at least hello next 3-6 months.</span></span> <span data-ttu-id="8a756-122">Срок действия сертификата hello разрыва безопасного доступа tooyour управляемого домена LDAP.</span><span class="sxs-lookup"><span data-stu-id="8a756-122">Secure LDAP access tooyour managed domain is disrupted when hello certificate expires.</span></span>
3. <span data-ttu-id="8a756-123">**Имя субъекта** -hello имя субъекта сертификата hello должно быть подстановочный знак для управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="8a756-123">**Subject name** - hello subject name on hello certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="8a756-124">Для экземпляра, если ваш домен называется «contoso100.com», имя субъекта сертификата hello должен быть "*. contoso100.com".</span><span class="sxs-lookup"><span data-stu-id="8a756-124">For instance, if your domain is named 'contoso100.com', hello certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="8a756-125">Задать toothis hello DNS-имя (альтернативное имя субъекта) имя подстановочный знак.</span><span class="sxs-lookup"><span data-stu-id="8a756-125">Set hello DNS name (subject alternate name) toothis wildcard name.</span></span>
4. <span data-ttu-id="8a756-126">**Использование ключа** - hello необходимо настроить сертификат для использует следующие hello - цифровые подписи и шифрование ключей.</span><span class="sxs-lookup"><span data-stu-id="8a756-126">**Key usage** - hello certificate must be configured for hello following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="8a756-127">**Назначение сертификата** -hello сертификат должен быть допустимым для проверки подлинности сервера SSL.</span><span class="sxs-lookup"><span data-stu-id="8a756-127">**Certificate purpose** - hello certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="8a756-128">**Центры сертификации предприятия**. Доменные службы Azure AD не поддерживают использование сертификатов защищенного протокола LDAP, выдающихся центром сертификации предприятия.</span><span class="sxs-lookup"><span data-stu-id="8a756-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="8a756-129">Это ограничение действует, так как служба hello не доверяет центр сертификации в качестве корневого центра сертификации предприятия.</span><span class="sxs-lookup"><span data-stu-id="8a756-129">This restriction is because hello service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="8a756-130">Задача 1. Получение сертификата для защищенного протокола LDAP</span><span class="sxs-lookup"><span data-stu-id="8a756-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="8a756-131">Первая задача Hello предполагает получение сертификата, используемого для безопасного доступа toohello управляемого домена LDAP.</span><span class="sxs-lookup"><span data-stu-id="8a756-131">hello first task involves obtaining a certificate used for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="8a756-132">Существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="8a756-132">You have two options:</span></span>

* <span data-ttu-id="8a756-133">Получите сертификат в центре сертификации.</span><span class="sxs-lookup"><span data-stu-id="8a756-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="8a756-134">Возможно, центр Hello общедоступным центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="8a756-134">hello authority may be a public certification authority.</span></span>
* <span data-ttu-id="8a756-135">Создать самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="8a756-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="8a756-136">Вариант А (рекомендуется). Получение сертификата защищенного протокола LDAP из центра сертификации</span><span class="sxs-lookup"><span data-stu-id="8a756-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="8a756-137">Если ваша организация получает сертификаты из общедоступного центра сертификации, вам понадобится сертификат hello безопасного tooobtain LDAP из этого общедоступным центром сертификации.</span><span class="sxs-lookup"><span data-stu-id="8a756-137">If your organization obtains its certificates from a public certification authority, you need tooobtain hello secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="8a756-138">При запросе сертификата, убедиться в выполнении всех hello требованиям, приведенным в [требования для безопасного LDAP сертификата hello](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="8a756-138">When requesting a certificate, ensure that you satisfy all hello requirements outlined in [Requirements for hello secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="8a756-139">Клиентские компьютеры, которым требуется управляемый домен tooconnect toohello использование защищенного протокола LDAP должны доверять hello издателя hello безопасный LDAP сертификата.</span><span class="sxs-lookup"><span data-stu-id="8a756-139">Client computers that need tooconnect toohello managed domain using secure LDAP must trust hello issuer of hello secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="8a756-140">Вариант Б. Создание самозаверяющего сертификата для защищенного протокола LDAP</span><span class="sxs-lookup"><span data-stu-id="8a756-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="8a756-141">Если предполагается, что toouse сертификата из общедоступного центра сертификации, вы можете toocreate самозаверяющего сертификата для защищенного LDAP.</span><span class="sxs-lookup"><span data-stu-id="8a756-141">If you do not expect toouse a certificate from a public certification authority, you may choose toocreate a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="8a756-142">**Создание самозаверяющего сертификата с использованием PowerShell**</span><span class="sxs-lookup"><span data-stu-id="8a756-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="8a756-143">На компьютере Windows, откройте окно PowerShell от **администратора** и типа hello следующие команды, toocreate новый самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="8a756-143">On your Windows computer, open a new PowerShell window as **Administrator** and type hello following commands, toocreate a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="8a756-144">В предыдущих образец hello, замените "*. contoso100.com" hello DNS-имени домена управляемого домена. Например, при создании управляемого домена с именем «contoso100.onmicrosoft.com» заменить "*. contoso100.com" в hello выше скрипт с "*. contoso100.onmicrosoft.com").</span><span class="sxs-lookup"><span data-stu-id="8a756-144">In hello preceding sample, replace '*.contoso100.com' with hello DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in hello above script with '*.contoso100.onmicrosoft.com').</span></span>

![Выбор каталога Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="8a756-146">самозаверяющий сертификат только что созданный Hello помещается в хранилище сертификатов локального компьютера hello.</span><span class="sxs-lookup"><span data-stu-id="8a756-146">hello newly created self-signed certificate is placed in hello local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="8a756-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8a756-147">Next step</span></span>
[<span data-ttu-id="8a756-148">Задача 2 - сертификат tooa экспорта hello безопасный LDAP. PFX-файла</span><span class="sxs-lookup"><span data-stu-id="8a756-148">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
