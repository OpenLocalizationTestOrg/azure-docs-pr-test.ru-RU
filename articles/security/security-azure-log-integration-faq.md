---
title: "Часто задаваемые вопросы об интеграции журналов Azure | Документация Майкрософт"
description: "Эта статья содержит ответы на часто задаваемые вопросы об интеграции журналов Azure."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: d06d1ac5-5c3b-49de-800e-4d54b3064c64
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload8: na
ms.date: 08/07/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: bfdc7154160bb6bb7dc9c46eb2352ce74310c4de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-log-integration-faq"></a><span data-ttu-id="27804-103">Часто задаваемые вопросы об интеграции журналов Azure</span><span class="sxs-lookup"><span data-stu-id="27804-103">Azure Log Integration FAQ</span></span>
<span data-ttu-id="27804-104">В этой статье содержатся ответы на некоторые часто задаваемые вопросы о службе интеграции журналов Azure.</span><span class="sxs-lookup"><span data-stu-id="27804-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span> 

<span data-ttu-id="27804-105">Служба интеграции журналов Azure (служба ОС Windows) позволяет интегрировать необработанные журналы из ресурсов Azure с локальными системами SIEM.</span><span class="sxs-lookup"><span data-stu-id="27804-105">Azure Log Integration is a Windows operating system service that you can use to integrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="27804-106">Такая интеграция обеспечивает единую панель мониторинга для всех локальных и облачных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="27804-106">This integration provides a unified dashboard for all your assets, on-premises or in the cloud.</span></span> <span data-ttu-id="27804-107">Интеграция также позволяет выполнять статистическое вычисление, сопоставление и анализ, а также предупреждать о событиях безопасности, связанных с приложениями.</span><span class="sxs-lookup"><span data-stu-id="27804-107">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-the-azure-log-integration-software-free"></a><span data-ttu-id="27804-108">Предоставляется ли служба интеграции журналов Azure бесплатно?</span><span class="sxs-lookup"><span data-stu-id="27804-108">Is the Azure Log Integration software free?</span></span>
<span data-ttu-id="27804-109">Да.</span><span class="sxs-lookup"><span data-stu-id="27804-109">Yes.</span></span> <span data-ttu-id="27804-110">Плата за использование службы интеграции журналов Azure не взимается.</span><span class="sxs-lookup"><span data-stu-id="27804-110">There is no charge for the Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="27804-111">Где доступна служба интеграции журналов Azure?</span><span class="sxs-lookup"><span data-stu-id="27804-111">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="27804-112">Сейчас служба доступна в рамках коммерческой лицензии Azure и лицензии Azure для государственных организаций и недоступна в Китае и в Германии.</span><span class="sxs-lookup"><span data-stu-id="27804-112">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-the-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="27804-113">Как увидеть учетные записи хранения, из которых служба интеграции журналов Azure извлекает журналы виртуальных машин Azure?</span><span class="sxs-lookup"><span data-stu-id="27804-113">How can I see the storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>
<span data-ttu-id="27804-114">Выполните команду **azlog source list**.</span><span class="sxs-lookup"><span data-stu-id="27804-114">Run the command **azlog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-the-azure-log-integration-logs-are-from"></a><span data-ttu-id="27804-115">Как определить, из каких подписок получены журналы службы интеграции журналов Azure?</span><span class="sxs-lookup"><span data-stu-id="27804-115">How can I tell which subscription the Azure Log Integration logs are from?</span></span>

<span data-ttu-id="27804-116">Если журналы аудита хранятся в каталогах **AzureResourcemanagerJson**, то идентификатором подписки является имя файла журнала.</span><span class="sxs-lookup"><span data-stu-id="27804-116">In the case of audit logs that are placed in the **AzureResourcemanagerJson** directories, the subscription ID is in the log file name.</span></span> <span data-ttu-id="27804-117">Это правило применяется и к журналам в папке **AzureSecurityCenterJson**.</span><span class="sxs-lookup"><span data-stu-id="27804-117">This is also true for logs in the **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="27804-118">Например:</span><span class="sxs-lookup"><span data-stu-id="27804-118">For example:</span></span>

<span data-ttu-id="27804-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span><span class="sxs-lookup"><span data-stu-id="27804-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="27804-120">В состав имен журналов аудита Azure Active Directory входит идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="27804-120">Azure Active Directory audit logs include the tenant ID as part of the name.</span></span>

<span data-ttu-id="27804-121">Журналы диагностики, которые считываются из концентратора событий, не содержат идентификатор подписки в имени.</span><span class="sxs-lookup"><span data-stu-id="27804-121">Diagnostic logs that are read from an event hub do not include the subscription ID as part of the name.</span></span> <span data-ttu-id="27804-122">Вместо этого они содержат понятное имя, заданное при создании источника концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="27804-122">Instead, they include the friendly name specified as part of the creation of the event hub source.</span></span> 

