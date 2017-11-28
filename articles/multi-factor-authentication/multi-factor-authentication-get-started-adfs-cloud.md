---
title: "Облачные ресурсы aaaSecure с Azure MFA и AD FS | Документы Microsoft"
description: "Это страница hello Azure многофакторной проверки подлинности, описывающий, как tooget работу с Azure MFA и AD FS в облаке hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="e8403-103">Защита облачных ресурсов с помощью Azure Multi-Factor Authentication и AD FS</span><span class="sxs-lookup"><span data-stu-id="e8403-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="e8403-104">Если в организации настроена федерация с Azure Active Directory, используйте Azure Multi-factor Authentication или служб федерации Active Directory (AD FS) toosecure ресурсы, к которым обращаются Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8403-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) toosecure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="e8403-105">Используйте следующие процедуры ресурсов Azure Active Directory toosecure с Azure Multi-factor Authentication или служб федерации Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="e8403-105">Use hello following procedures toosecure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="e8403-106">Защита ресурсов Azure AD с помощью AD FS</span><span class="sxs-lookup"><span data-stu-id="e8403-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="e8403-107">toosecure ресурса облака, настроить правило для утверждений, чтобы службы федерации Active Directory выдает утверждение multipleauthn hello, когда пользователь успешно выполняет двухшаговую проверку.</span><span class="sxs-lookup"><span data-stu-id="e8403-107">toosecure your cloud resource, set up a claims rule so that Active Directory Federation Services emits hello multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="e8403-108">Это утверждение будет передано в tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="e8403-108">This claim is passed on tooAzure AD.</span></span> <span data-ttu-id="e8403-109">Выполните это процедура toowalk шаги hello.</span><span class="sxs-lookup"><span data-stu-id="e8403-109">Follow this procedure toowalk through hello steps:</span></span>


1. <span data-ttu-id="e8403-110">Откройте оснастку управления AD FS.</span><span class="sxs-lookup"><span data-stu-id="e8403-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="e8403-111">В левой части экрана приветствия выберите **доверия с проверяющей стороной**.</span><span class="sxs-lookup"><span data-stu-id="e8403-111">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="e8403-112">Щелкните правой кнопкой мыши **Платформа удостоверений Microsoft Office 365** и выберите **Изменить правила утверждений**.</span><span class="sxs-lookup"><span data-stu-id="e8403-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="e8403-114">На вкладке "Правила преобразования выдачи" выберите **Добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="e8403-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="e8403-116">На Здравствуйте преобразования мастера добавления правила утверждения, выберите **пропуск или Фильтрация входящего утверждения** из hello раскрывающегося списка и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e8403-116">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>

   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="e8403-118">Укажите имя правила.</span><span class="sxs-lookup"><span data-stu-id="e8403-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="e8403-119">Выберите **ссылки на методы проверки подлинности** тип hello входящего утверждения.</span><span class="sxs-lookup"><span data-stu-id="e8403-119">Select **Authentication Methods References** as hello Incoming claim type.</span></span>
8. <span data-ttu-id="e8403-120">Щелкните **Пройти по всем значениям утверждений**.</span><span class="sxs-lookup"><span data-stu-id="e8403-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="e8403-121">![Мастер добавления правила преобразования утверждений](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="e8403-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="e8403-122">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="e8403-122">Click **Finish**.</span></span> <span data-ttu-id="e8403-123">Закройте консоль управления FS hello AD.</span><span class="sxs-lookup"><span data-stu-id="e8403-123">Close hello AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="e8403-124">Доверенные IP-адреса для федеративных пользователей</span><span class="sxs-lookup"><span data-stu-id="e8403-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="e8403-125">Надежные IP-адреса Администраторы на этапе tooby двухшаговую проверку для конкретных IP-адресов или для федеративных пользователей, имеющих запросов, исходящих из собственной интрасети.</span><span class="sxs-lookup"><span data-stu-id="e8403-125">Trusted IPs allow administrators tooby-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="e8403-126">Hello ниже описано, как tooconfigure Azure многофакторной проверки подлинности надежных IP-адресов с помощью федеративных пользователей и обойти двухшаговую проверку, когда запрос исходит от в интрасети федеративных пользователей.</span><span class="sxs-lookup"><span data-stu-id="e8403-126">hello following sections describe how tooconfigure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="e8403-127">Это достигается путем настройки AD FS toouse транзитного или фильтрации входящего шаблона утверждения с hello типа утверждения внутри корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="e8403-127">This is achieved by configuring AD FS toouse a pass-through or filter an incoming claim template with hello Inside Corporate Network claim type.</span></span>

