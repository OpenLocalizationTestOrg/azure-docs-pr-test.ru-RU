---
title: "aaaProtect персональные данные с помощью Azure элементов управления доступом и удостоверениями | Документы Microsoft"
description: "С помощью элементов управления доступом и удостоверениями Azure toohelp защиты личных данных"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a><span data-ttu-id="13f61-103">Azure Active Directory и Многофакторная идентификация. Защита персональных данных с помощью управления удостоверениями и доступом</span><span class="sxs-lookup"><span data-stu-id="13f61-103">Azure Active Directory and Multi-Factor Authentication: Protect personal data with identity and access controls</span></span>

<span data-ttu-id="13f61-104">Эта статья содержит сведения и процедуры, можно использовать tooprotect персональные данные с помощью служб и функций безопасности проверки подлинности Azure Active Directory и многофакторной.</span><span class="sxs-lookup"><span data-stu-id="13f61-104">This article provides information and procedures you can use tooprotect personal data using Azure Active Directory and Multi-factor authentication security features and services.</span></span>

## <a name="scenario"></a><span data-ttu-id="13f61-105">Сценарий</span><span class="sxs-lookup"><span data-stu-id="13f61-105">Scenario</span></span>

<span data-ttu-id="13f61-106">Компании больших прогулка по, рядом с офисом в Соединенных Штатах Америки hello, развернут расписаниям toooffer его операций в морская hello, Adriatic и Балтийский компании seas, а также Британские острова hello.</span><span class="sxs-lookup"><span data-stu-id="13f61-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="13f61-107">toosupport эти усилия, он получил несколько небольших строк прогулка по в Италии, Германии, Дания и hello Великобритания</span><span class="sxs-lookup"><span data-stu-id="13f61-107">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="13f61-108">Hello компания использует Microsoft Azure toostore корпоративных данных в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="13f61-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="13f61-109">Сюда входят персональные данные, позволяющие установить личность, например имена, адреса, номера телефонов и данные кредитной карты в глобальной клиентской базе.</span><span class="sxs-lookup"><span data-stu-id="13f61-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="13f61-110">Он также включает традиционные информацию о персонале, например адреса, номера телефонов, идентификационные номера налога и медицинские сведения о сотрудниках компании во всех расположениях.</span><span class="sxs-lookup"><span data-stu-id="13f61-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="13f61-111">Строка Hello прогулка по также хранится большой базы данных вознаграждения и постоянных элементов программы, содержат персональные данные tootrack связи с клиентами, текущие и прошлые.</span><span class="sxs-lookup"><span data-stu-id="13f61-111">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="13f61-112">Сотрудники предприятий сети hello доступ из удаленных офисов и путешествий hello компании расположены по всему Здравствуй, мир! имеют доступ к ресурсам компании toosome.</span><span class="sxs-lookup"><span data-stu-id="13f61-112">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="13f61-113">Проблема</span><span class="sxs-lookup"><span data-stu-id="13f61-113">Problem statement</span></span>

<span data-ttu-id="13f61-114">Hello компании должны защищать hello конфиденциальность личных данных сотрудников и клиентов от злоумышленников, пытается получить доступ toogain удостоверения toouse скомпрометирован.</span><span class="sxs-lookup"><span data-stu-id="13f61-114">hello company must protect hello privacy of customers’ and employees’ personal data from attackers seeking toouse compromised identities toogain access.</span></span> <span data-ttu-id="13f61-115">Они также необходимо убедиться, toopersonal доступ, данные по законных пользователей предназначен только для тех, кому она нужна toodo свою работу.</span><span class="sxs-lookup"><span data-stu-id="13f61-115">They also must ensure that access toopersonal data by legitimate users is restricted to only those who need it toodo their jobs.</span></span>

## <a name="company-goal"></a><span data-ttu-id="13f61-116">Цель компании</span><span class="sxs-lookup"><span data-stu-id="13f61-116">Company goal</span></span>