## <a name="how-can-i-update-the-proxy-configuration"></a><span data-ttu-id="27804-123">Как обновить конфигурацию прокси-сервера?</span><span class="sxs-lookup"><span data-stu-id="27804-123">How can I update the proxy configuration?</span></span>
<span data-ttu-id="27804-124">Если параметры прокси-сервера не позволяют получать доступ к хранилищу Azure напрямую, то откройте файл **AZLOG.EXE.CONFIG** из расположения **c:\Program Files\Microsoft Azure Log Integration**.</span><span class="sxs-lookup"><span data-stu-id="27804-124">If your proxy setting does not allow Azure storage access directly, open the **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="27804-125">Обновите файл, включив в его раздел **defaultProxy** прокси-адрес вашей организации.</span><span class="sxs-lookup"><span data-stu-id="27804-125">Update the file to include the **defaultProxy** section with the proxy address of your organization.</span></span> <span data-ttu-id="27804-126">После завершения обновления остановите и запустите службу с помощью команд **net stop azlog** и **net start azlog**.</span><span class="sxs-lookup"><span data-stu-id="27804-126">After the update is done, stop and start the service by using the commands **net stop azlog** and **net start azlog**.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress=http://127.0.0.1:8888
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-the-subscription-information-in-windows-events"></a><span data-ttu-id="27804-127">Как увидеть сведения о подписке в событиях Windows?</span><span class="sxs-lookup"><span data-stu-id="27804-127">How can I see the subscription information in Windows events?</span></span>
<span data-ttu-id="27804-128">При добавлении источника добавьте идентификатор к понятному имени:</span><span class="sxs-lookup"><span data-stu-id="27804-128">Append the subscription ID to the friendly name while adding the source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="27804-129">XML-файл события содержит следующие метаданные, включая идентификатор подписки:</span><span class="sxs-lookup"><span data-stu-id="27804-129">The event XML has the following metadata, including the subscription ID:</span></span>

![XML-файл события][1]

## <a name="error-messages"></a><span data-ttu-id="27804-131">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="27804-131">Error messages</span></span>
### <a name="when-i-run-the-command-azlog-createazureid-why-do-i-get-the-following-error"></a><span data-ttu-id="27804-132">Почему при выполнении команды **azlog createazureid** возникает следующая ошибка?</span><span class="sxs-lookup"><span data-stu-id="27804-132">When I run the command **azlog createazureid**, why do I get the following error?</span></span>
<span data-ttu-id="27804-133">Ошибка:</span><span class="sxs-lookup"><span data-stu-id="27804-133">Error:</span></span>

  <span data-ttu-id="27804-134">*Не удалось создать приложение AAD - Клиент 72f988bf-86f1-41af-91ab-2d7cd011db37 - Причина = 'Запрещено' - Сообщение = 'Недостаточно привилегий для выполнения операции.'*</span><span class="sxs-lookup"><span data-stu-id="27804-134">*Failed to create AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges to complete the operation.'*</span></span>

<span data-ttu-id="27804-135">Команда **azlog createazureid** пытается создать субъект-службу на всех клиентах Azure AD для подписок, к которым имеют доступ учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="27804-135">The **azlog createazureid** command attempts to create a service principal in all the Azure AD tenants for the subscriptions that the Azure login has access to.</span></span> <span data-ttu-id="27804-136">Если учетные данные Azure принадлежат пользователю-гостю на этом клиенте Azure AD, то команда завершается ошибкой и отображается сообщение "Недостаточно привилегий для выполнения операции".</span><span class="sxs-lookup"><span data-stu-id="27804-136">If your Azure login is only a guest user in that Azure AD tenant, the command fails with "Insufficient privileges to complete the operation."</span></span> <span data-ttu-id="27804-137">Попросите администратора клиента добавить вашу учетную запись в качестве пользователя данного клиента.</span><span class="sxs-lookup"><span data-stu-id="27804-137">Ask the tenant admin to add your account as a user in the tenant.</span></span>

### <a name="when-i-run-the-command-azlog-authorize-why-do-i-get-the-following-error"></a><span data-ttu-id="27804-138">Почему при выполнении команды **azlog authorize** возникает следующая ошибка?</span><span class="sxs-lookup"><span data-stu-id="27804-138">When I run the command **azlog authorize**, why do I get the following error?</span></span>
<span data-ttu-id="27804-139">Ошибка:</span><span class="sxs-lookup"><span data-stu-id="27804-139">Error:</span></span>

  <span data-ttu-id="27804-140">*"Warning creating Role Assignment - AuthorizationFailed" (Предупреждение при создании назначения роли — AuthorizationFailed): Клиент "janedo@microsoft.com" с идентификатором объекта "fe9e03e4-4dad-4328-910f-fd24a9660bd2" не авторизован для выполнения действия "Microsoft.Authorization/roleAssignments/write" с областью "/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000".*</span><span class="sxs-lookup"><span data-stu-id="27804-140">*Warning creating Role Assignment - AuthorizationFailed: The client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="27804-141">Команда **azlog authorize** назначает роль читателя субъекту-службе Azure AD (созданному с помощью команды **azlog createazureid**) для предоставленных подписок.</span><span class="sxs-lookup"><span data-stu-id="27804-141">The **azlog authorize** command assigns the role of reader to the Azure AD service principal (created with **azlog createazureid**) to the provided subscriptions.</span></span> <span data-ttu-id="27804-142">Если учетные данные Azure не принадлежат соадминистратору или владельцу подписки, то команда завершается ошибкой и отображается сообщение "Сбой авторизации".</span><span class="sxs-lookup"><span data-stu-id="27804-142">If the Azure login is not a co-administrator or an owner of the subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="27804-143">Для выполнения этого действия используйте управление доступом на основе ролей (RBAC) в Azure, настроив роль соадминистратора или владельца.</span><span class="sxs-lookup"><span data-stu-id="27804-143">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed to complete this action.</span></span>

