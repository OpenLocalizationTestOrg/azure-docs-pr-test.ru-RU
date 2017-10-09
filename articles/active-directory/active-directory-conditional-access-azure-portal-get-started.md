---
title: "aaaGet работы с условным доступом в Azure Active Directory | Документы Microsoft"
description: "Тестирование условного доступа с помощью условия расположения."
services: active-directory
keywords: "tooapps условного доступа, условного доступа с Azure AD, защита доступа к ресурсам toocompany, политики условного доступа"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="fae80-104">Начало работы с условным доступом в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fae80-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="fae80-105">Условный доступ — это компонент Azure Active Directory, который позволяет вам toodefine условия при которых несанкционированный доступ приложений.</span><span class="sxs-lookup"><span data-stu-id="fae80-105">Conditional access is a capability of Azure Active Directory that enables you toodefine conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="fae80-106">Эта статья содержит инструкции для тестирования условного доступа на основе условия расположения в среде.</span><span class="sxs-lookup"><span data-stu-id="fae80-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="fae80-107">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="fae80-107">Scenario description</span></span>

<span data-ttu-id="fae80-108">Одно общее требование во многих организациях — tooonly требовать многофакторную проверку подлинности для доступа tooapps, выполняется не из hello корпоративной интрасети.</span><span class="sxs-lookup"><span data-stu-id="fae80-108">One common requirement in many organizations is tooonly require multi-factor authentication for access tooapps that is not performed from hello corporate intranet.</span></span> <span data-ttu-id="fae80-109">Вы легко можете реализовать это с помощью Azure Active Directory, настроив политику условного доступа на основе расположения.</span><span class="sxs-lookup"><span data-stu-id="fae80-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="fae80-110">В этой статье вы найдете подробные инструкции по настройке соответствующей политики.</span><span class="sxs-lookup"><span data-stu-id="fae80-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="fae80-111">Здравствуйте, использует политику [надежных IP-адресов](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish между попытками доступа из корпоративной hello в интрасети и все остальные.</span><span class="sxs-lookup"><span data-stu-id="fae80-111">hello policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish between access attempts made from hello corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="fae80-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fae80-112">Prerequisites</span></span>

<span data-ttu-id="fae80-113">Hello сценарии, описанные в этом разделе предполагается, что вы знакомы с основными понятиями hello, описанные в [условного доступа Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fae80-113">hello scenario outlined in this topic assumes that you are familiar with hello concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="fae80-114">tootest этот сценарий, необходимо:</span><span class="sxs-lookup"><span data-stu-id="fae80-114">tootest this scenario, you need to:</span></span>

- <span data-ttu-id="fae80-115">Создать тестового пользователя.</span><span class="sxs-lookup"><span data-stu-id="fae80-115">Create a test user</span></span> 

- <span data-ttu-id="fae80-116">Назначить Azure AD Premium лицензирования toohello тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="fae80-116">Assign an Azure AD Premium license toohello test user</span></span>

- <span data-ttu-id="fae80-117">Настройка управляемого приложения и назначение вашей tooit тестового пользователя</span><span class="sxs-lookup"><span data-stu-id="fae80-117">Configure a managed app and assign your test user tooit</span></span>

- <span data-ttu-id="fae80-118">Настроить надежные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="fae80-118">Configure trusted IPs</span></span>

<span data-ttu-id="fae80-119">Дополнительные сведения о надежных IP-адресах см. в разделе [Надежные IP-адреса](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="fae80-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="fae80-120">Настройка политики</span><span class="sxs-lookup"><span data-stu-id="fae80-120">Policy configuration steps</span></span>

<span data-ttu-id="fae80-121">**tooconfigure политику условного доступа, выполните:**</span><span class="sxs-lookup"><span data-stu-id="fae80-121">**tooconfigure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="fae80-122">В hello портал Azure, на левой переходов hello, щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fae80-122">In hello Azure portal, on hello left navbar, click **Azure Active Directory**.</span></span> 

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="fae80-124">На hello **Azure Active Directory** колонки в hello **управление** щелкните **условного доступа**.</span><span class="sxs-lookup"><span data-stu-id="fae80-124">On hello **Azure Active Directory** blade, in hello **Manage** section, click **Conditional access**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="fae80-126">На hello **условного доступа** колонки, tooopen hello **New** колонки в верхней части экрана приветствия hello инструментов щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="fae80-126">On hello **Conditional Access** blade, tooopen hello **New** blade, in hello toolbar on hello top, click **Add**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="fae80-128">На hello **New** колонки в hello **имя** текстовом поле введите имя для политики.</span><span class="sxs-lookup"><span data-stu-id="fae80-128">On hello **New** blade, in hello **Name** textbox, type a name for your policy.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="fae80-130">В hello **назначения** щелкните **пользователей и групп**.</span><span class="sxs-lookup"><span data-stu-id="fae80-130">In hello **Assignment** section, click **Users and groups**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="fae80-132">На hello **пользователей и групп** колонки, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="fae80-132">On hello **Users and groups** blade, perform hello following steps:</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="fae80-134">а.</span><span class="sxs-lookup"><span data-stu-id="fae80-134">a.</span></span> <span data-ttu-id="fae80-135">Щелкните **Выбрать пользователей и группы**.</span><span class="sxs-lookup"><span data-stu-id="fae80-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="fae80-136">b.</span><span class="sxs-lookup"><span data-stu-id="fae80-136">b.</span></span> <span data-ttu-id="fae80-137">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="fae80-137">Click **Select**.</span></span>

    <span data-ttu-id="fae80-138">c.</span><span class="sxs-lookup"><span data-stu-id="fae80-138">c.</span></span> <span data-ttu-id="fae80-139">На hello **выберите** колонке выберите тестового пользователя и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="fae80-139">On hello **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="fae80-140">d.</span><span class="sxs-lookup"><span data-stu-id="fae80-140">d.</span></span> <span data-ttu-id="fae80-141">На hello **пользователей и групп** колонка, щелкните **сделать**.</span><span class="sxs-lookup"><span data-stu-id="fae80-141">On hello **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="fae80-142">На hello **New** колонки, tooopen hello **облачные приложения** колонки в hello **назначения** щелкните **облачные приложения**.</span><span class="sxs-lookup"><span data-stu-id="fae80-142">On hello **New** blade, tooopen hello **Cloud apps** blade, in hello **Assignment** section, click **Cloud apps**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="fae80-144">На hello **облачные приложения** колонки, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="fae80-144">On hello **Cloud apps** blade, perform hello following steps:</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="fae80-146">а.</span><span class="sxs-lookup"><span data-stu-id="fae80-146">a.</span></span> <span data-ttu-id="fae80-147">Щелкните **Выбрать приложения**.</span><span class="sxs-lookup"><span data-stu-id="fae80-147">Click **Select apps**.</span></span>

    <span data-ttu-id="fae80-148">b.</span><span class="sxs-lookup"><span data-stu-id="fae80-148">b.</span></span> <span data-ttu-id="fae80-149">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="fae80-149">Click **Select**.</span></span>

    <span data-ttu-id="fae80-150">c.</span><span class="sxs-lookup"><span data-stu-id="fae80-150">c.</span></span> <span data-ttu-id="fae80-151">На hello **выберите** колонке выберите облачные приложения и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="fae80-151">On hello **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="fae80-152">d.</span><span class="sxs-lookup"><span data-stu-id="fae80-152">d.</span></span> <span data-ttu-id="fae80-153">На hello **облачные приложения** колонка, щелкните **сделать**.</span><span class="sxs-lookup"><span data-stu-id="fae80-153">On hello **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="fae80-154">На hello **New** колонки, tooopen hello **условия** колонки в hello **назначения** щелкните **условия**.</span><span class="sxs-lookup"><span data-stu-id="fae80-154">On hello **New** blade, tooopen hello **Conditions** blade, in hello **Assignment** section, click **Conditions**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="fae80-156">На hello **условия** колонки, tooopen hello **расположения** колонка, щелкните **расположения**.</span><span class="sxs-lookup"><span data-stu-id="fae80-156">On hello **Conditions** blade, tooopen hello **Locations** blade, click **Locations**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="fae80-158">На hello **расположения** колонки, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="fae80-158">On hello **Locations** blade, perform hello following steps:</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="fae80-160">а.</span><span class="sxs-lookup"><span data-stu-id="fae80-160">a.</span></span> <span data-ttu-id="fae80-161">Под параметром **Настройка** нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="fae80-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="fae80-162">b.</span><span class="sxs-lookup"><span data-stu-id="fae80-162">b.</span></span> <span data-ttu-id="fae80-163">На вкладке **Включить** выберите **Все расположения**.</span><span class="sxs-lookup"><span data-stu-id="fae80-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="fae80-164">c.</span><span class="sxs-lookup"><span data-stu-id="fae80-164">c.</span></span> <span data-ttu-id="fae80-165">Откройте вкладку **Исключить** и выберите **All trusted IPs** (Все надежные IP-адреса).</span><span class="sxs-lookup"><span data-stu-id="fae80-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="fae80-167">d.</span><span class="sxs-lookup"><span data-stu-id="fae80-167">d.</span></span> <span data-ttu-id="fae80-168">Нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="fae80-168">Click **Done**.</span></span>

12. <span data-ttu-id="fae80-169">На hello **условия** колонка, щелкните **сделать**.</span><span class="sxs-lookup"><span data-stu-id="fae80-169">On hello **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="fae80-170">На hello **New** колонки, tooopen hello **Grant** колонки в hello **элементов управления** щелкните **Grant**.</span><span class="sxs-lookup"><span data-stu-id="fae80-170">On hello **New** blade, tooopen hello **Grant** blade, in hello **Controls** section, click **Grant**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="fae80-172">На hello **Grant** колонки, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="fae80-172">On hello **Grant** blade, perform hello following steps:</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="fae80-174">а.</span><span class="sxs-lookup"><span data-stu-id="fae80-174">a.</span></span> <span data-ttu-id="fae80-175">Выберите **Требовать многофакторную проверку подлинности**.</span><span class="sxs-lookup"><span data-stu-id="fae80-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="fae80-176">b.</span><span class="sxs-lookup"><span data-stu-id="fae80-176">b.</span></span> <span data-ttu-id="fae80-177">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="fae80-177">Click **Select**.</span></span>

15. <span data-ttu-id="fae80-178">На hello **New** колонки в разделе **включить политику**, нажмите кнопку **на**.</span><span class="sxs-lookup"><span data-stu-id="fae80-178">On hello **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="fae80-180">На hello **New** колонка, щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="fae80-180">On hello **New** blade, click **Create**.</span></span>


## <a name="testing-hello-policy"></a><span data-ttu-id="fae80-181">Политика тестирования hello</span><span class="sxs-lookup"><span data-stu-id="fae80-181">Testing hello policy</span></span>

<span data-ttu-id="fae80-182">tootest политики следует доступ к вашему приложению с устройств:</span><span class="sxs-lookup"><span data-stu-id="fae80-182">tootest your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="fae80-183">IP-адрес устройства входит в диапазон настроенных надежных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="fae80-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="fae80-184">IP-адрес устройства не входит в диапазон настроенных надежных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="fae80-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="fae80-185">Многофакторная идентификация должна требоваться только во время попытки подключения с устройства, IP-адрес которого не входит в диапазон настроенных надежных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="fae80-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="fae80-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fae80-186">Next steps</span></span>

<span data-ttu-id="fae80-187">При желании toolearn Дополнительные сведения о условного доступа в разделе [условного доступа Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fae80-187">If you would like toolearn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