<span data-ttu-id="13f61-117">Цель компании Hello — tooensure, доступ к данным toopersonal строгий контроль.</span><span class="sxs-lookup"><span data-stu-id="13f61-117">hello company’s goal is tooensure that access toopersonal data is strictly controlled.</span></span> <span data-ttu-id="13f61-118">Очень важно, чтобы удостоверений пользователей с toopersonal доступа к данным был защищен строгой проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="13f61-118">It is essential that identities of users with access toopersonal data be protected by strong authentication.</span></span> <span data-ttu-id="13f61-119">Политика [наименьших прав доступа] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) необходимо обеспечить, чтобы законных пользователей имеют только уровень hello получают доступ и больше не требуется.</span><span class="sxs-lookup"><span data-stu-id="13f61-119">A policy of [least privilege] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) must be enforced so that legitimate users have only hello level of  access they need, and no more.</span></span>

## <a name="solutions"></a><span data-ttu-id="13f61-120">Решения</span><span class="sxs-lookup"><span data-stu-id="13f61-120">Solutions</span></span>

<span data-ttu-id="13f61-121">Microsoft Azure предоставляет средства управления удостоверениями и доступом toohelp компаний контролировать, кто имеет доступ tooresources, содержат личные данные.</span><span class="sxs-lookup"><span data-stu-id="13f61-121">Microsoft Azure provides identity and access management tools toohelp companies control who has access tooresources that contain personal data.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="13f61-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="13f61-122">Azure Active Directory</span></span>

<span data-ttu-id="13f61-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) управляет идентификаторами и управляет доступом tooAzure, а также для других локальных и другие облачные ресурсы, данным и приложениям.</span><span class="sxs-lookup"><span data-stu-id="13f61-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) manages identities and controls access tooAzure as well as other on-premises and other cloud resources, data, and applications.</span></span> <span data-ttu-id="13f61-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) помогает администраторам Azure toominimize hello количество людей, имеющих доступ к сведениям toocertain, например личные данные.</span><span class="sxs-lookup"><span data-stu-id="13f61-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helps Azure administrators toominimize hello number of people who have access toocertain information such as personal data.</span></span> <span data-ttu-id="13f61-125">Позволяет им toodiscover, ограничения и мониторинг привилегированных удостоверений и доступа к tooresources и tooassign временным, JIT – JIT права администратора tooeligible пользователей.</span><span class="sxs-lookup"><span data-stu-id="13f61-125">It enables them toodiscover, restrict, and monitor privileged identities and their access tooresources, and tooassign temporary, Just-In-Time (JIT) administrative rights tooeligible users.</span></span> <span data-ttu-id="13f61-126">Она также предоставляет сведения о пользователях, имеющих права администратора AAD.</span><span class="sxs-lookup"><span data-stu-id="13f61-126">It also provides insight into those who have AAD administrative privileges.</span></span>

<span data-ttu-id="13f61-127">Hello действия, связанные с использованием AAD PIM включают:</span><span class="sxs-lookup"><span data-stu-id="13f61-127">hello activities involved in using AAD PIM include:</span></span>

- <span data-ttu-id="13f61-128">включение управления привилегированными пользователями для каталога;</span><span class="sxs-lookup"><span data-stu-id="13f61-128">Enabling Privileged Identity Management for your directory</span></span>

- <span data-ttu-id="13f61-129">С помощью управления привилегированными пользователями admin toosee важные сведения о панели мониторинга с первого взгляда</span><span class="sxs-lookup"><span data-stu-id="13f61-129">Using Privileged Identity Management admin dashboard toosee important information at a glance</span></span>

- <span data-ttu-id="13f61-130">Управление удостоверениями hello работы в привилегированном режиме (Администраторы), добавив или удалив роли администраторов постоянными или соответствующими условиям tooeach</span><span class="sxs-lookup"><span data-stu-id="13f61-130">Managing hello privileged identities (administrators) by adding or removing permanent or eligible administrators tooeach role</span></span>

