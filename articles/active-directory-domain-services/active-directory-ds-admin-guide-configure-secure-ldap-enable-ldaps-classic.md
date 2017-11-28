---
title: "aaaConfigure Secure LDAP (LDAPS) в доменные службы Azure AD | Документы Microsoft"
description: "Настройка защищенного протокола LDAP (LDAPS) для управляемого домена доменных служб Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="1a722-103">Настройка защищенного протокола LDAP (LDAPS) для управляемого домена доменных служб Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a722-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1a722-104">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="1a722-104">Before you begin</span></span>
<span data-ttu-id="1a722-105">Убедитесь в завершении [задача 2 - сертификат tooa экспорта hello безопасный LDAP. PFX-файла](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="1a722-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="1a722-106">Выберите toouse hello preview взаимодействие с портала Azure или hello Azure классического портала toocomplete этой задачи.</span><span class="sxs-lookup"><span data-stu-id="1a722-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="1a722-107">**Портал Azure (Предварительная версия)**: [Включить защищенный LDAP, с помощью портала Azure hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="1a722-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="1a722-108">**Классический портал Azure**: [Включить защищенный LDAP, с помощью классического портала Azure hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="1a722-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a><span data-ttu-id="1a722-109">Задача 3 — включить защищенного протокола LDAP для hello управляемого домена с помощью классического портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="1a722-109">Task 3 - enable secure LDAP for hello managed domain using hello classic Azure portal</span></span>
<span data-ttu-id="1a722-110">tooenable безопасной LDAP, выполните следующие действия по настройке hello.</span><span class="sxs-lookup"><span data-stu-id="1a722-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="1a722-111">Перейдите toohello  **[классический портал Azure](https://manage.windowsazure.com)**.</span><span class="sxs-lookup"><span data-stu-id="1a722-111">Navigate toohello **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="1a722-112">Выберите hello **Active Directory** узел в левой области hello.</span><span class="sxs-lookup"><span data-stu-id="1a722-112">Select hello **Active Directory** node on hello left pane.</span></span>
3. <span data-ttu-id="1a722-113">Выберите каталог hello Azure AD (также назывались tooas «клиент»), для которого включена доменные службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a722-113">Select hello Azure AD directory (also referred tooas 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Выбор каталога Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="1a722-115">Нажмите кнопку hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="1a722-115">Click hello **Configure** tab.</span></span>

    ![Вкладка "Настройка" каталога](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="1a722-117">Прокрутите раздел toohello **доменных служб**.</span><span class="sxs-lookup"><span data-stu-id="1a722-117">Scroll down toohello section titled **domain services**.</span></span> <span data-ttu-id="1a722-118">Вы увидите параметр под названием **Secure LDAP (LDAPS)** как показано на следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="1a722-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in hello following screenshot:</span></span>

    ![Раздел настройки доменных служб](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="1a722-120">Нажмите кнопку hello **настроить сертификат...**  toobring кнопки вверх hello **Настройка сертификата для безопасного LDAP** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="1a722-120">Click hello **Configure certificate ...** button toobring up hello **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![Настройка сертификата для защищенного LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="1a722-122">Нажмите значок следующих hello папку **PFX-ФАЙЛ с СЕРТИФИКАТОМ** toospecify hello PFX файл, содержащий сертификат hello нужно toouse для безопасного toohello доступа LDAP управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="1a722-122">Click hello folder icon following **PFX FILE WITH CERTIFICATE** toospecify hello PFX file, which contains hello certificate you wish toouse for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="1a722-123">Также можно ввести пароль hello, указанные при экспорте сертификата toohello hello PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="1a722-123">Also enter hello password you specified when exporting hello certificate toohello PFX file.</span></span> <span data-ttu-id="1a722-124">Нажмите кнопку сделать кнопку на нижней hello hello.</span><span class="sxs-lookup"><span data-stu-id="1a722-124">Then, click hello done button on hello bottom.</span></span>

    ![Указание PFX-файла и пароля защищенного LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="1a722-126">Hello **доменных служб** раздел hello **Настройка** вкладка должен получить серым и находится в hello **ожидающие...**  за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="1a722-126">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="1a722-127">В течение этого периода hello LDAPS сертификат проверяется для повышения точности и защищенного LDAP настроен для управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="1a722-127">During this period, hello LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![Защищенный LDAP — состояние ожидания](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="1a722-129">Занимает около 10 минут too15 tooenable защищенный LDAP для управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="1a722-129">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="1a722-130">Если hello при условии, что безопасный LDAP сертификат не соответствует hello необходимые условия, защищенного LDAP не включен для каталога, и вы увидите сбоя.</span><span class="sxs-lookup"><span data-stu-id="1a722-130">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="1a722-131">Например указано неверное имя домена hello, hello сертификата уже истек, или срок действия скоро истекает.</span><span class="sxs-lookup"><span data-stu-id="1a722-131">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="1a722-132">Если защищенного LDAP успешно включена для управляемого домена, hello **ожидающие...**  сообщение должно исчезнуть.</span><span class="sxs-lookup"><span data-stu-id="1a722-132">When secure LDAP is successfully enabled for your managed domain, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="1a722-133">Вы увидите hello отпечаток сертификата hello отображается.</span><span class="sxs-lookup"><span data-stu-id="1a722-133">You should see hello thumbprint of hello certificate displayed.</span></span>

    ![Защищенный LDAP включен](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a><span data-ttu-id="1a722-135">Задача 4 — Включить защищенный доступ LDAP через hello Интернета</span><span class="sxs-lookup"><span data-stu-id="1a722-135">Task 4 - enable secure LDAP access over hello internet</span></span>
<span data-ttu-id="1a722-136">**Необязательные задачи** — Если вы не планируете tooaccess hello управляемого домена с помощью LDAPS более Здравствуйте Интернета, пропустить эту задачу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1a722-136">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="1a722-137">Прежде чем начать эту задачу, убедитесь, выполнен hello действия, описанные в [задача 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="1a722-137">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="1a722-138">Вы увидите вариант слишком**hello ВКЛЮЧИТЬ SECURE LDAP доступ через Интернет** в hello **доменных служб** раздел hello **Настройка** страницы.</span><span class="sxs-lookup"><span data-stu-id="1a722-138">You should see an option too**ENABLE SECURE LDAP ACCESS OVER hello INTERNET** in hello **domain services** section of hello **Configure** page.</span></span> <span data-ttu-id="1a722-139">Этот параметр имеет значение слишком**нет** по умолчанию, так как управляемые toohello доступа к Интернету домена через безопасный LDAP по умолчанию отключена.</span><span class="sxs-lookup"><span data-stu-id="1a722-139">This option is set too**NO** by default since internet access toohello managed domain over secure LDAP is disabled by default.</span></span>

    ![Защищенный LDAP включен](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="1a722-141">Переключить **hello ВКЛЮЧИТЬ SECURE LDAP доступ через Интернет** слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="1a722-141">Toggle **ENABLE SECURE LDAP ACCESS OVER hello INTERNET** too**YES**.</span></span> <span data-ttu-id="1a722-142">Нажмите кнопку hello **Сохранить** кнопку на нижней панели hello.</span><span class="sxs-lookup"><span data-stu-id="1a722-142">Click hello **SAVE** button on hello bottom panel.</span></span>
    <span data-ttu-id="1a722-143">![Защищенный LDAP включен](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="1a722-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="1a722-144">Hello **доменных служб** раздел hello **Настройка** вкладка должен получить серым и находится в hello **ожидающие...**  за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="1a722-144">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="1a722-145">Через некоторое время включены internet access tooyour управляемого домена через безопасный LDAP.</span><span class="sxs-lookup"><span data-stu-id="1a722-145">After some time, internet access tooyour managed domain over secure LDAP is enabled.</span></span>

    ![Защищенный LDAP — состояние ожидания](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="1a722-147">Занимает около 10 минут tooenable доступ к Интернету через безопасный LDAP для управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="1a722-147">It takes about 10 minutes tooenable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="1a722-148">При безопасной tooyour доступа LDAP управляемого домена через Интернет успешно включен hello, hello **ожидающие...**  сообщение должно исчезнуть.</span><span class="sxs-lookup"><span data-stu-id="1a722-148">When secure LDAP access tooyour managed domain over hello internet is successfully enabled, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="1a722-149">Вы увидите hello внешний IP-адрес, адрес можно использовать tooaccess каталога через LDAPS в поле hello **ВНЕШНИЕ IP адрес для доступа через LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="1a722-149">You should see hello external IP address that can be used tooaccess your directory over LDAPS in hello field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![Защищенный LDAP включен](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="1a722-151">Задача 5 — Настройка управляемого домена DNS tooaccess hello из hello Интернета</span><span class="sxs-lookup"><span data-stu-id="1a722-151">Task 5 - configure DNS tooaccess hello managed domain from hello internet</span></span>
<span data-ttu-id="1a722-152">**Необязательные задачи** — Если вы не планируете tooaccess hello управляемого домена с помощью LDAPS более Здравствуйте Интернета, пропустить эту задачу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1a722-152">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="1a722-153">Прежде чем начать эту задачу, убедитесь, выполнен hello действия, описанные в [задача 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="1a722-153">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="1a722-154">После включения защищенный доступ LDAP через Интернет Здравствуйте, управляемого домена, необходимо tooupdate DNS, чтобы клиентские компьютеры могли найти этот управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="1a722-154">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="1a722-155">В конце задача 4 hello, внешний IP-адрес отображается на hello **Настройка** вкладке **ВНЕШНИЕ IP адрес для доступа через LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="1a722-155">At hello end of task 4, an external IP address is displayed on hello **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="1a722-156">Настройте внешнего поставщика DNS, чтобы DNS-имени hello объекта hello управляемого домена (например, «ldaps.contoso100.com») toothis точек внешний IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="1a722-156">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="1a722-157">В нашем примере мы должны hello toocreate следующие записи DNS.</span><span class="sxs-lookup"><span data-stu-id="1a722-157">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="1a722-158">Вот и все - теперь теперь вы готовы tooconnect toohello управляемых Здравствуйте, домена, с помощью защищенного LDAP через Интернет.</span><span class="sxs-lookup"><span data-stu-id="1a722-158">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="1a722-159">Помните, что клиентские компьютеры должны доверять hello издателя может tooconnect сертификата LDAPS toobe hello успешно toohello управляемого домена при использовании LDAPS.</span><span class="sxs-lookup"><span data-stu-id="1a722-159">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="1a722-160">Если вы используете центр сертификации предприятия или публично доверенным центром сертификации, необязательно toodo ничего, так как эти издатели сертификатов доверять клиентские компьютеры.</span><span class="sxs-lookup"><span data-stu-id="1a722-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="1a722-161">Если вы используете самозаверяющий сертификат, необходимо tooinstall hello открытую часть hello самозаверяющий сертификат в хранилище доверенных сертификатов hello на клиентском компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="1a722-161">If you are using a self-signed certificate, you need tooinstall hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="1a722-162">LDAPS блокировки доступа к управляемому домену tooyour через hello Интернета</span><span class="sxs-lookup"><span data-stu-id="1a722-162">Lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="1a722-163">**Необязательные задачи** — Если вы не включили LDAPS управляемого домена toohello доступа более Здравствуйте Интернета, пропустить эту задачу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1a722-163">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="1a722-164">Прежде чем начать эту задачу, убедитесь, выполнен hello действия, описанные в [задача 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="1a722-164">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="1a722-165">Предоставления управляемого домена для доступа LDAPS через hello Интернет представляет угрозу безопасности.</span><span class="sxs-lookup"><span data-stu-id="1a722-165">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="1a722-166">Hello управляемого домена доступен из hello Интернета с hello порт, используемый для защищенного LDAP (то есть, порт 636).</span><span class="sxs-lookup"><span data-stu-id="1a722-166">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="1a722-167">Таким образом вы можете toorestrict доступа toohello управляемого домена toospecific известные IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="1a722-167">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="1a722-168">В целях повышения безопасности создайте группу безопасности сети (NSG) и связать его с hello подсети, где вы включили доменные службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a722-168">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="1a722-169">Hello следующей таблице показан пример NSG можно настроить toolock вниз защищенный доступ LDAP через hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="1a722-169">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="1a722-170">Hello NSG содержит набор правил, которые разрешают доступ входящего трафика LDAPS через TCP-порт 636 только из указанного набора IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="1a722-170">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="1a722-171">Hello «DenyAll» правило по умолчанию применяется tooall других входящий трафик от hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="1a722-171">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="1a722-172">Hello доступа LDAPS tooallow правила NSG через hello Интернет с указанных IP-адресов имеет более высокий приоритет, чем правила DenyAll NSG hello.</span><span class="sxs-lookup"><span data-stu-id="1a722-172">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Здравствуйте, образец NSG toosecure LDAPS доступ через Интернет](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="1a722-174">**Дополнительные сведения см. в статье** - [Фильтрация сетевого трафика с помощью групп безопасности сети](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="1a722-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="1a722-175">Связанная информация</span><span class="sxs-lookup"><span data-stu-id="1a722-175">Related content</span></span>
* [<span data-ttu-id="1a722-176">Приступая к работе с доменными службами Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a722-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="1a722-177">Administer an Azure AD Domain Services managed domain (Администрирование управляемого домена доменных служб Azure AD)</span><span class="sxs-lookup"><span data-stu-id="1a722-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* <span data-ttu-id="1a722-178">[Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md) (Администрирование групповой политики в управляемом домене доменных служб Azure AD)</span><span class="sxs-lookup"><span data-stu-id="1a722-178">[Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md)</span></span>
* [<span data-ttu-id="1a722-179">Группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="1a722-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="1a722-180">Создание группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="1a722-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
