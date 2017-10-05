---
title: "Защита облачных ресурсов с помощью MFA Azure и AD FS | Документация Майкрософт"
description: "Эта страница посвящена Azure Multi-Factor Authentication. Она содержит сведения по началу работы с Azure MFA и AD FS в облаке."
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
ms.openlocfilehash: 6cf4ec4f777ea1f2b852945ab82da2547946f378
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="75de6-103">Защита облачных ресурсов с помощью Azure Multi-Factor Authentication и AD FS</span><span class="sxs-lookup"><span data-stu-id="75de6-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="75de6-104">Если в организации настроена федерация с Azure Active Directory, используйте Многофакторную идентификацию Azure или службы федерации Active Directory (AD FS), чтобы обеспечить безопасность ресурсов, доступных для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75de6-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) to secure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="75de6-105">Чтобы защитить ресурсы Azure Active Directory с помощью многофакторной идентификации Azure или служб федерации Active Directory, следуйте инструкциям, приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="75de6-105">Use the following procedures to secure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="75de6-106">Защита ресурсов Azure AD с помощью AD FS</span><span class="sxs-lookup"><span data-stu-id="75de6-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="75de6-107">Чтобы защитить облачный ресурс, настройте правило утверждений, чтобы при выполнении пользователем двухфакторной проверки подлинности службы федерации Active Directory выдавали утверждение multipleauthn.</span><span class="sxs-lookup"><span data-stu-id="75de6-107">To secure your cloud resource, set up a claims rule so that Active Directory Federation Services emits the multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="75de6-108">Это утверждение передается в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75de6-108">This claim is passed on to Azure AD.</span></span> <span data-ttu-id="75de6-109">Для этого следуйте такой процедуре:</span><span class="sxs-lookup"><span data-stu-id="75de6-109">Follow this procedure to walk through the steps:</span></span>


1. <span data-ttu-id="75de6-110">Откройте оснастку управления AD FS.</span><span class="sxs-lookup"><span data-stu-id="75de6-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="75de6-111">В левой части выберите **Отношения доверия проверяющей стороны**.</span><span class="sxs-lookup"><span data-stu-id="75de6-111">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="75de6-112">Щелкните правой кнопкой мыши **Платформа удостоверений Microsoft Office 365** и выберите **Изменить правила утверждений**.</span><span class="sxs-lookup"><span data-stu-id="75de6-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="75de6-114">На вкладке "Правила преобразования выдачи" выберите **Добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="75de6-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="75de6-116">В мастере добавления правила преобразования утверждения выберите **Проход через входящее утверждение или его фильтрация** в раскрывающемся списке и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="75de6-116">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>

   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="75de6-118">Укажите имя правила.</span><span class="sxs-lookup"><span data-stu-id="75de6-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="75de6-119">Выберите **Ссылки на методы проверки подлинности** в качестве типа входящего утверждения.</span><span class="sxs-lookup"><span data-stu-id="75de6-119">Select **Authentication Methods References** as the Incoming claim type.</span></span>
8. <span data-ttu-id="75de6-120">Щелкните **Пройти по всем значениям утверждений**.</span><span class="sxs-lookup"><span data-stu-id="75de6-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="75de6-121">![Мастер добавления правила преобразования утверждений](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="75de6-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="75de6-122">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="75de6-122">Click **Finish**.</span></span> <span data-ttu-id="75de6-123">Закройте консоль управления AD FS.</span><span class="sxs-lookup"><span data-stu-id="75de6-123">Close the AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="75de6-124">Доверенные IP-адреса для федеративных пользователей</span><span class="sxs-lookup"><span data-stu-id="75de6-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="75de6-125">Надежные IP-адреса позволяют администраторам обойти двухфакторную проверку подлинности для конкретных IP-адресов или для федеративных пользователей, запросы от которых формируются в их собственной интрасети.</span><span class="sxs-lookup"><span data-stu-id="75de6-125">Trusted IPs allow administrators to by-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="75de6-126">В следующих разделах описывается настройка многофакторной идентификации Azure с надежными IP-адресами для федеративных пользователей и для обхода двухфакторной проверки подлинности, когда запросы от федеративных пользователей формируются в их собственной интрасети.</span><span class="sxs-lookup"><span data-stu-id="75de6-126">The following sections describe how to configure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="75de6-127">Для этого необходимо настроить транзит в службе федерации Active Directory или отфильтровывать входящие шаблоны утверждения с типом утверждения в корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="75de6-127">This is achieved by configuring AD FS to use a pass-through or filter an incoming claim template with the Inside Corporate Network claim type.</span></span>

