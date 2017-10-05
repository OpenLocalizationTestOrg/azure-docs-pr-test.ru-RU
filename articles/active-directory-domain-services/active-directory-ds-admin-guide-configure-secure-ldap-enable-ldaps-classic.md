---
title: "Настройка защищенного протокола LDAP (LDAPS) в доменных службах Azure AD | Документация Майкрософт"
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
ms.openlocfilehash: 3aafe209aad7383cd0610d147b5fdba673023c93
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="f661b-103">Настройка защищенного протокола LDAP (LDAPS) для управляемого домена доменных служб Azure AD</span><span class="sxs-lookup"><span data-stu-id="f661b-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f661b-104">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="f661b-104">Before you begin</span></span>
<span data-ttu-id="f661b-105">Убедитесь, что вы выполнили [Задачу 2. Экспорт сертификата защищенного протокола LDAP в PFX-файл](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="f661b-105">Ensure you've completed [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="f661b-106">Выберите предварительную версию портала Azure или классический портал Azure для выполнения этой задачи.</span><span class="sxs-lookup"><span data-stu-id="f661b-106">Choose whether to use the preview Azure portal experience or the Azure classic portal to complete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="f661b-107">**Портал Azure (предварительная версия)**: [Включение защищенного протокола LDAP с помощью портала Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="f661b-107">**Azure portal (Preview)**: [Enable secure LDAP using the Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="f661b-108">**Классический портал Azure**: [Включение защищенного протокола LDAP с помощью классического портала Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="f661b-108">**Azure classic portal**: [Enable secure LDAP using the classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal"></a><span data-ttu-id="f661b-109">Задача 3. Включение защищенного протокола LDAP для управляемого домена с помощью классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="f661b-109">Task 3 - enable secure LDAP for the managed domain using the classic Azure portal</span></span>
<span data-ttu-id="f661b-110">Выполните следующие действия по настройке, чтобы включить защищенный протокол LDAP.</span><span class="sxs-lookup"><span data-stu-id="f661b-110">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="f661b-111">Перейдите на **[классический портал Azure](https://manage.windowsazure.com)**.</span><span class="sxs-lookup"><span data-stu-id="f661b-111">Navigate to the **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="f661b-112">На панели слева выберите **Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="f661b-112">Select the **Active Directory** node on the left pane.</span></span>
3. <span data-ttu-id="f661b-113">Выберите каталог Azure AD (также называемый клиентом), для которого включены доменные службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f661b-113">Select the Azure AD directory (also referred to as 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Выбор каталога Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="f661b-115">Выберите вкладку **Настройка** .</span><span class="sxs-lookup"><span data-stu-id="f661b-115">Click the **Configure** tab.</span></span>

    ![Вкладка "Настройка" каталога](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="f661b-117">Прокрутите страницу вниз до раздела **Доменные службы**.</span><span class="sxs-lookup"><span data-stu-id="f661b-117">Scroll down to the section titled **domain services**.</span></span> <span data-ttu-id="f661b-118">Вы увидите параметр **Защищенный LDAP (LDAPS)** , как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="f661b-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in the following screenshot:</span></span>

    ![Раздел настройки доменных служб](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="f661b-120">Нажмите кнопку **Настроить сертификат…**, чтобы открыть диалоговое окно **Настройка сертификата для защищенного LDAP**.</span><span class="sxs-lookup"><span data-stu-id="f661b-120">Click the **Configure certificate ...** button to bring up the **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![Настройка сертификата для защищенного LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="f661b-122">Щелкните значок папки возле параметра **PFX-ФАЙЛ С СЕРТИФИКАТОМ**, чтобы указать PFX-файл, содержащий сертификат, который необходимо использовать для защищенного доступа LDAP к управляемому домену.</span><span class="sxs-lookup"><span data-stu-id="f661b-122">Click the folder icon following **PFX FILE WITH CERTIFICATE** to specify the PFX file, which contains the certificate you wish to use for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="f661b-123">Затем введите пароль, который вы указали при экспорте сертификата в PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="f661b-123">Also enter the password you specified when exporting the certificate to the PFX file.</span></span> <span data-ttu-id="f661b-124">Затем нажмите кнопку "Готово" внизу.</span><span class="sxs-lookup"><span data-stu-id="f661b-124">Then, click the done button on the bottom.</span></span>

    ![Указание PFX-файла и пароля защищенного LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="f661b-126">Раздел **Доменные службы** на вкладке **Настройка** должен стать неактивным и перейти в состояние **Ожидание…** на несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f661b-126">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="f661b-127">В течение этого периода проверяется точность сертификата LDAPS и настраивается защищенный протокол LDAP для управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="f661b-127">During this period, the LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![Защищенный LDAP — состояние ожидания](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="f661b-129">Включение защищенного LDAP для управляемого домена займет примерно 10–15 минут.</span><span class="sxs-lookup"><span data-stu-id="f661b-129">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="f661b-130">Если предоставленный защищенный сертификат LDAP не соответствует необходимым требованиям, то защищенный протокол LDAP не будет включен для каталога и произойдет ошибка.</span><span class="sxs-lookup"><span data-stu-id="f661b-130">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="f661b-131">Например, отобразится сообщение о том, что указано неправильное доменное имя, срок действия сертификата истек или истекает в ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="f661b-131">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="f661b-132">Если защищенный LDAP успешно включен для управляемого домена, сообщение **Ожидание…** должно исчезнуть.</span><span class="sxs-lookup"><span data-stu-id="f661b-132">When secure LDAP is successfully enabled for your managed domain, the **Pending...** message should disappear.</span></span> <span data-ttu-id="f661b-133">Кроме того, должен появиться отпечаток отображаемого сертификата.</span><span class="sxs-lookup"><span data-stu-id="f661b-133">You should see the thumbprint of the certificate displayed.</span></span>

    ![Защищенный LDAP включен](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-the-internet"></a><span data-ttu-id="f661b-135">Задача 4. Включение защищенного доступа LDAP через Интернет</span><span class="sxs-lookup"><span data-stu-id="f661b-135">Task 4 - enable secure LDAP access over the internet</span></span>
<span data-ttu-id="f661b-136">**Необязательная задача**. Пропустите эту задачу настройки, если вы не планируете получать доступ к управляемому домену по протоколу LDAPS через Интернет.</span><span class="sxs-lookup"><span data-stu-id="f661b-136">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="f661b-137">К этой задаче следует приступать только после выполнения действий, описанных в разделе [Задача 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="f661b-137">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="f661b-138">В разделе **Доменные службы** страницы **Настройка** должен появиться параметр **ВКЛЮЧИТЬ ЗАЩИЩЕННЫЙ ДОСТУП LDAP ЧЕРЕЗ ИНТЕРНЕТ**.</span><span class="sxs-lookup"><span data-stu-id="f661b-138">You should see an option to **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** in the **domain services** section of the **Configure** page.</span></span> <span data-ttu-id="f661b-139">По умолчанию для этого параметра задано значение **НЕТ** , так как доступ к управляемому домену через Интернет по защищенному LDAP по умолчанию отключен.</span><span class="sxs-lookup"><span data-stu-id="f661b-139">This option is set to **NO** by default since internet access to the managed domain over secure LDAP is disabled by default.</span></span>

    ![Защищенный LDAP включен](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="f661b-141">Установите переключатель **ВКЛЮЧИТЬ ЗАЩИЩЕННЫЙ ДОСТУП LDAP ЧЕРЕЗ ИНТЕРНЕТ** в положение **ДА**.</span><span class="sxs-lookup"><span data-stu-id="f661b-141">Toggle **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** to **YES**.</span></span> <span data-ttu-id="f661b-142">Нажмите кнопку **СОХРАНИТЬ** в нижней области.</span><span class="sxs-lookup"><span data-stu-id="f661b-142">Click the **SAVE** button on the bottom panel.</span></span>
    <span data-ttu-id="f661b-143">![Защищенный LDAP включен](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="f661b-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="f661b-144">Раздел **Доменные службы** на вкладке **Настройка** должен стать неактивным и перейти в состояние **Ожидание…** на несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f661b-144">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="f661b-145">Через некоторое время будет включен доступ к управляемому домену по защищенному протоколу LDAP через Интернет.</span><span class="sxs-lookup"><span data-stu-id="f661b-145">After some time, internet access to your managed domain over secure LDAP is enabled.</span></span>

    ![Защищенный LDAP — состояние ожидания](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="f661b-147">Включение доступа к управляемому домену по защищенному протоколу LDAP через Интернет занимает примерно 10 минут.</span><span class="sxs-lookup"><span data-stu-id="f661b-147">It takes about 10 minutes to enable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="f661b-148">Если защищенный доступ LDAP к управляемому домену через Интернет успешно включен, сообщение **Ожидание…** должно исчезнуть.</span><span class="sxs-lookup"><span data-stu-id="f661b-148">When secure LDAP access to your managed domain over the internet is successfully enabled, the **Pending...** message should disappear.</span></span> <span data-ttu-id="f661b-149">В поле **ВНЕШНИЙ IP-АДРЕС ДЛЯ ДОСТУПА LDAPS**должен отобразиться внешний IP-адрес, который можно использовать для доступа к каталогу через LDAPS.</span><span class="sxs-lookup"><span data-stu-id="f661b-149">You should see the external IP address that can be used to access your directory over LDAPS in the field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![Защищенный LDAP включен](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-to-access-the-managed-domain-from-the-internet"></a><span data-ttu-id="f661b-151">Задача 5. Настройка DNS для доступа к управляемому домену через Интернет</span><span class="sxs-lookup"><span data-stu-id="f661b-151">Task 5 - configure DNS to access the managed domain from the internet</span></span>
<span data-ttu-id="f661b-152">**Необязательная задача**. Пропустите эту задачу настройки, если вы не планируете получать доступ к управляемому домену по протоколу LDAPS через Интернет.</span><span class="sxs-lookup"><span data-stu-id="f661b-152">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="f661b-153">К этой задаче следует приступать только после выполнения действий, описанных в разделе [Задача 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="f661b-153">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="f661b-154">После включения защищенного доступа LDAP к управляемому домену через Интернет необходимо обновить DNS-запись, чтобы клиентские компьютеры могли найти этот управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="f661b-154">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="f661b-155">По завершении задачи 4 внешний IP-адрес отобразится на вкладке **Настройка** в поле **ВНЕШНИЙ IP-АДРЕС ДЛЯ ДОСТУПА LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="f661b-155">At the end of task 4, an external IP address is displayed on the **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="f661b-156">Настройте внешний поставщик DNS, чтобы DNS-имя управляемого домена (например, ldaps.contoso100.com) указывало на этот внешний IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f661b-156">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span></span> <span data-ttu-id="f661b-157">В нашем примере необходимо создать следующую запись DNS.</span><span class="sxs-lookup"><span data-stu-id="f661b-157">In our example, we need to create the following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="f661b-158">Вот и все! Теперь вы готовы подключиться к управляемому домену по защищенному LDAP через Интернет.</span><span class="sxs-lookup"><span data-stu-id="f661b-158">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span></span>

> [!WARNING]
> <span data-ttu-id="f661b-159">Помните, что клиентские компьютеры должны доверять издателю сертификата LDAPS, чтобы иметь возможность подключиться к управляемому домену по протоколу LDAPS.</span><span class="sxs-lookup"><span data-stu-id="f661b-159">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span></span> <span data-ttu-id="f661b-160">Если вы используете корпоративный центр сертификации предприятия или общедоступный доверенный центр сертификации, то никакие действия не потребуются, так как клиентские компьютеры доверяют этим издателям сертификатов.</span><span class="sxs-lookup"><span data-stu-id="f661b-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="f661b-161">Если вы используете самозаверяющий сертификат, то на клиентском компьютере в хранилище доверенных сертификатов понадобится установить открытую часть самозаверяющего сертификата.</span><span class="sxs-lookup"><span data-stu-id="f661b-161">If you are using a self-signed certificate, you need to install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a><span data-ttu-id="f661b-162">Блокировка доступа через LDAPS к управляемому домену через Интернет</span><span class="sxs-lookup"><span data-stu-id="f661b-162">Lock-down LDAPS access to your managed domain over the internet</span></span>
> [!NOTE]
> <span data-ttu-id="f661b-163">**Необязательная задача**. Если вы не включали доступ к управляемому домену по протоколу LDAPS через Интернет, пропустите эту задачу.</span><span class="sxs-lookup"><span data-stu-id="f661b-163">**Optional task** - If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="f661b-164">К этой задаче следует приступать только после выполнения действий, описанных в разделе [Задача 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="f661b-164">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="f661b-165">Предоставление доступа к управляемому домену по протоколу LDAPS через Интернет представляет угрозу безопасности.</span><span class="sxs-lookup"><span data-stu-id="f661b-165">Exposing your managed domain for LDAPS access over the internet represents a security threat.</span></span> <span data-ttu-id="f661b-166">Управляемый домен доступен через Интернет на том порту, который используется для защищенного протокола LDAP (то есть порт 636).</span><span class="sxs-lookup"><span data-stu-id="f661b-166">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="f661b-167">Таким образом, вы можете ограничить доступ к управляемому домену для определенных известных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="f661b-167">Therefore, you can choose to restrict access to the managed domain to specific known IP addresses.</span></span> <span data-ttu-id="f661b-168">Для повышения безопасности создайте группу безопасности сети и свяжите ее с подсетью, для которой включены доменные службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f661b-168">For improved security, create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="f661b-169">В следующей таблице показан пример группы безопасности сети для блокировки доступа по защищенному протоколу LDAP через Интернет.</span><span class="sxs-lookup"><span data-stu-id="f661b-169">The following table illustrates a sample NSG you can configure, to lock down secure LDAP access over the internet.</span></span> <span data-ttu-id="f661b-170">Группа безопасности сети содержит набор правил, которые разрешают входящий доступ по протоколу LDAPS через TCP-порт 636 только для указанного набора IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="f661b-170">The NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="f661b-171">Правило "DenyAll" по умолчанию применяется ко всему входящему трафику из Интернета.</span><span class="sxs-lookup"><span data-stu-id="f661b-171">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span> <span data-ttu-id="f661b-172">Правило группы безопасности сети, которое разрешает доступ по протоколу LDAPS через Интернет только с указанных IP-адресов, имеет более высокий приоритет по сравнению с правилом группы безопасности сети "DenyAll".</span><span class="sxs-lookup"><span data-stu-id="f661b-172">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![Пример группы безопасности сети для доступа по защищенному протоколу LDAPS через Интернет](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="f661b-174">**Дополнительные сведения см. в статье** - [Фильтрация сетевого трафика с помощью групп безопасности сети](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="f661b-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="f661b-175">Связанная информация</span><span class="sxs-lookup"><span data-stu-id="f661b-175">Related content</span></span>
* [<span data-ttu-id="f661b-176">Приступая к работе с доменными службами Azure AD</span><span class="sxs-lookup"><span data-stu-id="f661b-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="f661b-177">Administer an Azure AD Domain Services managed domain (Администрирование управляемого домена доменных служб Azure AD)</span><span class="sxs-lookup"><span data-stu-id="f661b-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* <span data-ttu-id="f661b-178">[Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md) (Администрирование групповой политики в управляемом домене доменных служб Azure AD)</span><span class="sxs-lookup"><span data-stu-id="f661b-178">[Administer Group Policy on an Azure AD Domain Services managed domain](active-directory-ds-admin-guide-administer-group-policy.md)</span></span>
* [<span data-ttu-id="f661b-179">Группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="f661b-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="f661b-180">Создание группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="f661b-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