## <a name="where-can-i-find-the-definition-of-the-properties-in-the-audit-log"></a><span data-ttu-id="27804-144">Где найти определения свойств в журнале аудита?</span><span class="sxs-lookup"><span data-stu-id="27804-144">Where can I find the definition of the properties in the audit log?</span></span>
<span data-ttu-id="27804-145">См.:</span><span class="sxs-lookup"><span data-stu-id="27804-145">See:</span></span>

* <span data-ttu-id="27804-146">[Просмотр журналов действий для аудита действий с ресурсами](../azure-resource-manager/resource-group-audit.md);</span><span class="sxs-lookup"><span data-stu-id="27804-146">[Audit operations with Azure Resource Manager](../azure-resource-manager/resource-group-audit.md)</span></span>
* <span data-ttu-id="27804-147">[Activity Logs](https://msdn.microsoft.com/library/azure/dn931934.aspx) (Журналы действий).</span><span class="sxs-lookup"><span data-stu-id="27804-147">[List the management events in a subscription in the Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931934.aspx)</span></span>

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="27804-148">Где найти подробные сведения об оповещениях центра безопасности Azure?</span><span class="sxs-lookup"><span data-stu-id="27804-148">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="27804-149">См. статью [Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="27804-149">See [Managing and responding to security alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="27804-150">Как изменить, что именно должна собирать система диагностики виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="27804-150">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="27804-151">Сведения о том, как получать, изменять и настраивать конфигурацию системы диагностики Azure, см. в статье [Включение системы диагностики Azure на виртуальной машине под управлением Windows с помощью PowerShell](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="27804-151">For details on how to get, modify, and set the Azure Diagnostics configuration, see [Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="27804-152">В следующем примере показано получение конфигурации системы диагностики Azure:</span><span class="sxs-lookup"><span data-stu-id="27804-152">The following example gets the Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="27804-153">В следующем примере показано изменение конфигурации системы диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="27804-153">The following example modifies the Azure Diagnostics configuration.</span></span> <span data-ttu-id="27804-154">В этой конфигурации из журнала событий безопасности собираются только идентификаторы события 4624 и 4625.</span><span class="sxs-lookup"><span data-stu-id="27804-154">In this configuration, only event ID 4624 and event ID 4625 are collected from the security event log.</span></span> <span data-ttu-id="27804-155">События антивредоносного ПО Майкрософт для Azure собираются из журнала системных событий.</span><span class="sxs-lookup"><span data-stu-id="27804-155">Microsoft Antimalware for Azure events are collected from the system event log.</span></span> <span data-ttu-id="27804-156">Дополнительные сведения об использовании выражений XPath см. в статье [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)) (Использование событий).</span><span class="sxs-lookup"><span data-stu-id="27804-156">For details on the use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="27804-157">В следующем примере показан выбор конфигурации системы диагностики Azure:</span><span class="sxs-lookup"><span data-stu-id="27804-157">The following example sets the Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="27804-158">После внесения изменений проверьте учетную запись хранения, чтобы убедиться, что собираются именно необходимые события.</span><span class="sxs-lookup"><span data-stu-id="27804-158">After you make changes, check the storage account to ensure that the correct events are collected.</span></span>

<span data-ttu-id="27804-159">При наличии проблем во время установки и настройки создайте [запрос на поддержку](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span><span class="sxs-lookup"><span data-stu-id="27804-159">If you have any issues during the installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="27804-160">Выберите **Интеграция с журналом** в качестве службы, в которую необходимо отправить запрос поддержки.</span><span class="sxs-lookup"><span data-stu-id="27804-160">Select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-to-integrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="27804-161">Можно ли интегрировать журналы службы "Наблюдатель за сетями" с системой SIEM с помощью службы интеграции журналов Azure?</span><span class="sxs-lookup"><span data-stu-id="27804-161">Can I use Azure Log Integration to integrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="27804-162">Служба "Наблюдатель за сетями Azure" создает множество сведений о журналах.</span><span class="sxs-lookup"><span data-stu-id="27804-162">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="27804-163">Эти журналы не следует отправлять в SIEM.</span><span class="sxs-lookup"><span data-stu-id="27804-163">These logs are not meant to be sent to a SIEM.</span></span> <span data-ttu-id="27804-164">Журналы Наблюдателя за сетями отправляются только в учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="27804-164">The only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="27804-165">Служба интеграции журналов Azure не поддерживает чтение этих журналов и не обеспечивает их доступность в системе SIEM.</span><span class="sxs-lookup"><span data-stu-id="27804-165">Azure Log Integration does not support reading these logs and making them available to a SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
