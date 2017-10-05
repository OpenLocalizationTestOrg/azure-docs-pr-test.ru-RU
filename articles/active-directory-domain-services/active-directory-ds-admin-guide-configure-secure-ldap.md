---
title: "Настройка защищенного протокола LDAP (LDAPS) в доменных службах Azure AD | Документация Майкрософт"
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
ms.openlocfilehash: 93afa49166c5b31d23237c308b9d34f6d6f3507d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="86dc0-103">Настройка защищенного протокола LDAP (LDAPS) для управляемого домена доменных служб Azure AD</span><span class="sxs-lookup"><span data-stu-id="86dc0-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="86dc0-104">В этой статье показано, как включить протокол LDAPS для управляемого домена доменных служб Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86dc0-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="86dc0-105">Защищенный протокол LDAP также называется "LDAP через SSL или TLS".</span><span class="sxs-lookup"><span data-stu-id="86dc0-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="86dc0-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="86dc0-106">Before you begin</span></span>
<span data-ttu-id="86dc0-107">Чтобы выполнить задачи, описанные в этой статье, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="86dc0-107">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="86dc0-108">Действующая **подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="86dc0-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="86dc0-109">**Каталог Azure AD** — синхронизированный с локальным каталогом или каталогом только для облака.</span><span class="sxs-lookup"><span data-stu-id="86dc0-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="86dc0-110">**Доменные службы Azure AD** должны быть включены для каталога Azure AD.</span><span class="sxs-lookup"><span data-stu-id="86dc0-110">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="86dc0-111">Если это еще не сделано, выполните все задачи, описанные в [руководстве по началу работы](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="86dc0-111">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="86dc0-112">**Сертификат, используемый для включения защищенного протокола LDAP**.</span><span class="sxs-lookup"><span data-stu-id="86dc0-112">A **certificate to be used to enable secure LDAP**.</span></span>

   * <span data-ttu-id="86dc0-113">**Рекомендуется** получить сертификат из доверенного общедоступного центра сертификации.</span><span class="sxs-lookup"><span data-stu-id="86dc0-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="86dc0-114">Этот параметр конфигурации обеспечивает повышенную безопасность.</span><span class="sxs-lookup"><span data-stu-id="86dc0-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="86dc0-115">Кроме того, можно также [создать самозаверяющий сертификат](#task-1---obtain-a-certificate-for-secure-ldap) , как показано далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="86dc0-115">Alternately, you may also choose to [create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-the-secure-ldap-certificate"></a><span data-ttu-id="86dc0-116">Требования к сертификату защищенного протокола LDAP</span><span class="sxs-lookup"><span data-stu-id="86dc0-116">Requirements for the secure LDAP certificate</span></span>
<span data-ttu-id="86dc0-117">Прежде чем включить защищенный протокол LDAP, необходимо получить допустимый сертификат согласно приведенным ниже указаниям.</span><span class="sxs-lookup"><span data-stu-id="86dc0-117">Acquire a valid certificate per the following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="86dc0-118">Попытка включить защищенный протокол LDAP для управляемого домена, используя недопустимый или неправильный сертификат, приведет к сбоям.</span><span class="sxs-lookup"><span data-stu-id="86dc0-118">You encounter failures if you try to enable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="86dc0-119">**Надежный издатель**. Сертификат должен быть выдан центром сертификации, являющимся доверенным для компьютеров, подключающихся к управляемому домену по защищенному протоколу LDAP.</span><span class="sxs-lookup"><span data-stu-id="86dc0-119">**Trusted issuer** - The certificate must be issued by an authority trusted by computers connecting to the managed domain using secure LDAP.</span></span> <span data-ttu-id="86dc0-120">Это может быть общедоступный центр сертификации, который является доверенным для этих компьютеров.</span><span class="sxs-lookup"><span data-stu-id="86dc0-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="86dc0-121">**Срок действия**. Сертификат должен быть допустимым в течение по крайней мере следующих 3–6 месяцев.</span><span class="sxs-lookup"><span data-stu-id="86dc0-121">**Lifetime** - The certificate must be valid for at least the next 3-6 months.</span></span> <span data-ttu-id="86dc0-122">Защищенный доступ LDAP к управляемому домену не будет прерван после истечения срока действия сертификата.</span><span class="sxs-lookup"><span data-stu-id="86dc0-122">Secure LDAP access to your managed domain is disrupted when the certificate expires.</span></span>
3. <span data-ttu-id="86dc0-123">**Имя субъекта**. Имя субъекта сертификата должно состоять из имени управляемого домена и подстановочного знака.</span><span class="sxs-lookup"><span data-stu-id="86dc0-123">**Subject name** - The subject name on the certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="86dc0-124">Например, если имя вашего домена — contoso100.com, то имя субъекта сертификата должно быть *.contoso100.com.</span><span class="sxs-lookup"><span data-stu-id="86dc0-124">For instance, if your domain is named 'contoso100.com', the certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="86dc0-125">Задайте имя с подстановочными знаками в качестве DNS-имени (альтернативного имени субъекта).</span><span class="sxs-lookup"><span data-stu-id="86dc0-125">Set the DNS name (subject alternate name) to this wildcard name.</span></span>
4. <span data-ttu-id="86dc0-126">**Использование ключа**. Сертификат необходимо настроить для создания цифровых подписей и шифрования ключей.</span><span class="sxs-lookup"><span data-stu-id="86dc0-126">**Key usage** - The certificate must be configured for the following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="86dc0-127">**Назначение сертификата**. Сертификат должен быть допустимым для аутентификации на сервере SSL.</span><span class="sxs-lookup"><span data-stu-id="86dc0-127">**Certificate purpose** - The certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="86dc0-128">**Центры сертификации предприятия**. Доменные службы Azure AD не поддерживают использование сертификатов защищенного протокола LDAP, выдающихся центром сертификации предприятия.</span><span class="sxs-lookup"><span data-stu-id="86dc0-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="86dc0-129">Это ограничение объясняется тем, что служба не воспринимает центр сертификации предприятия как доверенный корневой центр сертификации.</span><span class="sxs-lookup"><span data-stu-id="86dc0-129">This restriction is because the service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="86dc0-130">Задача 1. Получение сертификата для защищенного протокола LDAP</span><span class="sxs-lookup"><span data-stu-id="86dc0-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="86dc0-131">Первая задача предполагает получение сертификата, который будет использоваться для защищенного доступа LDAP к управляемому домену.</span><span class="sxs-lookup"><span data-stu-id="86dc0-131">The first task involves obtaining a certificate used for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="86dc0-132">Существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="86dc0-132">You have two options:</span></span>

* <span data-ttu-id="86dc0-133">Получите сертификат в центре сертификации.</span><span class="sxs-lookup"><span data-stu-id="86dc0-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="86dc0-134">Это может быть общедоступный центр сертификации.</span><span class="sxs-lookup"><span data-stu-id="86dc0-134">The authority may be a public certification authority.</span></span>
* <span data-ttu-id="86dc0-135">Создать самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="86dc0-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="86dc0-136">Вариант А (рекомендуется). Получение сертификата защищенного протокола LDAP из центра сертификации</span><span class="sxs-lookup"><span data-stu-id="86dc0-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="86dc0-137">Если ваша организация получает свои сертификаты из общедоступного центра сертификации, то необходимо получить сертификат защищенного протокола LDAP из этого ЦС.</span><span class="sxs-lookup"><span data-stu-id="86dc0-137">If your organization obtains its certificates from a public certification authority, you need to obtain the secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="86dc0-138">При запросе сертификата должны быть выполнены все требования, описанные в разделе [Требования к сертификату защищенного протокола LDAP](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="86dc0-138">When requesting a certificate, ensure that you satisfy all the requirements outlined in [Requirements for the secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="86dc0-139">Клиентские компьютеры, которым требуется подключение к управляемому домену по защищенному протоколу LDAP, должны доверять издателю сертификата защищенного протокола LDAP.</span><span class="sxs-lookup"><span data-stu-id="86dc0-139">Client computers that need to connect to the managed domain using secure LDAP must trust the issuer of the secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="86dc0-140">Вариант Б. Создание самозаверяющего сертификата для защищенного протокола LDAP</span><span class="sxs-lookup"><span data-stu-id="86dc0-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="86dc0-141">Если вы не планируете использовать сертификат из общедоступного центра сертификации, то вы можете создать самозаверяющий сертификат для защищенного протокола LDAP.</span><span class="sxs-lookup"><span data-stu-id="86dc0-141">If you do not expect to use a certificate from a public certification authority, you may choose to create a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="86dc0-142">**Создание самозаверяющего сертификата с использованием PowerShell**</span><span class="sxs-lookup"><span data-stu-id="86dc0-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="86dc0-143">Чтобы создать самозаверяющий сертификат, на компьютере Windows откройте новое окно PowerShell с правами **администратора** и введите следующие команды.</span><span class="sxs-lookup"><span data-stu-id="86dc0-143">On your Windows computer, open a new PowerShell window as **Administrator** and type the following commands, to create a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="86dc0-144">В примере выше замените *.contoso100.com на DNS-имя своего управляемого домена. Например, если вы создали управляемый домен contoso100.onmicrosoft.com, замените* .contoso100.com в приведенном выше скрипте на *.contoso100.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="86dc0-144">In the preceding sample, replace '*.contoso100.com' with the DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in the above script with '*.contoso100.onmicrosoft.com').</span></span>

![Выбор каталога Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="86dc0-146">Созданный самозаверяющий сертификат помещается в хранилище сертификатов на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="86dc0-146">The newly created self-signed certificate is placed in the local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="86dc0-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="86dc0-147">Next step</span></span>
[<span data-ttu-id="86dc0-148">Задача 2. Экспорт сертификата защищенного протокола LDAP в PFX-файл</span><span class="sxs-lookup"><span data-stu-id="86dc0-148">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