<span data-ttu-id="75de6-128">В этом примере для доверенных отношений с проверяющей стороной используется Office 365.</span><span class="sxs-lookup"><span data-stu-id="75de6-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-the-ad-fs-claims-rules"></a><span data-ttu-id="75de6-129">Настройка правил утверждений AD FS</span><span class="sxs-lookup"><span data-stu-id="75de6-129">Configure the AD FS claims rules</span></span>
<span data-ttu-id="75de6-130">Первое, что необходимо сделать, — настроить утверждения AD FS.</span><span class="sxs-lookup"><span data-stu-id="75de6-130">The first thing we need to do is to configure the AD FS claims.</span></span> <span data-ttu-id="75de6-131">Создайте два правила утверждений: одно для типа утверждений в корпоративной сети и второе для пользователей, выполнивших вход.</span><span class="sxs-lookup"><span data-stu-id="75de6-131">Create two claims rules, one for the Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="75de6-132">Откройте оснастку управления AD FS.</span><span class="sxs-lookup"><span data-stu-id="75de6-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="75de6-133">В левой части выберите **Отношения доверия проверяющей стороны**.</span><span class="sxs-lookup"><span data-stu-id="75de6-133">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="75de6-134">Щелкните правой кнопкой мыши **Microsoft Office 365 Identity Platform** (Платформа идентификации Microsoft Office 365) и выберите **Изменить правила утверждений...**
   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="75de6-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="75de6-135">На вкладке "Правила преобразования выдачи" выберите **Добавить правило**.
   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="75de6-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="75de6-136">В мастере добавления правила преобразования утверждения выберите **Проход через входящее утверждение или его фильтрация** в раскрывающемся списке и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="75de6-136">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>
   <span data-ttu-id="75de6-137">![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="75de6-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="75de6-138">В поле рядом с именем правила утверждения укажите имя правила.</span><span class="sxs-lookup"><span data-stu-id="75de6-138">In the box next to Claim rule name, give your rule a name.</span></span> <span data-ttu-id="75de6-139">Пример: InsideCorpNet.</span><span class="sxs-lookup"><span data-stu-id="75de6-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="75de6-140">В раскрывающемся списке "Тип входящего утверждения" выберите **В корпоративной сети**.</span><span class="sxs-lookup"><span data-stu-id="75de6-140">From the drop-down, next to Incoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="75de6-141">![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="75de6-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="75de6-142">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="75de6-142">Click **Finish**.</span></span>
9. <span data-ttu-id="75de6-143">На вкладке "Правила преобразования выдачи" выберите **Добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="75de6-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="75de6-144">В мастере добавления правила преобразования утверждения выберите **Отправка утверждений с помощью настраиваемого правила** в раскрывающемся списке и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="75de6-144">On the Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from the drop-down and click **Next**.</span></span>
11. <span data-ttu-id="75de6-145">В поле "Имя правила утверждения" введите *Не затрагивать пользователей, вошедших в систему*.</span><span class="sxs-lookup"><span data-stu-id="75de6-145">In the box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="75de6-146">В поле "Настраиваемое правило " введите следующее:</span><span class="sxs-lookup"><span data-stu-id="75de6-146">In the Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="75de6-148">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="75de6-148">Click **Finish**.</span></span>
14. <span data-ttu-id="75de6-149">Нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="75de6-149">Click **Apply**.</span></span>
15. <span data-ttu-id="75de6-150">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="75de6-150">Click **Ok**.</span></span>
16. <span data-ttu-id="75de6-151">Откройте оснастку управления AD FS.</span><span class="sxs-lookup"><span data-stu-id="75de6-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="75de6-152">Настройка Multi-Factor Authentication с доверенными IP-адресами в Azure для федеративных пользователей</span><span class="sxs-lookup"><span data-stu-id="75de6-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="75de6-153">Теперь, когда утверждения добавлены, можно настроить надежные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="75de6-153">Now that the claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="75de6-154">Перейдите на [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="75de6-154">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="75de6-155">В левой части щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="75de6-155">On the left, click **Active Directory**.</span></span>
3. <span data-ttu-id="75de6-156">В разделе "Каталог" выберите каталог, в котором нужно настроить надежные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="75de6-156">Under Directory, select the directory where you want to set up trusted IPs.</span></span>
4. <span data-ttu-id="75de6-157">Выбрав нужный каталог, щелкните **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="75de6-157">On the Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="75de6-158">В разделе многофакторной идентификации щелкните **Управление параметрами службы**.</span><span class="sxs-lookup"><span data-stu-id="75de6-158">In the multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="75de6-159">На странице настроек службы в списке надежных IP-адресов выберите **Пропустить многофакторную проверку подлинности для запросов от федеративных пользователей из моей интрасети**.</span><span class="sxs-lookup"><span data-stu-id="75de6-159">On the Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![Облако](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="75de6-161">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="75de6-161">Click **save**.</span></span>
8. <span data-ttu-id="75de6-162">После применения обновлений щелкните **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="75de6-162">Once the updates have been applied, click **close**.</span></span>

<span data-ttu-id="75de6-163">Это все!</span><span class="sxs-lookup"><span data-stu-id="75de6-163">That’s it!</span></span> <span data-ttu-id="75de6-164">Теперь федеративные пользователи Office 365 должны использовать MFA только в том случае, если утверждение сформировано за пределами корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="75de6-164">At this point, federated Office 365 users should only have to use MFA when a claim originates from outside the corporate intranet.</span></span>