- <span data-ttu-id="13f61-131">Настройка параметров активации роли hello</span><span class="sxs-lookup"><span data-stu-id="13f61-131">Configuring hello role activation settings</span></span>

- <span data-ttu-id="13f61-132">активация ролей;</span><span class="sxs-lookup"><span data-stu-id="13f61-132">Activating roles</span></span>

- <span data-ttu-id="13f61-133">просмотр активности роли.</span><span class="sxs-lookup"><span data-stu-id="13f61-133">Reviewing role activity</span></span>

#### <a name="how-do-i-enable-aad-pim"></a><span data-ttu-id="13f61-134">Включение AAD PIM</span><span class="sxs-lookup"><span data-stu-id="13f61-134">How do I enable AAD PIM?</span></span>

<span data-ttu-id="13f61-135">с помощью PIM для вашего каталога toostart hello следующие:</span><span class="sxs-lookup"><span data-stu-id="13f61-135">toostart using PIM for your directory, do hello following:</span></span>

1. <span data-ttu-id="13f61-136">Войдите в toohello портал Azure как глобальный администратор каталога.</span><span class="sxs-lookup"><span data-stu-id="13f61-136">Sign in toohello Azure portal as a global administrator of your directory.</span></span>

2. <span data-ttu-id="13f61-137">Если ваша организация имеет несколько каталогов, выберите свое имя пользователя в верхнем правом углу hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="13f61-137">If your organization has more than one directory, select your username in hello upper right-hand corner of hello Azure portal.</span></span> <span data-ttu-id="13f61-138">Выберите каталог hello, где будет использовать Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="13f61-138">Select hello directory where you will use Azure AD Privileged Identity Management.</span></span>

3. <span data-ttu-id="13f61-139">Выберите **дополнительные службы** и использовать hello **фильтра** toosearch textbox для Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="13f61-139">Select **More services** and use hello **Filter** textbox toosearch for Azure AD Privileged Identity Management.</span></span>

4. <span data-ttu-id="13f61-140">Проверьте **toodashboard ПИН-код** и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="13f61-140">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="13f61-141">Открывает Hello управления привилегированными пользователями приложения.</span><span class="sxs-lookup"><span data-stu-id="13f61-141">hello Privileged Identity Management application opens.</span></span>

<span data-ttu-id="13f61-142">После настройки Azure AD Privileged Identity Management вы видите колонке навигации hello каждый раз при открытии приложения hello.</span><span class="sxs-lookup"><span data-stu-id="13f61-142">Once Azure AD Privileged Identity Management is set up, you see hello navigation blade whenever you open hello application.</span></span>

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

