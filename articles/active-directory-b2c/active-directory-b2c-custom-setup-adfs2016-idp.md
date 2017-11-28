---
title: "Azure Active Directory B2C. Добавление ADFS в качестве поставщика удостоверений SAML с помощью пользовательских политик"
description: "Эта статья представляет собой практическое руководство, в котором объясняется, как настроить ADFS 2016 с помощью протокола SAML и пользовательских политик."
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: ef0495460b5652dd6052a49ab9c722381e93458b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a><span data-ttu-id="f4f47-103">Azure Active Directory B2C. Добавление ADFS в качестве поставщика удостоверений SAML с помощью пользовательских политик</span><span class="sxs-lookup"><span data-stu-id="f4f47-103">Azure Active Directory B2C: Add ADFS as a SAML identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="f4f47-104">В этой статье описывается выполнение входа для пользователей из учетной записи ADFS с помощью [пользовательских политик](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="f4f47-104">This article shows you how to enable sign-in for users from ADFS account through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4f47-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f4f47-105">Prerequisites</span></span>

<span data-ttu-id="f4f47-106">Выполните шаги, описанные в статье [Azure Active Directory B2C. Приступая к работе с настраиваемыми политиками](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="f4f47-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="f4f47-107">А именно:</span><span class="sxs-lookup"><span data-stu-id="f4f47-107">These steps include:</span></span>

1.  <span data-ttu-id="f4f47-108">Создание отношения доверия с проверяющей стороной ADFS.</span><span class="sxs-lookup"><span data-stu-id="f4f47-108">Creating an ADFS Relying Party Trust.</span></span>
2.  <span data-ttu-id="f4f47-109">Добавление сертификата отношения доверия с проверяющей стороной ADFS в Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f4f47-109">Adding the ADFS Relying Party Trust certificate to Azure AD B2C.</span></span>
3.  <span data-ttu-id="f4f47-110">Добавление поставщика утверждений в политику.</span><span class="sxs-lookup"><span data-stu-id="f4f47-110">Adding claims provider to a policy.</span></span>
4.  <span data-ttu-id="f4f47-111">Регистрация поставщика утверждений учетной записи ADFS для пути взаимодействия пользователя.</span><span class="sxs-lookup"><span data-stu-id="f4f47-111">Registering the ADFS account claims provider to a user journey.</span></span>
5.  <span data-ttu-id="f4f47-112">Отправка политики в клиент Azure AD B2C и ее проверка.</span><span class="sxs-lookup"><span data-stu-id="f4f47-112">Uploading the policy to an Azure AD B2C tenant and test it.</span></span>

## <a name="to-create-a-claims-aware-relying-party-trust"></a><span data-ttu-id="f4f47-113">Создание отношения доверия с проверяющей стороной, поддерживающей утверждения</span><span class="sxs-lookup"><span data-stu-id="f4f47-113">To create a claims-aware Relying Party Trust</span></span>

<span data-ttu-id="f4f47-114">Чтобы использовать ADFS в качестве поставщика удостоверений в Azure Active Directory (Azure AD) B2C, необходимо сначала создать отношение доверия с проверяющей стороной ADFS и задать в ней правильные параметры.</span><span class="sxs-lookup"><span data-stu-id="f4f47-114">To use ADFS as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an ADFS Relying Party Trust and supply it with the right parameters.</span></span>

<span data-ttu-id="f4f47-115">Чтобы добавить новое отношение доверия с проверяющей стороной с помощью оснастки управления AD FS и вручную настроить параметры, выполните следующую процедуру на сервере федерации.</span><span class="sxs-lookup"><span data-stu-id="f4f47-115">To add a new relying party trust by using the AD FS Management snap-in and manually configure the settings, perform the following procedure on a federation server.</span></span>

<span data-ttu-id="f4f47-116">Чтобы выполнить эту процедуру, необходимо по крайней мере входить в группу **Администраторы** или аналогичную группу на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="f4f47-116">Membership in **Administrators**, or equivalent, on the local computer is the minimum required to complete this procedure.</span></span> <span data-ttu-id="f4f47-117">Дополнительные сведения об использовании соответствующих учетных записей и членстве в группах см. в статье [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477) (Локальные и доменные группы по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="f4f47-117">Review details about using the appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span></span>

1.  <span data-ttu-id="f4f47-118">В диспетчере серверов щелкните **Средства**, а затем выберите **ADFS Management** (Управление ADFS).</span><span class="sxs-lookup"><span data-stu-id="f4f47-118">In Server Manager, click **Tools**, and then select **ADFS Management**.</span></span>

2.  <span data-ttu-id="f4f47-119">Выберите **Add Relying Party Trust** (Добавить отношение доверия с проверяющей стороной).</span><span class="sxs-lookup"><span data-stu-id="f4f47-119">Click on **Add Relying Party Trust**.</span></span>
    <span data-ttu-id="f4f47-120">![Добавление отношения доверия проверяющей стороны](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-120">![Add Relying Party Trust](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span></span>

3.  <span data-ttu-id="f4f47-121">На странице **приветствия** выберите **Claims aware** (Поддерживающие утверждения) и нажмите кнопку **Начало**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-121">On the **Welcome** page, choose **Claims aware** and click **Start**.</span></span>
    <span data-ttu-id="f4f47-122">![На странице приветствия выберите Claims aware (Поддерживающие утверждения)](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-122">![On the Welcome page, choose Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span></span>
4.  <span data-ttu-id="f4f47-123">На странице **Выберите источник данных** щелкните **Enter data about the relying party manually** (Ввод данных о проверяющей стороне вручную), а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-123">On the **Select Data Source** page, click **Enter data about the relying party manually**, and then click **Next**.</span></span>
    <span data-ttu-id="f4f47-124">![Ввод данных о проверяющей стороне](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-124">![Enter data about the relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span></span>

5.  <span data-ttu-id="f4f47-125">На странице **Specify Display Name** (Указание отображаемого имени) введите имя в поле **Отображаемое имя**. В поле **Примечания** введите описание для этого отношения доверия с проверяющей стороной и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-125">On the **Specify Display Name** page, type a name in **Display name**, under **Notes** type a description for this relying party trust, and then click **Next**.</span></span>
    <span data-ttu-id="f4f47-126">![Указание отображаемого имени и примечаний](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-126">![Specify Display Name and notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span></span>
6.  <span data-ttu-id="f4f47-127">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="f4f47-127">Optional.</span></span> <span data-ttu-id="f4f47-128">Если у вас есть необязательный сертификат для шифрования маркера, на странице **Configure Certificate** (Настройка сертификата) щелкните **Обзор** для поиска файла сертификата, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-128">If you have an optional token encryption certificate, then on the **Configure Certificate** page, click **Browse** to locate your certificate file, and then click **Next**.</span></span>
    <span data-ttu-id="f4f47-129">![Настройка сертификата](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-129">![Configure Certificate](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span></span>
7.  <span data-ttu-id="f4f47-130">На странице **Configure URL** (Настройка URL-адреса) установите флажок **Enable support for the SAML 2.0 WebSSO protocol** (Включить поддержку протокола SAML 2.0 WebSSO).</span><span class="sxs-lookup"><span data-stu-id="f4f47-130">On the **Configure URL** page, select the **Enable support for the SAML 2.0 WebSSO protocol** check box.</span></span> <span data-ttu-id="f4f47-131">В поле **Relying party SAML 2.0 SSO service URL** (URL-адрес службы SAML 2.0 SSO проверяющей стороны) введите URL-адрес конечной точки службы SAML для этого отношения доверия с проверяющей стороной и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-131">Under **Relying party SAML 2.0 SSO service URL**, type the Security Assertion Markup Language (SAML) service endpoint URL for this relying party trust, and then click **Next**.</span></span>  <span data-ttu-id="f4f47-132">Вставьте `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}` в поле **Relying party SAML 2.0 SSO service URL** (URL-адрес службы SAML 2.0 SSO проверяющей стороны).</span><span class="sxs-lookup"><span data-stu-id="f4f47-132">For the **Relying party SAML 2.0 SSO service URL**, paste the `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span></span> <span data-ttu-id="f4f47-133">Замените {tenant} на имя вашего клиента (например, contosob2c.onmicrosoft.com), а {policy} — на имя политики расширений (например, B2C_1A_TrustFrameworkExtensions).</span><span class="sxs-lookup"><span data-stu-id="f4f47-133">Replace {tenant} with your tenant's name (for example, contosob2c.onmicrosoft.com), and replace the {policy} with your extensions policy name (for example, B2C_1A_TrustFrameworkExtensions).</span></span>
    > [!IMPORTANT]
    ><span data-ttu-id="f4f47-134">Именем политики является имя, которое наследуется от политики signup_or_signin. В данном случае это `B2C_1A_TrustFrameworkExtensions`.</span><span class="sxs-lookup"><span data-stu-id="f4f47-134">The policy name  is the one that signup_or_signin policy inherits from, in this case it is: `B2C_1A_TrustFrameworkExtensions`.</span></span>
    ><span data-ttu-id="f4f47-135">Например, URL-адресом может быть https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-135">For example the URL could be:   https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span></span>

    ![URL-адрес службы SAML 2.0 SSO проверяющей стороны](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. <span data-ttu-id="f4f47-137">На странице **Configure Identifiers** (Настройка идентификатора) укажите тот же URL-адрес, нажмите кнопку **Добавить**, чтобы добавить его в список, а затем — **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-137">On the **Configure Identifiers** page, specify the same URL as the previous step, click **Add** to add them to the list, and then click **Next**.</span></span>
    <span data-ttu-id="f4f47-138">![Идентификаторы отношений доверия проверяющей стороны](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-138">![Relying party trust identifiers](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span></span>
9.  <span data-ttu-id="f4f47-139">На странице **Choose Access Control Policy** (Выбрать политику управления доступом) выберите политику и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-139">On the **Choose Access Control Policy** select a policy and click **Next**.</span></span>
    <span data-ttu-id="f4f47-140">![Выбор политики управления доступом](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-140">![Choose Access Control Policy](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span></span>
10.  <span data-ttu-id="f4f47-141">На странице **Ready to Add Trust** (Готовность для добавления отношения доверия) проверьте параметры и нажмите кнопку **Далее**, чтобы сохранить сведения об отношении доверия с проверяющей стороной.</span><span class="sxs-lookup"><span data-stu-id="f4f47-141">On the **Ready to Add Trust** page, review the settings, and then click **Next** to save your relying party trust information.</span></span>
    <span data-ttu-id="f4f47-142">![Сохранение сведений об отношении доверия с проверяющей стороной](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-142">![Save your relying party trust information](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span></span>
11.  <span data-ttu-id="f4f47-143">На странице **Готово** щелкните **Закрыть**. При этом автоматически откроется диалоговое окно **Edit Claim Rules** (Изменение правил утверждений).</span><span class="sxs-lookup"><span data-stu-id="f4f47-143">On the **Finish** page, click **Close**, this action automatically displays the **Edit Claim Rules** dialog box.</span></span>
    <span data-ttu-id="f4f47-144">![Изменение правил утверждений](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-144">![Edit Claim Rules](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span></span>
12. <span data-ttu-id="f4f47-145">Щелкните **Добавить правило**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-145">Click **Add Rule**.</span></span>  
      <span data-ttu-id="f4f47-146">![Добавление нового правила](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-146">![Add new rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span></span>
13.  <span data-ttu-id="f4f47-147">В разделе **Claim rule template** (Шаблон правила утверждения) выберите **Send LDAP attributes as claims** (Отправка атрибутов LDAP как утверждений).</span><span class="sxs-lookup"><span data-stu-id="f4f47-147">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
    <span data-ttu-id="f4f47-148">![Выбор шаблона правила "Отправка атрибутов LDAP как утверждений"](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-148">![Select Send LDAP attributes as claims template rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span></span>
14.  <span data-ttu-id="f4f47-149">Укажите **имя правила утверждения**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-149">Provide **Claim rule name**.</span></span> <span data-ttu-id="f4f47-150">В разделе **Attribute store** (Хранилище атрибутов) выберите **Active Directory**, добавьте следующие утверждения, а затем нажмите кнопку **Готово** и **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-150">For the **Attribute store** select **Select Active Directory** Add the following claims, then click **Finish** and **OK**.</span></span>
    <span data-ttu-id="f4f47-151">![Настройка свойств правила](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-151">![Set rule properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span></span>
15.  <span data-ttu-id="f4f47-152">В диспетчере серверов выберите **Relying Party Trusts** (Отношения доверия с проверяющей стороной), а затем выберите созданное отношение доверия с проверяющей стороной и щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-152">In Server Manager, select **Relying Party Trusts** then select the relying party trust you created and click **Properties**.</span></span>
    <span data-ttu-id="f4f47-153">![Изменение свойств проверяющей стороны](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-153">![Relying party edit properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span></span>
16.  <span data-ttu-id="f4f47-154">В окне свойств отношения доверия с проверяющей стороной (демоверсия B2C) перейдите на вкладку **Подпись** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-154">One the relying party trust (B2C Demo) properties window click **Signature** tab and click **Add**.</span></span>  
    <span data-ttu-id="f4f47-155">![Настройка подписи](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-155">![Set signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span></span>
17.  <span data-ttu-id="f4f47-156">Добавьте сертификат подписи (CERT-файл без закрытого ключа).</span><span class="sxs-lookup"><span data-stu-id="f4f47-156">Add your signature certificate (.cert file, without private key).</span></span>  
    ![Добавление сертификата подписи](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  <span data-ttu-id="f4f47-158">В окне свойств отношения доверия с проверяющей стороной (демоверсия B2C) перейдите на вкладку **Дополнительно**, измените **алгоритм SHA** на **SHA-1** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-158">On the relying party trust (B2C Demo) properties window click **Advanced** tab and change the **Secure hash algorithm** to **SHA-1**, Click **Ok**.</span></span>  
    <span data-ttu-id="f4f47-159">![Изменение алгоритма SHA на SHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-159">![Set secure hash algorithm to SHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span></span>

## <a name="add-the-adfs-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="f4f47-160">Добавление ключа приложения учетной записи ADFS в Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="f4f47-160">Add the ADFS account application key to Azure AD B2C</span></span>
<span data-ttu-id="f4f47-161">Для федерации с учетными записями ADFS требуется секрет клиента учетной записи ADFS, чтобы доверять Azure AD B2C от имени приложения.</span><span class="sxs-lookup"><span data-stu-id="f4f47-161">Federation with ADFS accounts requires a client secret for ADFS account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="f4f47-162">Вам необходимо сохранить сертификат ADFS в клиенте Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f4f47-162">You need to store your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1.  <span data-ttu-id="f4f47-163">Перейдите к клиенту Azure AD B2C и выберите **B2C Settings** (Параметры B2C)  > **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-163">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="f4f47-164">Выберите **Policy Keys** (Ключи политики), чтобы просмотреть доступные в клиенте ключи.</span><span class="sxs-lookup"><span data-stu-id="f4f47-164">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="f4f47-165">Щелкните **+Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-165">Click **+Add**.</span></span>
4.  <span data-ttu-id="f4f47-166">В пункте **Параметры** используйте вариант **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-166">For **Options**, use **Upload**.</span></span>
5.  <span data-ttu-id="f4f47-167">Для параметра **Имя** используйте значение `ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="f4f47-167">For **Name**, use `ADFSSamlCert`.</span></span>  
    <span data-ttu-id="f4f47-168">Префикс `B2C_1A_` может быть добавлен автоматически.</span><span class="sxs-lookup"><span data-stu-id="f4f47-168">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="f4f47-169">В поле "Отправка файлов" выберите PFX-файл сертификата с закрытым ключом.</span><span class="sxs-lookup"><span data-stu-id="f4f47-169">In the File upload,** select your certificate .pfx file with private key.</span></span> <span data-ttu-id="f4f47-170">Примечание. Это должен быть сертификат (с закрытым ключом), выданный и использованный для проверяющей стороны ADFS.</span><span class="sxs-lookup"><span data-stu-id="f4f47-170">Note: this certificate (with the private key) should be the same one that issued and used for the ADFS relying party.</span></span>
<span data-ttu-id="f4f47-171">![Отправка ключа политики](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span><span class="sxs-lookup"><span data-stu-id="f4f47-171">![Upload policy key](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span></span>
7.  <span data-ttu-id="f4f47-172">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="f4f47-172">Click **Create**</span></span>
8.  <span data-ttu-id="f4f47-173">Убедитесь, что вы создали ключ `B2C_1A_ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="f4f47-173">Confirm that you've created the key `B2C_1A_ADFSSamlCert`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="f4f47-174">Добавление поставщика утверждений в политику расширения</span><span class="sxs-lookup"><span data-stu-id="f4f47-174">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="f4f47-175">Чтобы пользователи выполняли вход с помощью учетной записи ADFS, необходимо определить учетную запись ADFS в качестве поставщика утверждений.</span><span class="sxs-lookup"><span data-stu-id="f4f47-175">If you want users to sign in by using ADFS account, you need to define ADFS account as a claims provider.</span></span> <span data-ttu-id="f4f47-176">Другими словами, необходимо указать конечную точку, с которой взаимодействует Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f4f47-176">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="f4f47-177">Конечная точка предоставляет набор утверждений, используемых Azure AD B2C, чтобы проверить, была ли выполнена проверка подлинности определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="f4f47-177">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="f4f47-178">Определите ADFS в качестве поставщика утверждений, добавив узел `<ClaimsProvider>` в файл политики расширения.</span><span class="sxs-lookup"><span data-stu-id="f4f47-178">Define ADFS as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="f4f47-179">Откройте файл политики расширения (TrustFrameworkExtensions.xml) из рабочего каталога.</span><span class="sxs-lookup"><span data-stu-id="f4f47-179">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="f4f47-180">Если вам нужен редактор XML, [попробуйте Visual Studio Code](https://code.visualstudio.com/download) — упрощенный кроссплатформенный редактор.</span><span class="sxs-lookup"><span data-stu-id="f4f47-180">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="f4f47-181">Найдите раздел `<ClaimsProviders>`.</span><span class="sxs-lookup"><span data-stu-id="f4f47-181">Find the `<ClaimsProviders>` section</span></span>
3. <span data-ttu-id="f4f47-182">Добавьте следующий фрагмент XML-кода в элемент `ClaimsProviders`, замените `identityProvider` на DNS (произвольное значение, указывающее домен) и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="f4f47-182">Add the following XML snippet under the `ClaimsProviders` element and replace `identityProvider` with your DNS (Arbitrary value that indicates your domain), and save the file.</span></span> 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-the-adfs-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="f4f47-183">Регистрация поставщика утверждений учетной записи ADFS для пути взаимодействия пользователя "Регистрация" или "Вход"</span><span class="sxs-lookup"><span data-stu-id="f4f47-183">Register the ADFS account claims provider to Sign up or Sign in user journey</span></span>
<span data-ttu-id="f4f47-184">На этом этапе поставщик удостоверений настроен.</span><span class="sxs-lookup"><span data-stu-id="f4f47-184">At this point, the identity provider has been set up.</span></span>  <span data-ttu-id="f4f47-185">Однако он недоступен ни на одном из экранов регистрации или входа.</span><span class="sxs-lookup"><span data-stu-id="f4f47-185">However, it is not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="f4f47-186">Теперь необходимо добавить поставщик удостоверений учетной записи ADFS для пути взаимодействия пользователя `SignUpOrSignIn`.</span><span class="sxs-lookup"><span data-stu-id="f4f47-186">Now you need to add the ADFS account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="f4f47-187">Чтобы сделать его доступным, необходимо создать дубликат имеющегося шаблона пути взаимодействия пользователя,</span><span class="sxs-lookup"><span data-stu-id="f4f47-187">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="f4f47-188">а затем изменить его таким образом, чтобы он содержал поставщик удостоверений ADFS.</span><span class="sxs-lookup"><span data-stu-id="f4f47-188">Then, we modify it so it includes the ADFS identity provider:</span></span>
    >[!NOTE]
    >If you previously copied the `<UserJourneys>` element from base file of your policy to the extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  <span data-ttu-id="f4f47-189">Откройте базовый файл политики (например, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="f4f47-189">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="f4f47-190">Найдите элемент `<UserJourneys>` и скопируйте все содержимое узла `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="f4f47-190">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="f4f47-191">Откройте файл расширения (например, TrustFrameworkExtensions.xml) и найдите элемент `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="f4f47-191">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="f4f47-192">Если элемент не существует, добавьте его.</span><span class="sxs-lookup"><span data-stu-id="f4f47-192">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="f4f47-193">Вставьте весь скопированный узел `<UserJournesy>` как дочерний узел элемента `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="f4f47-193">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="f4f47-194">Отображение кнопки</span><span class="sxs-lookup"><span data-stu-id="f4f47-194">Display the button</span></span>
<span data-ttu-id="f4f47-195">Элемент `<ClaimsProviderSelections>` определяет список параметров выбора поставщика утверждений и их порядок.</span><span class="sxs-lookup"><span data-stu-id="f4f47-195">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="f4f47-196">Элемент `<ClaimsProviderSelection>` является аналогом кнопки поставщика удостоверений на странице регистрации или входа.</span><span class="sxs-lookup"><span data-stu-id="f4f47-196">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="f4f47-197">Если вы добавите для учетной записи ADFS элемент `<ClaimsProviderSelection>`, при переходе пользователя на страницу отобразится новая кнопка.</span><span class="sxs-lookup"><span data-stu-id="f4f47-197">If you add a `<ClaimsProviderSelection>` element for  ADFS account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="f4f47-198">Для этого:</span><span class="sxs-lookup"><span data-stu-id="f4f47-198">To add this element:</span></span>

1.  <span data-ttu-id="f4f47-199">Найдите узел `<UserJourney>`, содержащий `Id="SignUpOrSignIn"` в скопированном пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="f4f47-199">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="f4f47-200">Найдите узел `<OrchestrationStep>`, содержащий `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="f4f47-200">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="f4f47-201">Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="f4f47-201">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-the-button-to-an-action"></a><span data-ttu-id="f4f47-202">Связывание кнопки с действием</span><span class="sxs-lookup"><span data-stu-id="f4f47-202">Link the button to an action</span></span>

<span data-ttu-id="f4f47-203">Теперь, когда у вас есть кнопка, вам необходимо связать ее с действием.</span><span class="sxs-lookup"><span data-stu-id="f4f47-203">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="f4f47-204">В этом случае действие — это возможность взаимодействия Azure AD B2C с учетной записью ADFS для получения маркера.</span><span class="sxs-lookup"><span data-stu-id="f4f47-204">The action, in this case, is for Azure AD B2C to communicate with ADFS account to receive a token.</span></span> <span data-ttu-id="f4f47-205">Свяжите кнопку с действием, связав технический профиль для поставщика утверждений учетной записи ADFS.</span><span class="sxs-lookup"><span data-stu-id="f4f47-205">Link the button to an action by linking the technical profile for your ADFS account claims provider:</span></span>

1.  <span data-ttu-id="f4f47-206">Найдите `<OrchestrationStep>`, который содержит `Order="2"` в узле `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="f4f47-206">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="f4f47-207">Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="f4f47-207">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * <span data-ttu-id="f4f47-208">Убедитесь, что `Id` имеет то же значение, что и `TargetClaimsExchangeId` в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="f4f47-208">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
> * <span data-ttu-id="f4f47-209">Убедитесь, что для `TechnicalProfileReferenceId` задан ранее созданный технический профиль (Contoso-SAML2).</span><span class="sxs-lookup"><span data-stu-id="f4f47-209">Ensure `TechnicalProfileReferenceId` is set to the technical profile you created earlier (Contoso-SAML2).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="f4f47-210">Отправка политики в клиент</span><span class="sxs-lookup"><span data-stu-id="f4f47-210">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="f4f47-211">На [портале Azure](https://portal.azure.com) переключитесь в [контекст клиента Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md) и откройте колонку **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-211">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="f4f47-212">Выберите **Инфраструктура процедур идентификации**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-212">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="f4f47-213">Откройте колонку **Все политики**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-213">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="f4f47-214">Щелкните **Отправить политику**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-214">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="f4f47-215">Установите флажок **Перезаписать политику, если она существует**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-215">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="f4f47-216">**Отправьте** файл TrustFrameworkExtensions.xml и немного подождите, чтобы удостовериться в отсутствии сбоя при проверке.</span><span class="sxs-lookup"><span data-stu-id="f4f47-216">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="f4f47-217">Тестирование настраиваемой политики с помощью команды "Запустить сейчас"</span><span class="sxs-lookup"><span data-stu-id="f4f47-217">Test the custom policy by using Run Now</span></span>
1.  <span data-ttu-id="f4f47-218">Откройте **Параметры Azure AD B2C** и перейдите к элементу **Инфраструктура процедур идентификации**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-218">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="f4f47-219">Откройте **B2C_1A_signup_signin**, отправленную вами пользовательскую политику проверяющей стороны.</span><span class="sxs-lookup"><span data-stu-id="f4f47-219">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="f4f47-220">Выберите **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-220">Select **Run now**.</span></span>
3.  <span data-ttu-id="f4f47-221">Вы можете войти с использованием учетной записи ADFS.</span><span class="sxs-lookup"><span data-stu-id="f4f47-221">You should be able to sign in using ADFS account.</span></span>

## <a name="optional-register-the-adfs-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="f4f47-222">[Необязательно] Регистрация поставщика утверждений учетной записи ADFS для пути взаимодействия пользователя "Изменение профиля"</span><span class="sxs-lookup"><span data-stu-id="f4f47-222">[Optional] Register the ADFS account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="f4f47-223">Вы также можете добавить поставщик удостоверений учетной записи ADFS для пути взаимодействия пользователя `ProfileEdit`.</span><span class="sxs-lookup"><span data-stu-id="f4f47-223">You may want to add the ADFS account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="f4f47-224">Чтобы сделать его доступным, необходимо повторить последние два шага:</span><span class="sxs-lookup"><span data-stu-id="f4f47-224">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="f4f47-225">Отображение кнопки</span><span class="sxs-lookup"><span data-stu-id="f4f47-225">Display the button</span></span>
1.  <span data-ttu-id="f4f47-226">Откройте файл расширения политики (например, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="f4f47-226">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="f4f47-227">Найдите узел `<UserJourney>`, содержащий `Id="ProfileEdit"` в скопированном пути пользователя.</span><span class="sxs-lookup"><span data-stu-id="f4f47-227">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="f4f47-228">Найдите узел `<OrchestrationStep>`, содержащий `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="f4f47-228">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="f4f47-229">Добавьте в узел `<ClaimsProviderSelections>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="f4f47-229">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="f4f47-230">Связывание кнопки с действием</span><span class="sxs-lookup"><span data-stu-id="f4f47-230">Link the button to an action</span></span>
1.  <span data-ttu-id="f4f47-231">Найдите `<OrchestrationStep>`, который содержит `Order="2"` в узле `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="f4f47-231">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="f4f47-232">Добавьте в узел `<ClaimsExchanges>` следующий фрагмент XML-кода:</span><span class="sxs-lookup"><span data-stu-id="f4f47-232">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="f4f47-233">Тестирование пользовательской политики изменения профиля с помощью команды "Запустить сейчас"</span><span class="sxs-lookup"><span data-stu-id="f4f47-233">Test the custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="f4f47-234">Откройте **Параметры Azure AD B2C** и перейдите к элементу **Инфраструктура процедур идентификации**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-234">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="f4f47-235">Откройте **B2C_1A_ProfileEdit**, отправленную пользовательскую политику проверяющей стороны.</span><span class="sxs-lookup"><span data-stu-id="f4f47-235">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="f4f47-236">Выберите **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="f4f47-236">Select **Run now**.</span></span>
3.  <span data-ttu-id="f4f47-237">Вы можете войти с использованием учетной записи ADFS.</span><span class="sxs-lookup"><span data-stu-id="f4f47-237">You should be able to sign in using ADFS account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="f4f47-238">Загрузка завершенных файлов политики</span><span class="sxs-lookup"><span data-stu-id="f4f47-238">Download the complete policy files</span></span>
<span data-ttu-id="f4f47-239">Необязательно. Мы советуем создать свой сценарий, используя собственные файлы пользовательской политики, после того как вы ознакомитесь с пошаговым руководством по началу работы с пользовательскими политиками.</span><span class="sxs-lookup"><span data-stu-id="f4f47-239">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through.</span></span> [<span data-ttu-id="f4f47-240">Файлы примеров политики, предназначенные только для справки</span><span class="sxs-lookup"><span data-stu-id="f4f47-240">Policy sample files for reference only</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
