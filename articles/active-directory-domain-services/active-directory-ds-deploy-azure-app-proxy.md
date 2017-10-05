---
title: "Доменные службы Azure Active Directory: развертывание прокси приложения Azure Active Directory | Документация Майкрософт"
description: "Использование прокси приложения Azure AD в управляемых доменах доменных служб Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: c158c67a82e12501386179e19bc75fd852d7e308
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="4d76a-103">Развертывание прокси приложения Azure AD в управляемых доменах доменных служб Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d76a-103">Deploy Azure AD Application Proxy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="4d76a-104">Прокси приложения Azure Active Directory помогает организовать удаленную работу сотрудников, публикуя локальные приложения для доступа через Интернет.</span><span class="sxs-lookup"><span data-stu-id="4d76a-104">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="4d76a-105">С помощью доменных служб Azure AD теперь можно переносить устаревшие локальные приложения в службы инфраструктуры Azure.</span><span class="sxs-lookup"><span data-stu-id="4d76a-105">With Azure AD Domain Services, you can now lift-and-shift legacy applications running on-premises to Azure Infrastructure Services.</span></span> <span data-ttu-id="4d76a-106">Затем эти приложения можно опубликовать с помощью прокси приложения Azure AD, чтобы обеспечить безопасный удаленный доступ для пользователей в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="4d76a-106">You can then publish these applications using the Azure AD Application Proxy, to provide secure remote access to users in your organization.</span></span>