<span data-ttu-id="e8403-128">В этом примере для доверенных отношений с проверяющей стороной используется Office 365.</span><span class="sxs-lookup"><span data-stu-id="e8403-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-hello-ad-fs-claims-rules"></a><span data-ttu-id="e8403-129">Настройка правил утверждений AD FS hello</span><span class="sxs-lookup"><span data-stu-id="e8403-129">Configure hello AD FS claims rules</span></span>
<span data-ttu-id="e8403-130">Первое Hello нам нужно toodo — утверждений tooconfigure hello AD FS.</span><span class="sxs-lookup"><span data-stu-id="e8403-130">hello first thing we need toodo is tooconfigure hello AD FS claims.</span></span> <span data-ttu-id="e8403-131">Создание двух правил для утверждений, один для hello внутри корпоративной сети утверждений типа и дополнительное для сохранения пользователей в системе.</span><span class="sxs-lookup"><span data-stu-id="e8403-131">Create two claims rules, one for hello Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="e8403-132">Откройте оснастку управления AD FS.</span><span class="sxs-lookup"><span data-stu-id="e8403-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="e8403-133">В левой части экрана приветствия выберите **доверия с проверяющей стороной**.</span><span class="sxs-lookup"><span data-stu-id="e8403-133">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="e8403-134">Щелкните правой кнопкой мыши **Microsoft Office 365 Identity Platform** (Платформа идентификации Microsoft Office 365) и выберите **Изменить правила утверждений...**
   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="e8403-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="e8403-135">На вкладке "Правила преобразования выдачи" выберите **Добавить правило**.
   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="e8403-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="e8403-136">На Здравствуйте преобразования мастера добавления правила утверждения, выберите **пропуск или Фильтрация входящего утверждения** из hello раскрывающегося списка и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e8403-136">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>
   <span data-ttu-id="e8403-137">![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="e8403-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="e8403-138">В hello поле Далее tooClaim имя правила присвойте правилу имя.</span><span class="sxs-lookup"><span data-stu-id="e8403-138">In hello box next tooClaim rule name, give your rule a name.</span></span> <span data-ttu-id="e8403-139">Пример: InsideCorpNet.</span><span class="sxs-lookup"><span data-stu-id="e8403-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="e8403-140">Из hello раскрывающегося списка, далее tooIncoming тип утверждения, выберите **внутри корпоративной сети**.</span><span class="sxs-lookup"><span data-stu-id="e8403-140">From hello drop-down, next tooIncoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="e8403-141">![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="e8403-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="e8403-142">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="e8403-142">Click **Finish**.</span></span>
9. <span data-ttu-id="e8403-143">На вкладке "Правила преобразования выдачи" выберите **Добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="e8403-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="e8403-144">На Здравствуйте преобразования мастера добавления правила утверждения, выберите **Отправка утверждений с помощью настраиваемого правила** из hello раскрывающегося списка и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e8403-144">On hello Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from hello drop-down and click **Next**.</span></span>
11. <span data-ttu-id="e8403-145">В окне приветствия под именем правила утверждений: введите *сохранить пользователей подписаны в*.</span><span class="sxs-lookup"><span data-stu-id="e8403-145">In hello box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="e8403-146">В hello пользовательские правила введите:</span><span class="sxs-lookup"><span data-stu-id="e8403-146">In hello Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="e8403-148">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="e8403-148">Click **Finish**.</span></span>
14. <span data-ttu-id="e8403-149">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="e8403-149">Click **Apply**.</span></span>
15. <span data-ttu-id="e8403-150">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e8403-150">Click **Ok**.</span></span>
16. <span data-ttu-id="e8403-151">Откройте оснастку управления AD FS.</span><span class="sxs-lookup"><span data-stu-id="e8403-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="e8403-152">Настройка Multi-Factor Authentication с доверенными IP-адресами в Azure для федеративных пользователей</span><span class="sxs-lookup"><span data-stu-id="e8403-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="e8403-153">Теперь, когда hello утверждения будут на месте, можно настроить надежные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="e8403-153">Now that hello claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="e8403-154">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e8403-154">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e8403-155">В левой части экрана приветствия щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e8403-155">On hello left, click **Active Directory**.</span></span>
3. <span data-ttu-id="e8403-156">В каталоге выберите каталог hello, где требуется tooset копирование надежные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="e8403-156">Under Directory, select hello directory where you want tooset up trusted IPs.</span></span>
4. <span data-ttu-id="e8403-157">На hello выбранном вами каталоге нажмите **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="e8403-157">On hello Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="e8403-158">В разделе hello многофакторной проверки подлинности щелкните **Управление параметрами службы**.</span><span class="sxs-lookup"><span data-stu-id="e8403-158">In hello multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="e8403-159">На странице настройки службы hello в списке надежных IP-адресов, выберите **пропустить / Multi-factor-authentication для запросов от федеративных пользователей из моей интрасети**.</span><span class="sxs-lookup"><span data-stu-id="e8403-159">On hello Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="e8403-161">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e8403-161">Click **save**.</span></span>
8. <span data-ttu-id="e8403-162">После применения обновления hello щелкните **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="e8403-162">Once hello updates have been applied, click **close**.</span></span>

<span data-ttu-id="e8403-163">Это все!</span><span class="sxs-lookup"><span data-stu-id="e8403-163">That’s it!</span></span> <span data-ttu-id="e8403-164">На этом этапе федеративные пользователи Office 365 должна иметь только toouse многофакторной проверки Подлинности когда утверждения приходят из вне корпоративной интрасети hello.</span><span class="sxs-lookup"><span data-stu-id="e8403-164">At this point, federated Office 365 users should only have toouse MFA when a claim originates from outside hello corporate intranet.</span></span>