<span data-ttu-id="13f61-143">Дополнительные сведения и инструкции по началу работы с AAD PIM см. в статье [Приступая к использованию Azure AD Privileged Identity Management](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started).</span><span class="sxs-lookup"><span data-stu-id="13f61-143">For more information and instructions on getting started with AAD PIM, see [Start Using Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span></span>

### <a name="azure-role-based-access-control"></a><span data-ttu-id="13f61-144">Управление доступом на основе ролей в Azure</span><span class="sxs-lookup"><span data-stu-id="13f61-144">Azure Role-based Access Control</span></span>

<span data-ttu-id="13f61-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) помогает управлять ресурсами tooAzure доступа, позволяя hello предоставление доступа на основе назначенного роли пользователя hello администраторов Azure.</span><span class="sxs-lookup"><span data-stu-id="13f61-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helps Azure administrators manage access tooAzure resources by enabling hello granting of access based on hello user’s assigned role.</span></span> <span data-ttu-id="13f61-146">Можно разделить обязанностей в команде и предоставить только hello объем toousers доступа, группы и приложения, что они должны tooperform свою работу.</span><span class="sxs-lookup"><span data-stu-id="13f61-146">You can segregate duties within a team and grant only hello amount of access toousers, groups and applications that they need tooperform their jobs.</span></span>

<span data-ttu-id="13f61-147">С помощью портала Azure hello, средств командной строки Azure или API управления Azure toousers может быть предоставлен доступ, на основе ролей.</span><span class="sxs-lookup"><span data-stu-id="13f61-147">Role-based access can be granted toousers using hello Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

<span data-ttu-id="13f61-148">Дополнительные сведения об основах Azure RBAC см. в разделе [приступить к работе с элементом управления доступом на основе ролей в hello портала Azure.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span><span class="sxs-lookup"><span data-stu-id="13f61-148">For more information about Azure RBAC basics, see [Get started with Role-Based Access Control in hello Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span></span>

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a><span data-ttu-id="13f61-149">Управление Azure RBAC с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="13f61-149">How do I manage Azure RBAC with PowerShell?</span></span>

<span data-ttu-id="13f61-150">Можно использовать командлеты PowerShell toomanage RBAC Azure, включая следующие задачи по управлению hello.</span><span class="sxs-lookup"><span data-stu-id="13f61-150">You can use PowerShell cmdlets toomanage Azure RBAC, including hello following management tasks:</span></span>

- <span data-ttu-id="13f61-151">Вывод списка ролей</span><span class="sxs-lookup"><span data-stu-id="13f61-151">List roles</span></span>

- <span data-ttu-id="13f61-152">Увидеть, у кого есть доступ</span><span class="sxs-lookup"><span data-stu-id="13f61-152">See who has access</span></span>

- <span data-ttu-id="13f61-153">Предоставление доступа</span><span class="sxs-lookup"><span data-stu-id="13f61-153">Grant access</span></span>

- <span data-ttu-id="13f61-154">Запрет доступа</span><span class="sxs-lookup"><span data-stu-id="13f61-154">Remove access</span></span>

- <span data-ttu-id="13f61-155">Создание настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="13f61-155">Create a custom role</span></span>

- <span data-ttu-id="13f61-156">Получение действий для поставщика ресурсов</span><span class="sxs-lookup"><span data-stu-id="13f61-156">Get Actions for a Resource Provider</span></span>

- <span data-ttu-id="13f61-157">Изменение настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="13f61-157">Modify a custom role</span></span>

- <span data-ttu-id="13f61-158">Удаление настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="13f61-158">Delete a custom role</span></span>

- <span data-ttu-id="13f61-159">Вывод списка настраиваемых ролей</span><span class="sxs-lookup"><span data-stu-id="13f61-159">List custom roles</span></span>

<span data-ttu-id="13f61-160">Инструкции по toomanage RBAC Azure с помощью PowerShell, в статье [управление доступом на основе с помощью Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span><span class="sxs-lookup"><span data-stu-id="13f61-160">For instructions on how toomanage Azure RBAC with PowerShell, see [Manage Role-based Access with Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span></span>

### <a name="azure-multi-factor-authentication"></a><span data-ttu-id="13f61-161">Многофакторная идентификация Microsoft Azure;</span><span class="sxs-lookup"><span data-stu-id="13f61-161">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="13f61-162">[Azure Multi-factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) — двухэтапный проверки решение toodata защиты доступа и приложений, удовлетворением спроса на простой процесс входа в систему.</span><span class="sxs-lookup"><span data-stu-id="13f61-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is a two-step verification solution that helps safeguard access toodata and applications, while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="13f61-163">Служба обеспечивает строгую аутентификацию с помощью различных способов проверки — телефонного звонка, текстового сообщения или проверки в мобильном приложении.</span><span class="sxs-lookup"><span data-stu-id="13f61-163">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

<span data-ttu-id="13f61-164">toodeploy многофакторной проверки Подлинности в облаке Azure hello необходимо toofirst использовать ее, а затем включить двухшаговую проверку для пользователей.</span><span class="sxs-lookup"><span data-stu-id="13f61-164">toodeploy MFA in hello Azure cloud, you need toofirst enable it and then turn on two-step verification for users.</span></span>

#### <a name="how-do-i-enable-azure-toouse-mfa"></a><span data-ttu-id="13f61-165">Как включить Azure toouse MFA?</span><span class="sxs-lookup"><span data-stu-id="13f61-165">How do I enable Azure toouse MFA?</span></span>

<span data-ttu-id="13f61-166">Если у пользователей есть лицензии, которые включают многофакторной проверки подлинности Azure, что нет требуются tooturn toodo на многофакторной проверки Подлинности Azure.</span><span class="sxs-lookup"><span data-stu-id="13f61-166">If your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="13f61-167">В противном случае необходимо toocreate поставщик многофакторной проверки подлинности в вашем каталоге.</span><span class="sxs-lookup"><span data-stu-id="13f61-167">If not, you need toocreate a Multi-Factor Auth provider in your directory.</span></span> <span data-ttu-id="13f61-168">toodo это, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="13f61-168">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="13f61-169">Выберите **Active Directory** в hello Azure классического портала (войти в систему как администратор).</span><span class="sxs-lookup"><span data-stu-id="13f61-169">Select **Active Directory** in hello Azure classic portal (logged on as an administrator).</span></span>

2. <span data-ttu-id="13f61-170">Выберите **поставщиков Многофакторной идентификации**.</span><span class="sxs-lookup"><span data-stu-id="13f61-170">Select **Multi-Factor Authentication Providers.**</span></span>

3. <span data-ttu-id="13f61-171">Выберите **Создать**, а затем в разделе **Службы приложений** щелкните **Поставщик многофакторной проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="13f61-171">Select **New,** and then under **App Services,** select **Multi-Factor Auth Provider.**</span></span>

4. <span data-ttu-id="13f61-172">Выберите **Быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="13f61-172">Select **Quick Create.**</span></span>

5. <span data-ttu-id="13f61-173">Заполните поле имени hello и модель использования (на проверку подлинности или каждого включенного пользователя).</span><span class="sxs-lookup"><span data-stu-id="13f61-173">Fill in hello name field and select a usage model (per authentication or per enabled user).</span></span>

6. <span data-ttu-id="13f61-174">Задается каталог, с которой hello связан поставщик многофакторной проверки Подлинности.</span><span class="sxs-lookup"><span data-stu-id="13f61-174">Designate a directory with which hello MFA Provider is associated.</span></span>

7. <span data-ttu-id="13f61-175">Нажмите кнопку hello **создать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="13f61-175">Click hello **Create** button.</span></span>

![](media/protect-personal-data-identity-access-controls/quick-create.png)

<span data-ttu-id="13f61-176">Дополнительные сведения о том, как toomanage поставщик многофакторной проверки подлинности. в разделе [Приступая к работе с поставщик многофакторной проверки подлинности Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span><span class="sxs-lookup"><span data-stu-id="13f61-176">For more instructions on how toomanage your Multi-Factor Auth Provider, see [Getting Started with an Azure Multi-Factor Auth Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span></span>

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a><span data-ttu-id="13f61-177">Включение двухфакторной проверки подлинности для пользователей</span><span class="sxs-lookup"><span data-stu-id="13f61-177">How do I turn on two-step verification for users?</span></span>

<span data-ttu-id="13f61-178">Вы можете применять двухшаговую проверку для всех входов или проверки двухэтапный toorequire политики условного доступа можно создать только при выполнении определенных условий.</span><span class="sxs-lookup"><span data-stu-id="13f61-178">You can enforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when specific conditions apply.</span></span>

<span data-ttu-id="13f61-179">Включение многофакторной проверки Подлинности Azure путем изменения состояния пользователя является hello традиционный подход, когда требуется двухшаговую проверку.</span><span class="sxs-lookup"><span data-stu-id="13f61-179">Enabling Azure MFA by changing user states is hello traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="13f61-180">Все пользователи hello, включении будут иметь hello же требование tooperform двухшаговую проверку, каждый раз при входе.</span><span class="sxs-lookup"><span data-stu-id="13f61-180">All hello users that you enable will have hello same requirement tooperform two-step verification every time they sign in.</span></span> <span data-ttu-id="13f61-181">Включение такой аутентификации для пользователя переопределяет любые политики условного доступа, которые могут действовать для него.</span><span class="sxs-lookup"><span data-stu-id="13f61-181">Enabling a user overrides any conditional access policies that may affect that user.</span></span>

<span data-ttu-id="13f61-182">Включение Azure MFA с политикой условного доступа — это более гибкий подход к применению двухфакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="13f61-182">Enabling Azure MFA with a conditional access policy is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="13f61-183">Можно создать политики условного доступа, применяемые toogroups, а также для отдельных пользователей.</span><span class="sxs-lookup"><span data-stu-id="13f61-183">You can create conditional access policies that apply toogroups as well as individual users.</span></span> <span data-ttu-id="13f61-184">Для групп с высоким риском можно задать больше ограничений, чем для групп с низким риском. Или вы можете сделать двухфакторную проверку подлинности обязательной только для облачных приложений с высоким риском, пропуская ее для приложений с низким риском.</span><span class="sxs-lookup"><span data-stu-id="13f61-184">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> <span data-ttu-id="13f61-185">Однако условный доступ — это платная функция Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="13f61-185">However, conditional access is a paid feature of Azure Active Directory.</span></span>

<span data-ttu-id="13f61-186">tooenable многофакторной проверки Подлинности, изменяя состояние пользователя hello следующие:</span><span class="sxs-lookup"><span data-stu-id="13f61-186">tooenable MFA by changing user state, do hello following:</span></span>

1. <span data-ttu-id="13f61-187">Войдите в toohello портал Azure с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="13f61-187">Sign in toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="13f61-188">Go слишком**Azure Active Directory \> пользователей и групп \> всех пользователей**.</span><span class="sxs-lookup"><span data-stu-id="13f61-188">Go too**Azure Active Directory \> Users and groups \> All users**.</span></span>
3. <span data-ttu-id="13f61-189">Выберите **Многофакторная идентификация**.</span><span class="sxs-lookup"><span data-stu-id="13f61-189">Select **Multi-Factor Authentication**.</span></span>
4. <span data-ttu-id="13f61-190">Найти hello пользователя требуется tooenable многофакторной проверки подлинности Azure.</span><span class="sxs-lookup"><span data-stu-id="13f61-190">Find hello user that you want tooenable for Azure MFA.</span></span> <span data-ttu-id="13f61-191">Может потребоваться toochange hello в верхней hello.</span><span class="sxs-lookup"><span data-stu-id="13f61-191">You may need toochange hello view at hello top.</span></span>
5. <span data-ttu-id="13f61-192">Проверьте имя hello поле Далее toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="13f61-192">Check hello box next toohello user’s name.</span></span>
6. <span data-ttu-id="13f61-193">В hello справа в списке быстрых действий, выберите **включить**.</span><span class="sxs-lookup"><span data-stu-id="13f61-193">On hello right, under quick steps, choose **Enable**.</span></span>

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. <span data-ttu-id="13f61-194">Подтвердите свой выбор в открывшемся всплывающем окне hello.</span><span class="sxs-lookup"><span data-stu-id="13f61-194">Confirm your selection in hello pop-up window that opens.</span></span>  <span data-ttu-id="13f61-195">Пользователи, для которых включена многофакторной проверки Подлинности будет выведено tooregister hello при очередном входе.</span><span class="sxs-lookup"><span data-stu-id="13f61-195">Users for whom MFA has been enabled will be asked tooregister hello next time they sign in.</span></span>

<span data-ttu-id="13f61-196">tooenable многофакторной проверки Подлинности Azure с помощью политики условного доступа hello следующие:</span><span class="sxs-lookup"><span data-stu-id="13f61-196">tooenable Azure MFA with a conditional access policy, do hello following:</span></span>

1. <span data-ttu-id="13f61-197">Войдите в toohello портал Azure с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="13f61-197">Sign in toohello Azure portal as an administrator.</span></span>

2. <span data-ttu-id="13f61-198">Go слишком**Azure Active Directory \> условного доступа**.</span><span class="sxs-lookup"><span data-stu-id="13f61-198">Go too**Azure Active Directory \> Conditional access**.</span></span>

3. <span data-ttu-id="13f61-199">Выберите **Новая политика**.</span><span class="sxs-lookup"><span data-stu-id="13f61-199">Select **New policy**.</span></span>

4. <span data-ttu-id="13f61-200">В разделе **Назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="13f61-200">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="13f61-201">Используйте hello **Include** и **исключить** вкладки toospecify, какие пользователи и группы будут управляться с помощью политики hello.</span><span class="sxs-lookup"><span data-stu-id="13f61-201">Use hello **Include** and     **Exclude** tabs toospecify which users and groups will be managed by hello policy.</span></span>

5. <span data-ttu-id="13f61-202">В разделе **Назначения** выберите **Облачные приложения**.</span><span class="sxs-lookup"><span data-stu-id="13f61-202">Under **Assignments**, select **Cloud apps.**</span></span> <span data-ttu-id="13f61-203">Выберите слишком**включают все облачные приложения**.</span><span class="sxs-lookup"><span data-stu-id="13f61-203">Choose too**include All cloud apps**.</span></span>
6.  <span data-ttu-id="13f61-204">В разделе **Элементы управления доступом** выберите **Предоставление**.</span><span class="sxs-lookup"><span data-stu-id="13f61-204">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="13f61-205">Выберите **Требовать многофакторную проверку подлинности**.</span><span class="sxs-lookup"><span data-stu-id="13f61-205">Choose **Require multi-factor authentication**.</span></span>
7.  <span data-ttu-id="13f61-206">Включить **включить политику** слишком**на** , а затем выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="13f61-206">Turn **Enable policy** too**On** and then select **Save**.</span></span>

<span data-ttu-id="13f61-207">Сведения о tooconfigure tooset параметры многофакторной проверки Подлинности Azure предупреждений о мошенничестве создать одноразовый обход проверки, настраиваемых голосовых сообщений, настройте кэширование, укажите надежные IP-адреса, создавать пароли приложений, включение запоминание многофакторной проверки Подлинности для устройств, которым доверяете пользователям и выберите методы проверки в разделе [настроить параметры многофакторной проверки подлинности Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span><span class="sxs-lookup"><span data-stu-id="13f61-207">For information on how tooconfigure Azure MFA settings tooset up fraud alerts, create a one-time bypass, use custom voice messages, configure caching, specify trusted IPs, create app passwords, enable remembering MFA for devices that users trust, and select verification methods, see [Configure Azure Multi-Factor Authentication Settings.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span></span>

## <a name="next-steps"></a><span data-ttu-id="13f61-208">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="13f61-208">Next steps</span></span>

- [<span data-ttu-id="13f61-209">Защита привилегированного доступа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="13f61-209">Securing privileged access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [<span data-ttu-id="13f61-210">Часто задаваемые вопросы о Многофакторной идентификации Azure</span><span class="sxs-lookup"><span data-stu-id="13f61-210">Frequently asked questions about Azure Multi-Factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [<span data-ttu-id="13f61-211">Устранение неполадок при управлении доступом на основе ролей</span><span class="sxs-lookup"><span data-stu-id="13f61-211">Role-based Access Control troubleshooting</span></span>](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [<span data-ttu-id="13f61-212">Защита идентификации Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="13f61-212">Azure Active Directory Identity Protection</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