<span data-ttu-id="4d76a-107">Если вы еще не знакомы с прокси приложения Azure AD, узнайте, [как обеспечить безопасный удаленный доступ к локальным приложениям](../active-directory/active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4d76a-107">If you're new to the Azure AD Application Proxy, learn more about this feature with the following article: [How to provide secure remote access to on-premises applications](../active-directory/active-directory-application-proxy-get-started.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="4d76a-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="4d76a-108">Before you begin</span></span>
<span data-ttu-id="4d76a-109">Чтобы выполнить задачи, описанные в этой статье, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="4d76a-109">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="4d76a-110">Действующая **подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="4d76a-110">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="4d76a-111">**Каталог Azure AD** — синхронизированный с локальным каталогом или каталогом только для облака.</span><span class="sxs-lookup"><span data-stu-id="4d76a-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="4d76a-112">Для использования прокси приложения Azure AD необходима **лицензия Azure AD Basic или Premium**.</span><span class="sxs-lookup"><span data-stu-id="4d76a-112">An **Azure AD Basic or Premium license** is required to use the Azure AD Application Proxy.</span></span>
4. <span data-ttu-id="4d76a-113">**Доменные службы Azure AD** должны быть включены для каталога Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d76a-113">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="4d76a-114">Если это еще не сделано, выполните все задачи, описанные в [руководстве по началу работы](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="4d76a-114">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a><span data-ttu-id="4d76a-115">Задача 1. Включить прокси приложения Azure AD для каталога Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d76a-115">Task 1 - Enable Azure AD Application Proxy for your Azure AD directory</span></span>
<span data-ttu-id="4d76a-116">Чтобы включить прокси приложения Azure AD для каталога Azure AD, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4d76a-116">Perform the following steps to enable the Azure AD Application Proxy for your Azure AD directory.</span></span>

1. <span data-ttu-id="4d76a-117">Войдите на [портал Azure](http://portal.azure.com) с учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="4d76a-117">Sign in as an administrator in the [Azure portal](http://portal.azure.com).</span></span>

2. <span data-ttu-id="4d76a-118">Щелкните **Azure Active Directory**, чтобы просмотреть каталоги.</span><span class="sxs-lookup"><span data-stu-id="4d76a-118">Click **Azure Active Directory** to bring up the directory overview.</span></span> <span data-ttu-id="4d76a-119">Щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="4d76a-119">Click **Enterprise applications**.</span></span>

    ![Выбор каталога Azure AD](./media/app-proxy/app-proxy-enable-start.png)
3. <span data-ttu-id="4d76a-121">Щелкните **Прокси приложения**.</span><span class="sxs-lookup"><span data-stu-id="4d76a-121">Click **Application proxy**.</span></span> <span data-ttu-id="4d76a-122">Если у вас нет подписки Azure AD Basic или Azure AD Premium, на экране отобразится приглашение включить пробную версию.</span><span class="sxs-lookup"><span data-stu-id="4d76a-122">If you do not have an Azure AD Basic or Azure AD Premium subscription, you see an option to enable a trial.</span></span> <span data-ttu-id="4d76a-123">Установите для параметра **Включить прокси приложения?** значение **Включить** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4d76a-123">Toggle **Enable Application Proxy?** to **Enable** and click **Save**.</span></span>

    ![Использование прокси приложения](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. <span data-ttu-id="4d76a-125">Чтобы загрузить соединитель, нажмите кнопку **Соединитель**.</span><span class="sxs-lookup"><span data-stu-id="4d76a-125">To download the connector, click the **Connector** button.</span></span>

    ![Загрузка соединителя](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. <span data-ttu-id="4d76a-127">На странице загрузки примите условия лицензионного соглашения и соглашения о конфиденциальности и нажмите кнопку **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="4d76a-127">On the download page, accept the license terms and privacy agreement and click the **Download** button.</span></span>

    ![Подтверждение загрузки](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-to-deploy-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="4d76a-129">Задача 2. Подготовка серверов в составе домена Windows для развертывания соединителя прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d76a-129">Task 2 - Provision domain-joined Windows servers to deploy the Azure AD Application Proxy connector</span></span>
<span data-ttu-id="4d76a-130">Для этого необходимы виртуальные машины под управлением Windows Server в составе домена, на которых можно установить соединитель прокси приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d76a-130">You need domain-joined Windows Server virtual machines on which you can install the Azure AD Application Proxy connector.</span></span> <span data-ttu-id="4d76a-131">В зависимости от публикуемых приложений можно подготовить несколько серверов, на которых будет установлен соединитель.</span><span class="sxs-lookup"><span data-stu-id="4d76a-131">Depending on the applications being published, you may choose to provision multiple servers on which the connector is installed.</span></span> <span data-ttu-id="4d76a-132">Этот параметр развертывания обеспечивает более высокую доступность и позволяет обрабатывать более тяжелые нагрузки аутентификации.</span><span class="sxs-lookup"><span data-stu-id="4d76a-132">This deployment option gives you greater availability and helps handle heavier authentication loads.</span></span>

<span data-ttu-id="4d76a-133">Подготавливайте серверы соединителя в той же виртуальной сети (подключенной или одноранговой виртуальной сети), в которой включен управляемый домен доменных служб Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d76a-133">Provision the connector servers on the same virtual network (or a connected/peered virtual network), in which you have enabled your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="4d76a-134">Аналогичным образом серверы, на которых размещаются приложения, публикуемые с использованием прокси приложения, должны быть установлены в той же виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="4d76a-134">Similarly, the servers hosting the applications you publish via the Application Proxy need to be installed on the same Azure virtual network.</span></span>

<span data-ttu-id="4d76a-135">Чтобы подготовить серверы соединителя, выполните задачи, описанные в статье [Присоединение виртуальной машины Windows к управляемому домену](active-directory-ds-admin-guide-join-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="4d76a-135">To provision connector servers, follow the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>


## <a name="task-3---install-and-register-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="4d76a-136">Задача 3. Установка и регистрация соединителя прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d76a-136">Task 3 - Install and register the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="4d76a-137">Ранее была выполнена подготовка виртуальной машины Windows Server и ее присоединение к управляемому домену.</span><span class="sxs-lookup"><span data-stu-id="4d76a-137">Previously, you provisioned a Windows Server virtual machine and joined it to the managed domain.</span></span> <span data-ttu-id="4d76a-138">В этой задаче будет установлен соединитель прокси приложения Azure AD в этой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="4d76a-138">In this task, you will install the Azure AD Application Proxy connector on this virtual machine.</span></span>

1. <span data-ttu-id="4d76a-139">Скопируйте пакет установки соединителя в виртуальную машину, в которой устанавливается соединитель прокси веб-приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d76a-139">Copy the connector installation package to the VM on which you install the Azure AD Web Application Proxy connector.</span></span>

2. <span data-ttu-id="4d76a-140">В виртуальной машине запустите **AADApplicationProxyConnectorInstaller.exe**.</span><span class="sxs-lookup"><span data-stu-id="4d76a-140">Run **AADApplicationProxyConnectorInstaller.exe** on the virtual machine.</span></span> <span data-ttu-id="4d76a-141">Примите условия лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="4d76a-141">Accept the software license terms.</span></span>

    ![Принятие условий установки](./media/app-proxy/app-proxy-install-connector-terms.png)
3. <span data-ttu-id="4d76a-143">Во время установки вам будет предложено зарегистрировать соединитель прокси приложения каталога Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d76a-143">During installation, you are prompted to register the connector with the Application Proxy of your Azure AD directory.</span></span>
    * <span data-ttu-id="4d76a-144">Укажите **учетные данные глобального администратора Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="4d76a-144">Provide your **Azure AD global administrator credentials**.</span></span> <span data-ttu-id="4d76a-145">Ваш клиент глобального администратора может отличаться от учетных данных Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4d76a-145">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
    * <span data-ttu-id="4d76a-146">Учетная запись администратора, используемая для регистрации соединителя, должна принадлежать тому каталогу, где включена служба прокси приложения.</span><span class="sxs-lookup"><span data-stu-id="4d76a-146">The administrator account used to register the connector must belong to the same directory where you enabled the Application Proxy service.</span></span> <span data-ttu-id="4d76a-147">Например, если домен клиента contoso.com, администратором должен быть пользователь admin@contoso.com или другой действительный псевдоним в этом домене.</span><span class="sxs-lookup"><span data-stu-id="4d76a-147">For example, if the tenant domain is contoso.com, the admin should be admin@contoso.com or any other valid alias on that domain.</span></span>
    * <span data-ttu-id="4d76a-148">Если на сервере, на который устанавливается соединитель, включена конфигурация усиленной безопасности Internet Explorer, экран регистрации может быть заблокирован.</span><span class="sxs-lookup"><span data-stu-id="4d76a-148">If IE Enhanced Security Configuration is turned on for the server where you are installing the connector, the registration screen might be blocked.</span></span> <span data-ttu-id="4d76a-149">Чтобы разрешить доступ, следуйте указаниям в сообщении об ошибке.</span><span class="sxs-lookup"><span data-stu-id="4d76a-149">To allow access, follow the instructions in the error message.</span></span> <span data-ttu-id="4d76a-150">Убедитесь, что конфигурация усиленной безопасности Internet Explorer отключена.</span><span class="sxs-lookup"><span data-stu-id="4d76a-150">Make sure that Internet Explorer Enhanced Security is off.</span></span>
    * <span data-ttu-id="4d76a-151">Если не удается зарегистрировать соединитель, см. сведения в статье [Устранение неполадок прокси-сервера приложений](../active-directory/active-directory-application-proxy-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="4d76a-151">If connector registration does not succeed, see [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md).</span></span>

    ![Соединитель установлен](./media/app-proxy/app-proxy-connector-installed.png)
4. <span data-ttu-id="4d76a-153">Чтобы убедиться, что соединитель работает должным образом, запустите средство устранения неполадок соединителя прокси приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d76a-153">To ensure the connector works properly, run the Azure AD Application Proxy Connector Troubleshooter.</span></span> <span data-ttu-id="4d76a-154">После запуска средства устранения неполадок должен отобразиться отчет об успешном завершении.</span><span class="sxs-lookup"><span data-stu-id="4d76a-154">You should see a successful report after running the troubleshooter.</span></span>

    ![Успешное завершение работы средства устранения неполадок](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. <span data-ttu-id="4d76a-156">Вы увидите недавно установленный соединитель, указанный на странице прокси приложения в каталоге Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d76a-156">You should see the newly installed connector listed on the Application proxy page in your Azure AD directory.</span></span>

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> <span data-ttu-id="4d76a-157">Соединители можно установить на нескольких серверах, чтобы обеспечить высокую доступность для аутентификации приложений, опубликованных с использованием прокси приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d76a-157">You may choose to install connectors on multiple servers to guarantee high availability for authenticating applications published through the Azure AD Application Proxy.</span></span> <span data-ttu-id="4d76a-158">Выполните перечисленные выше шаги, чтобы установить соединитель на других серверах, которые присоединены к управляемому домену.</span><span class="sxs-lookup"><span data-stu-id="4d76a-158">Perform the same steps listed above to install the connector on other servers joined to your managed domain.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="4d76a-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4d76a-159">Next Steps</span></span>
<span data-ttu-id="4d76a-160">После этого прокси приложения Azure AD настроен и интегрирован в управляемый домен доменных служб Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d76a-160">You have set up the Azure AD Application Proxy and integrated it with your Azure AD Domain Services managed domain.</span></span>

* <span data-ttu-id="4d76a-161">**Перенос приложений в виртуальные машины Azure.** Приложения можно перенести из локальных серверов в виртуальные машины Azure, которые присоединены к управляемому домену.</span><span class="sxs-lookup"><span data-stu-id="4d76a-161">**Migrate your applications to Azure virtual machines:** You can lift-and-shift your applications from on-premises servers to Azure virtual machines joined to your managed domain.</span></span> <span data-ttu-id="4d76a-162">Это позволяет избавиться от затрат на поддержание инфраструктуры локальных серверов.</span><span class="sxs-lookup"><span data-stu-id="4d76a-162">Doing so helps you get rid of the infrastructure costs of running servers on-premises.</span></span>

* <span data-ttu-id="4d76a-163">**Публикация приложений с помощью прокси приложения Azure AD.** Публикация приложений, работающих в виртуальных машинах Azure, с использованием прокси приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d76a-163">**Publish applications using Azure AD Application Proxy:** Publish applications running on your Azure virtual machines using the Azure AD Application Proxy.</span></span> <span data-ttu-id="4d76a-164">Дополнительные сведения см. в статье [Публикация приложений с помощью прокси приложения Azure AD](../active-directory/application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4d76a-164">For more information, see [publish applications using Azure AD Application Proxy](../active-directory/application-proxy-publish-azure-portal.md)</span></span>


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="4d76a-165">Примечание к развертыванию. Публикация приложений интегрированной проверки подлинности Windows с использованием прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d76a-165">Deployment note - Publish IWA (Integrated Windows Authentication) applications using Azure AD Application Proxy</span></span>
<span data-ttu-id="4d76a-166">Для приложений с использованием интегрированной проверки подлинности Windows активируйте единый вход (SSO), разрешив соединителям прокси приложения олицетворять пользователей, а также отправлять и получать токены от их имени.</span><span class="sxs-lookup"><span data-stu-id="4d76a-166">Enable single sign-on to your applications using Integrated Windows Authentication (IWA) by granting Application Proxy Connectors permission to impersonate users, and send and receive tokens on their behalf.</span></span> <span data-ttu-id="4d76a-167">Настройка ограниченного делегирования Kerberos для коннектора, чтобы предоставлять необходимые разрешения для доступа к ресурсам управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="4d76a-167">Configure kerberos constrained delegation (KCD) for the connector to grant the required permissions to access resources on the managed domain.</span></span> <span data-ttu-id="4d76a-168">Используйте механизм ограниченного делегирования Kerberos на основе ресурсов в управляемых доменах для повышения уровня безопасности.</span><span class="sxs-lookup"><span data-stu-id="4d76a-168">Use the resource-based KCD mechanism on managed domains for increased security.</span></span>


### <a name="enable-resource-based-kerberos-constrained-delegation-for-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="4d76a-169">Включение ограниченного делегирования Kerberos на основе ресурсов для соединителя прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d76a-169">Enable resource-based kerberos constrained delegation for the Azure AD Application Proxy connector</span></span>
<span data-ttu-id="4d76a-170">Соединитель прокси приложения Azure необходимо настроить для ограниченного делегирования Kerberos, чтобы он мог олицетворять пользователей в управляемом домене.</span><span class="sxs-lookup"><span data-stu-id="4d76a-170">The Azure Application Proxy connector should be configured for kerberos constrained delegation (KCD), so it can impersonate users on the managed domain.</span></span> <span data-ttu-id="4d76a-171">В управляемом домене доменных служб Azure AD у вас нет привилегий администратора домена.</span><span class="sxs-lookup"><span data-stu-id="4d76a-171">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span></span> <span data-ttu-id="4d76a-172">Таким образом **традиционное ограниченное делегирование Kerberos на уровне учетной записи нельзя настроить в управляемом домене**.</span><span class="sxs-lookup"><span data-stu-id="4d76a-172">Therefore, **traditional account-level KCD cannot be configured on a managed domain**.</span></span>

<span data-ttu-id="4d76a-173">Используйте основанное на ресурсах ограниченное делегирование Kerberos, как описано в этой [статье](active-directory-ds-enable-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="4d76a-173">Use resource-based KCD as described in this [article](active-directory-ds-enable-kcd.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4d76a-174">Чтобы администрировать управляемый домен, используя командлеты AD PowerShell, необходимо быть участником группы "Администраторы контроллера домена AAD".</span><span class="sxs-lookup"><span data-stu-id="4d76a-174">You need to be a member of the 'AAD DC Administrators' group, to administer the managed domain using AD PowerShell cmdlets.</span></span>
>
>

<span data-ttu-id="4d76a-175">Чтобы получить параметры для компьютера, на котором установлен соединитель прокси приложения Azure AD, используйте командлет PowerShell Get-ADComputer.</span><span class="sxs-lookup"><span data-stu-id="4d76a-175">Use the Get-ADComputer PowerShell cmdlet to retrieve the settings for the computer on which the Azure AD Application Proxy connector is installed.</span></span>
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

<span data-ttu-id="4d76a-176">После этого используйте командлет Set-ADComputer для настройки ограниченного делегирования Kerberos на основе ресурсов для сервера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4d76a-176">Thereafter, use the Set-ADComputer cmdlet to set up resource-based KCD for the resource server.</span></span>
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

<span data-ttu-id="4d76a-177">При развертывании нескольких соединителей прокси приложения в управляемом домене необходимо настроить ограниченное делегирование Kerberos на основе ресурсов для каждого такого экземпляра соединителя.</span><span class="sxs-lookup"><span data-stu-id="4d76a-177">If you have deployed multiple Application Proxy connectors on your managed domain, you need to configure resource-based KCD for each such connector instance.</span></span>


## <a name="related-content"></a><span data-ttu-id="4d76a-178">Похожий контент</span><span class="sxs-lookup"><span data-stu-id="4d76a-178">Related Content</span></span>
* [<span data-ttu-id="4d76a-179">Приступая к работе с доменными службами Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d76a-179">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="4d76a-180">Настройка ограниченного делегирования Kerberos в управляемом домене</span><span class="sxs-lookup"><span data-stu-id="4d76a-180">Configure Kerberos Constrained Delegation on a managed domain</span></span>](active-directory-ds-enable-kcd.md)
* [<span data-ttu-id="4d76a-181">(Обзор ограниченного делегирования Kerberos)</span><span class="sxs-lookup"><span data-stu-id="4d76a-181">Kerberos Constrained Delegation Overview</span></span>](https://technet.microsoft.com/library/jj553400.aspx)
