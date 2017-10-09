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
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="907a2-103">Настройка защищенного протокола LDAP (LDAPS) для управляемого домена доменных служб Azure AD</span><span class="sxs-lookup"><span data-stu-id="907a2-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="907a2-104">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="907a2-104">Before you begin</span></span>
<span data-ttu-id="907a2-105">Убедитесь в завершении [задача 2 - сертификат tooa экспорта hello безопасный LDAP. PFX-файла](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="907a2-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="907a2-106">Выберите toouse hello preview взаимодействие с портала Azure или hello Azure классического портала toocomplete этой задачи.</span><span class="sxs-lookup"><span data-stu-id="907a2-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="907a2-107">**Портал Azure (Предварительная версия)**: [Включить защищенный LDAP, с помощью портала Azure hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="907a2-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="907a2-108">**Классический портал Azure**: [Включить защищенный LDAP, с помощью классического портала Azure hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="907a2-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a><span data-ttu-id="907a2-109">Задача 3 — включить защищенного протокола LDAP для hello управляемого домена с помощью hello портал Azure (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="907a2-109">Task 3 - enable secure LDAP for hello managed domain using hello Azure portal (Preview)</span></span>
<span data-ttu-id="907a2-110">tooenable безопасной LDAP, выполните следующие действия по настройке hello.</span><span class="sxs-lookup"><span data-stu-id="907a2-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="907a2-111">Перейдите toohello  **[портал Azure](https://portal.azure.com)**.</span><span class="sxs-lookup"><span data-stu-id="907a2-111">Navigate toohello **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="907a2-112">Поиск «доменных служб» hello **Найдите ресурсы** поле поиска.</span><span class="sxs-lookup"><span data-stu-id="907a2-112">Search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="907a2-113">Выберите **доменные службы Azure AD** из результатов поиска hello.</span><span class="sxs-lookup"><span data-stu-id="907a2-113">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="907a2-114">Hello **доменные службы Azure AD** колонке перечислены управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="907a2-114">hello **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![Поиск подготавливаемого управляемого домена](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="907a2-116">Щелкните имя hello toosee hello управляемого домена (например, «contoso100.com») Дополнительные сведения о домене hello.</span><span class="sxs-lookup"><span data-stu-id="907a2-116">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Доменные службы — состояние подготовки](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="907a2-118">Нажмите кнопку **Secure LDAP** на панели навигации hello.</span><span class="sxs-lookup"><span data-stu-id="907a2-118">Click **Secure LDAP** on hello navigation pane.</span></span>

    ![Доменные службы — колонка "Защищенный протокол LDAP"](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="907a2-120">Безопасный доступ tooyour управляемого домена LDAP отключена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="907a2-120">By default, secure LDAP access tooyour managed domain is disabled.</span></span> <span data-ttu-id="907a2-121">Переключить **Secure LDAP** слишком**включить**.</span><span class="sxs-lookup"><span data-stu-id="907a2-121">Toggle **Secure LDAP** too**Enable**.</span></span>

    ![Включение защищенного протокола LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="907a2-123">По умолчанию безопасного tooyour доступа LDAP управляемого домена через Интернет отключен hello.</span><span class="sxs-lookup"><span data-stu-id="907a2-123">By default, secure LDAP access tooyour managed domain over hello internet is disabled.</span></span> <span data-ttu-id="907a2-124">Переключить **Здравствуйте, разрешить защищенный доступ LDAP через Интернет** слишком**включить**при необходимости.</span><span class="sxs-lookup"><span data-stu-id="907a2-124">Toggle **Allow secure LDAP access over hello internet** too**Enable**, if desired.</span></span> 

6. <span data-ttu-id="907a2-125">Нажмите значок следующих hello папку **. PFX-файл с сертификатом безопасности LDAP**.</span><span class="sxs-lookup"><span data-stu-id="907a2-125">Click hello folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="907a2-126">Укажите путь toohello hello PFX-файл с сертификатом hello для безопасного доступа toohello управляемого домена LDAP.</span><span class="sxs-lookup"><span data-stu-id="907a2-126">Specify hello path toohello PFX file with hello certificate for secure LDAP access toohello managed domain.</span></span>

7. <span data-ttu-id="907a2-127">Укажите hello **toodecrypt пароль. PFX-файла**.</span><span class="sxs-lookup"><span data-stu-id="907a2-127">Specify hello **Password toodecrypt .PFX file**.</span></span> <span data-ttu-id="907a2-128">Укажите hello же пароль, используемый при экспорте сертификата toohello hello PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="907a2-128">Provide hello same password you used when exporting hello certificate toohello PFX file.</span></span>

8. <span data-ttu-id="907a2-129">Закончив, нажмите кнопку hello **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="907a2-129">When you are done, click hello **Save** button.</span></span>

9. <span data-ttu-id="907a2-130">Вы увидите уведомление о том, что защищенного LDAP настроена для hello управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="907a2-130">You see a notification that informs you secure LDAP is being configured for hello managed domain.</span></span> <span data-ttu-id="907a2-131">До завершения этой операции не удается изменить другие параметры для домена hello.</span><span class="sxs-lookup"><span data-stu-id="907a2-131">Until this operation is complete, you cannot modify other settings for hello domain.</span></span>

    ![Настройка защищенного протокола LDAP для hello управляемого домена](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="907a2-133">Занимает около 10 минут too15 tooenable защищенный LDAP для управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="907a2-133">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="907a2-134">Если hello при условии, что безопасный LDAP сертификат не соответствует hello необходимые условия, защищенного LDAP не включен для каталога, и вы увидите сбоя.</span><span class="sxs-lookup"><span data-stu-id="907a2-134">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="907a2-135">Например указано неверное имя домена hello, hello сертификата уже истек, или срок действия скоро истекает.</span><span class="sxs-lookup"><span data-stu-id="907a2-135">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span> <span data-ttu-id="907a2-136">В этом случае повторите попытку, указав действительный сертификат.</span><span class="sxs-lookup"><span data-stu-id="907a2-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="907a2-137">Задача 4 — Настройка управляемого домена DNS tooaccess hello из hello Интернета</span><span class="sxs-lookup"><span data-stu-id="907a2-137">Task 4 - configure DNS tooaccess hello managed domain from hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="907a2-138">**Необязательные задачи** — Если вы не планируете tooaccess hello управляемого домена с помощью LDAPS более Здравствуйте Интернета, пропустить эту задачу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="907a2-138">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="907a2-139">Прежде чем начать эту задачу, убедитесь, выполнен hello действия, описанные в [задача 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="907a2-139">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="907a2-140">После включения защищенный доступ LDAP через Интернет Здравствуйте, управляемого домена, необходимо tooupdate DNS, чтобы клиентские компьютеры могли найти этот управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="907a2-140">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="907a2-141">В конце hello задача 3, внешний IP-адрес отображается на hello **свойства** колонки в **ВНЕШНИЕ IP адрес для доступа через LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="907a2-141">At hello end of task 3, an external IP address is displayed on hello **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="907a2-142">Настройте внешнего поставщика DNS, чтобы DNS-имени hello объекта hello управляемого домена (например, «ldaps.contoso100.com») toothis точек внешний IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="907a2-142">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="907a2-143">В нашем примере мы должны hello toocreate следующие записи DNS.</span><span class="sxs-lookup"><span data-stu-id="907a2-143">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="907a2-144">Вот и все - теперь теперь вы готовы tooconnect toohello управляемых Здравствуйте, домена, с помощью защищенного LDAP через Интернет.</span><span class="sxs-lookup"><span data-stu-id="907a2-144">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="907a2-145">Помните, что клиентские компьютеры должны доверять hello издателя может tooconnect сертификата LDAPS toobe hello успешно toohello управляемого домена при использовании LDAPS.</span><span class="sxs-lookup"><span data-stu-id="907a2-145">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="907a2-146">Если вы используете публично доверенным центром сертификации, необязательно toodo ничего, так как эти издатели сертификатов доверять клиентские компьютеры.</span><span class="sxs-lookup"><span data-stu-id="907a2-146">If you are using a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="907a2-147">Если вы используете самозаверяющий сертификат, установите hello открытую часть hello самозаверяющий сертификат в хранилище доверенных сертификатов hello на клиентском компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="907a2-147">If you are using a self-signed certificate, install hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="907a2-148">Задача 5 - LDAPS блокировки доступа к tooyour управляемого домена через hello Интернета</span><span class="sxs-lookup"><span data-stu-id="907a2-148">Task 5 - lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="907a2-149">**Необязательные задачи** — Если вы не включили LDAPS управляемого домена toohello доступа более Здравствуйте Интернета, пропустить эту задачу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="907a2-149">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="907a2-150">Прежде чем начать эту задачу, убедитесь, выполнен hello действия, описанные в [задача 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="907a2-150">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="907a2-151">Предоставления управляемого домена для доступа LDAPS через hello Интернет представляет угрозу безопасности.</span><span class="sxs-lookup"><span data-stu-id="907a2-151">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="907a2-152">Hello управляемого домена доступен из hello Интернета с hello порт, используемый для защищенного LDAP (то есть, порт 636).</span><span class="sxs-lookup"><span data-stu-id="907a2-152">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="907a2-153">Таким образом вы можете toorestrict доступа toohello управляемого домена toospecific известные IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="907a2-153">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="907a2-154">В целях повышения безопасности создайте группу безопасности сети (NSG) и связать его с hello подсети, где вы включили доменные службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="907a2-154">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="907a2-155">Hello следующей таблице показан пример NSG можно настроить toolock вниз защищенный доступ LDAP через hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="907a2-155">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="907a2-156">Hello NSG содержит набор правил, которые разрешают доступ входящего трафика LDAPS через TCP-порт 636 только из указанного набора IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="907a2-156">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="907a2-157">Hello «DenyAll» правило по умолчанию применяется tooall других входящий трафик от hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="907a2-157">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="907a2-158">Hello доступа LDAPS tooallow правила NSG через hello Интернет с указанных IP-адресов имеет более высокий приоритет, чем правила DenyAll NSG hello.</span><span class="sxs-lookup"><span data-stu-id="907a2-158">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Здравствуйте, образец NSG toosecure LDAPS доступ через Интернет](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="907a2-160">**Дополнительные сведения см. в статье** - [Фильтрация сетевого трафика с помощью групп безопасности сети](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="907a2-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="907a2-161">Связанная информация</span><span class="sxs-lookup"><span data-stu-id="907a2-161">Related content</span></span>
* [<span data-ttu-id="907a2-162">Приступая к работе с доменными службами Azure AD</span><span class="sxs-lookup"><span data-stu-id="907a2-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="907a2-163">Administer an Azure AD Domain Services managed domain (Администрирование управляемого домена доменных служб Azure AD)</span><span class="sxs-lookup"><span data-stu-id="907a2-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* <span data-ttu-id="907a2-164">[Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md) (Администрирование групповой политики в управляемом домене доменных служб Azure AD)</span><span class="sxs-lookup"><span data-stu-id="907a2-164">[Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md)</span></span>
* [<span data-ttu-id="907a2-165">Группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="907a2-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="907a2-166">Создание группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="907a2-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
