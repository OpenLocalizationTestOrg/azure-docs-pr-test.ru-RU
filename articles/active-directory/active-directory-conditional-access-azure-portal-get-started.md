---
title: "Начало работы с условным доступом в Azure Active Directory | Документы Майкрософт"
description: "Тестирование условного доступа с помощью условия расположения."
services: active-directory
keywords: "условный доступ к приложениям, условный доступ посредством Azure Active Directory, безопасный доступ к ресурсам организации, политики условного доступа"
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
ms.openlocfilehash: cd53e8be32d1e98aaf9f72177895871dba69df86
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="1c3f7-104">Начало работы с условным доступом в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1c3f7-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="1c3f7-105">Условный доступ — функция Azure Active Directory, позволяющая вам определить условия, при которых авторизованным пользователям разрешен доступ к вашим приложениям.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-105">Conditional access is a capability of Azure Active Directory that enables you to define conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="1c3f7-106">Эта статья содержит инструкции для тестирования условного доступа на основе условия расположения в среде.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="1c3f7-107">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="1c3f7-107">Scenario description</span></span>

<span data-ttu-id="1c3f7-108">Во многих организациях общим требованием является обязательная многофакторная идентификация для доступа к приложениям, который выполняется не из корпоративной интрасети.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-108">One common requirement in many organizations is to only require multi-factor authentication for access to apps that is not performed from the corporate intranet.</span></span> <span data-ttu-id="1c3f7-109">Вы легко можете реализовать это с помощью Azure Active Directory, настроив политику условного доступа на основе расположения.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="1c3f7-110">В этой статье вы найдете подробные инструкции по настройке соответствующей политики.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="1c3f7-111">С помощью [надежных IP-адресов](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) политика отличает попытки доступа из корпоративной интрасети от попыток доступа из остальных расположений.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-111">The policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) to distinguish between access attempts made from the corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="1c3f7-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1c3f7-112">Prerequisites</span></span>

<span data-ttu-id="1c3f7-113">В сценарии из этой статьи предполагается, что вы знакомы с основными понятиями, описанными в статье об [условном доступе Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1c3f7-113">The scenario outlined in this topic assumes that you are familiar with the concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="1c3f7-114">Чтобы протестировать этот сценарий, вам потребуется выполнить следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-114">To test this scenario, you need to:</span></span>

- <span data-ttu-id="1c3f7-115">Создать тестового пользователя.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-115">Create a test user</span></span> 

- <span data-ttu-id="1c3f7-116">Назначить лицензию Azure AD Premium тестовому пользователю.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-116">Assign an Azure AD Premium license to the test user</span></span>

- <span data-ttu-id="1c3f7-117">Настроить управляемое приложение и назначить ему тестового пользователя.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-117">Configure a managed app and assign your test user to it</span></span>

- <span data-ttu-id="1c3f7-118">Настроить надежные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-118">Configure trusted IPs</span></span>

<span data-ttu-id="1c3f7-119">Дополнительные сведения о надежных IP-адресах см. в разделе [Надежные IP-адреса](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="1c3f7-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="1c3f7-120">Настройка политики</span><span class="sxs-lookup"><span data-stu-id="1c3f7-120">Policy configuration steps</span></span>

<span data-ttu-id="1c3f7-121">**Чтобы настроить политику условного доступа, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="1c3f7-121">**To configure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="1c3f7-122">На портале Azure на панели навигации слева щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-122">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span></span> 

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="1c3f7-124">В колонке **Azure Active Directory** в разделе **Управление** щелкните **Условный доступ**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-124">On the **Azure Active Directory** blade, in the **Manage** section, click **Conditional access**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="1c3f7-126">В колонке **Условный доступ** на панели инструментов сверху нажмите кнопку **Добавить**, чтобы открыть колонку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-126">On the **Conditional Access** blade, to open the **New** blade, in the toolbar on the top, click **Add**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="1c3f7-128">В колонке **Создать** в текстовом поле **Имя** введите имя политики.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-128">On the **New** blade, in the **Name** textbox, type a name for your policy.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="1c3f7-130">В разделе **Назначение** щелкните **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-130">In the **Assignment** section, click **Users and groups**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="1c3f7-132">В колонке **Пользователи и группы** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-132">On the **Users and groups** blade, perform the following steps:</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="1c3f7-134">а.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-134">a.</span></span> <span data-ttu-id="1c3f7-135">Щелкните **Выбрать пользователей и группы**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="1c3f7-136">b.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-136">b.</span></span> <span data-ttu-id="1c3f7-137">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-137">Click **Select**.</span></span>

    <span data-ttu-id="1c3f7-138">c.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-138">c.</span></span> <span data-ttu-id="1c3f7-139">В колонке **Выбрать** выберите тестового пользователя и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-139">On the **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="1c3f7-140">d.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-140">d.</span></span> <span data-ttu-id="1c3f7-141">В колонке **Пользователи и группы** нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-141">On the **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="1c3f7-142">В колонке **Создать** в разделе **Назначения** щелкните **Облачные приложения**, чтобы открыть колонку **Облачные приложения**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-142">On the **New** blade, to open the **Cloud apps** blade, in the **Assignment** section, click **Cloud apps**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="1c3f7-144">В колонке **Облачные приложения** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-144">On the **Cloud apps** blade, perform the following steps:</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="1c3f7-146">а.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-146">a.</span></span> <span data-ttu-id="1c3f7-147">Щелкните **Выбрать приложения**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-147">Click **Select apps**.</span></span>

    <span data-ttu-id="1c3f7-148">b.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-148">b.</span></span> <span data-ttu-id="1c3f7-149">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-149">Click **Select**.</span></span>

    <span data-ttu-id="1c3f7-150">c.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-150">c.</span></span> <span data-ttu-id="1c3f7-151">В колонке **Выбрать** выберите облачное приложение и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-151">On the **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="1c3f7-152">d.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-152">d.</span></span> <span data-ttu-id="1c3f7-153">В колонке **Облачные приложения** нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-153">On the **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="1c3f7-154">В колонке **Создать** в разделе **Назначения** щелкните **Условия**, чтобы открыть колонку **Условия**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-154">On the **New** blade, to open the **Conditions** blade, in the **Assignment** section, click **Conditions**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="1c3f7-156">В колонке **Условия** щелкните **Расположения**, чтобы открыть колонку **Расположения**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-156">On the **Conditions** blade, to open the **Locations** blade, click **Locations**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="1c3f7-158">В колонке **Расположения** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-158">On the **Locations** blade, perform the following steps:</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="1c3f7-160">а.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-160">a.</span></span> <span data-ttu-id="1c3f7-161">Под параметром **Настройка** нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="1c3f7-162">b.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-162">b.</span></span> <span data-ttu-id="1c3f7-163">На вкладке **Включить** выберите **Все расположения**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="1c3f7-164">c.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-164">c.</span></span> <span data-ttu-id="1c3f7-165">Откройте вкладку **Исключить** и выберите **All trusted IPs** (Все надежные IP-адреса).</span><span class="sxs-lookup"><span data-stu-id="1c3f7-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="1c3f7-167">d.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-167">d.</span></span> <span data-ttu-id="1c3f7-168">Нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="1c3f7-168">Click **Done**.</span></span>

12. <span data-ttu-id="1c3f7-169">В колонке **Условия** нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-169">On the **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="1c3f7-170">В колонке **Создать** в разделе **Элементы управления** щелкните **Предоставить**, чтобы открыть колонку **Предоставить**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-170">On the **New** blade, to open the **Grant** blade, in the **Controls** section, click **Grant**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="1c3f7-172">В колонке **Предоставить** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-172">On the **Grant** blade, perform the following steps:</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="1c3f7-174">а.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-174">a.</span></span> <span data-ttu-id="1c3f7-175">Выберите **Требовать многофакторную проверку подлинности**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="1c3f7-176">b.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-176">b.</span></span> <span data-ttu-id="1c3f7-177">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-177">Click **Select**.</span></span>

15. <span data-ttu-id="1c3f7-178">В колонке **Создать** в разделе **Включить политику** нажмите кнопку **Вкл.**</span><span class="sxs-lookup"><span data-stu-id="1c3f7-178">On the **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Условный доступ](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="1c3f7-180">В колонке**Создать** щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-180">On the **New** blade, click **Create**.</span></span>


## <a name="testing-the-policy"></a><span data-ttu-id="1c3f7-181">Тестирование политики</span><span class="sxs-lookup"><span data-stu-id="1c3f7-181">Testing the policy</span></span>

<span data-ttu-id="1c3f7-182">Чтобы протестировать политику, обратитесь к приложению с устройств, к которым применимы следующие характеристики:</span><span class="sxs-lookup"><span data-stu-id="1c3f7-182">To test your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="1c3f7-183">IP-адрес устройства входит в диапазон настроенных надежных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="1c3f7-184">IP-адрес устройства не входит в диапазон настроенных надежных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="1c3f7-185">Многофакторная идентификация должна требоваться только во время попытки подключения с устройства, IP-адрес которого не входит в диапазон настроенных надежных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="1c3f7-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="1c3f7-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c3f7-186">Next steps</span></span>

<span data-ttu-id="1c3f7-187">Дополнительные сведения см. в статье об [условном доступе в Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1c3f7-187">If you would like to learn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

