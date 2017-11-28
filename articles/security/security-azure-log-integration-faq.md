---
title: "aaaAzure журнала интеграции часто задаваемые вопросы | Документы Microsoft"
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
ms.openlocfilehash: e886035c9a180d0cd5fcbe9cc02483782df6dbe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-faq"></a><span data-ttu-id="2c001-103">Часто задаваемые вопросы об интеграции журналов Azure</span><span class="sxs-lookup"><span data-stu-id="2c001-103">Azure Log Integration FAQ</span></span>
<span data-ttu-id="2c001-104">В этой статье содержатся ответы на некоторые часто задаваемые вопросы о службе интеграции журналов Azure.</span><span class="sxs-lookup"><span data-stu-id="2c001-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span> 

<span data-ttu-id="2c001-105">Интеграция Azure журнала является служба операционной системы Windows, можно использовать журналы необработанных toointegrate по вашим ресурсам Azure в вашей локальной безопасности сведения и событий (SIEM) систем управления.</span><span class="sxs-lookup"><span data-stu-id="2c001-105">Azure Log Integration is a Windows operating system service that you can use toointegrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="2c001-106">Такая интеграция обеспечивает единый панели мониторинга для каждого из ОС, локально или в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="2c001-106">This integration provides a unified dashboard for all your assets, on-premises or in hello cloud.</span></span> <span data-ttu-id="2c001-107">Интеграция также позволяет выполнять статистическое вычисление, сопоставление и анализ, а также предупреждать о событиях безопасности, связанных с приложениями.</span><span class="sxs-lookup"><span data-stu-id="2c001-107">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-hello-azure-log-integration-software-free"></a><span data-ttu-id="2c001-108">— Это программное обеспечение интеграции Azure журнала hello бесплатно?</span><span class="sxs-lookup"><span data-stu-id="2c001-108">Is hello Azure Log Integration software free?</span></span>
<span data-ttu-id="2c001-109">Да.</span><span class="sxs-lookup"><span data-stu-id="2c001-109">Yes.</span></span> <span data-ttu-id="2c001-110">Нет бесплатно hello программным обеспечением для интеграции журналов Azure.</span><span class="sxs-lookup"><span data-stu-id="2c001-110">There is no charge for hello Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="2c001-111">Где доступна служба интеграции журналов Azure?</span><span class="sxs-lookup"><span data-stu-id="2c001-111">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="2c001-112">Сейчас служба доступна в рамках коммерческой лицензии Azure и лицензии Azure для государственных организаций и недоступна в Китае и в Германии.</span><span class="sxs-lookup"><span data-stu-id="2c001-112">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="2c001-113">Просмотр учетных записей хранения hello, из которых интеграции Azure журнала запрашивает журналы виртуальной Машине Azure?</span><span class="sxs-lookup"><span data-stu-id="2c001-113">How can I see hello storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>
<span data-ttu-id="2c001-114">Выполните команду hello **azlog исходного списка**.</span><span class="sxs-lookup"><span data-stu-id="2c001-114">Run hello command **azlog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a><span data-ttu-id="2c001-115">Как узнать, какие подписки hello Azure Integration журнала записываются из?</span><span class="sxs-lookup"><span data-stu-id="2c001-115">How can I tell which subscription hello Azure Log Integration logs are from?</span></span>

<span data-ttu-id="2c001-116">В случае, когда hello журналы аудита, которые помещаются в hello **AzureResourcemanagerJson** каталоги, идентификатор подписки hello — в файле журнала hello.</span><span class="sxs-lookup"><span data-stu-id="2c001-116">In hello case of audit logs that are placed in hello **AzureResourcemanagerJson** directories, hello subscription ID is in hello log file name.</span></span> <span data-ttu-id="2c001-117">Это справедливо для журналов в hello **AzureSecurityCenterJson** папки.</span><span class="sxs-lookup"><span data-stu-id="2c001-117">This is also true for logs in hello **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="2c001-118">Например:</span><span class="sxs-lookup"><span data-stu-id="2c001-118">For example:</span></span>

<span data-ttu-id="2c001-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span><span class="sxs-lookup"><span data-stu-id="2c001-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="2c001-120">Журналы аудита Azure Active Directory включают hello идентификатор клиента как часть имени hello.</span><span class="sxs-lookup"><span data-stu-id="2c001-120">Azure Active Directory audit logs include hello tenant ID as part of hello name.</span></span>

<span data-ttu-id="2c001-121">Журналы диагностики, которые считываются из концентратора событий не включают идентификатор подписки hello как часть имени hello.</span><span class="sxs-lookup"><span data-stu-id="2c001-121">Diagnostic logs that are read from an event hub do not include hello subscription ID as part of hello name.</span></span> <span data-ttu-id="2c001-122">Вместо этого они включают hello понятное имя, указанное как часть создания hello источника концентратора событий hello.</span><span class="sxs-lookup"><span data-stu-id="2c001-122">Instead, they include hello friendly name specified as part of hello creation of hello event hub source.</span></span> 

## <a name="how-can-i-update-hello-proxy-configuration"></a><span data-ttu-id="2c001-123">Как обновить настройки прокси-сервера hello</span><span class="sxs-lookup"><span data-stu-id="2c001-123">How can I update hello proxy configuration?</span></span>
<span data-ttu-id="2c001-124">Если параметра прокси не позволяет непосредственно для доступа к хранилищу Azure, откройте hello **AZLOG. EXE-ФАЙЛА. КОНФИГУРАЦИИ** файла в **c:\Program Files\Microsoft Azure журнала интеграции**.</span><span class="sxs-lookup"><span data-stu-id="2c001-124">If your proxy setting does not allow Azure storage access directly, open hello **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="2c001-125">Обновление hello файл tooinclude hello **defaultProxy** раздел с hello адрес прокси-сервера в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="2c001-125">Update hello file tooinclude hello **defaultProxy** section with hello proxy address of your organization.</span></span> <span data-ttu-id="2c001-126">После завершения обновления hello остановить и запустить службу hello с помощью команд hello **azlog net stop** и **команда net start azlog**.</span><span class="sxs-lookup"><span data-stu-id="2c001-126">After hello update is done, stop and start hello service by using hello commands **net stop azlog** and **net start azlog**.</span></span>

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

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a><span data-ttu-id="2c001-127">Просмотр сведений о подписке hello в событиях Windows?</span><span class="sxs-lookup"><span data-stu-id="2c001-127">How can I see hello subscription information in Windows events?</span></span>
<span data-ttu-id="2c001-128">Понятное имя идентификатора подписки toohello hello добавьте при добавлении источника hello:</span><span class="sxs-lookup"><span data-stu-id="2c001-128">Append hello subscription ID toohello friendly name while adding hello source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="2c001-129">событие Hello XML имеет следующие метаданные, включая идентификатор подписки hello hello:</span><span class="sxs-lookup"><span data-stu-id="2c001-129">hello event XML has hello following metadata, including hello subscription ID:</span></span>

![XML-файл события][1]

## <a name="error-messages"></a><span data-ttu-id="2c001-131">Сообщения об ошибках</span><span class="sxs-lookup"><span data-stu-id="2c001-131">Error messages</span></span>
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a><span data-ttu-id="2c001-132">При запуске команды hello **azlog createazureid**, возникает следующая ошибка hello?</span><span class="sxs-lookup"><span data-stu-id="2c001-132">When I run hello command **azlog createazureid**, why do I get hello following error?</span></span>
<span data-ttu-id="2c001-133">Ошибка:</span><span class="sxs-lookup"><span data-stu-id="2c001-133">Error:</span></span>

  <span data-ttu-id="2c001-134">*Сбой toocreate AAD приложения - клиента 72f988bf-86f1-41af-91ab-2d7cd011db37 - причина = «Запрещено» — сообщение = «Недостаточно прав доступа операция toocomplete hello».*</span><span class="sxs-lookup"><span data-stu-id="2c001-134">*Failed toocreate AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges toocomplete hello operation.'*</span></span>

<span data-ttu-id="2c001-135">Hello **azlog createazureid** toocreate участника службы на все клиенты hello Azure AD для hello подписок, которые hello Azure имя входа имеет доступ к предпринимается.</span><span class="sxs-lookup"><span data-stu-id="2c001-135">hello **azlog createazureid** command attempts toocreate a service principal in all hello Azure AD tenants for hello subscriptions that hello Azure login has access to.</span></span> <span data-ttu-id="2c001-136">Если имя входа Azure только гостя в этом клиенте Azure AD, hello команда выдает «операция hello toocomplete недостаточно прав доступа».</span><span class="sxs-lookup"><span data-stu-id="2c001-136">If your Azure login is only a guest user in that Azure AD tenant, hello command fails with "Insufficient privileges toocomplete hello operation."</span></span> <span data-ttu-id="2c001-137">Попросите администратора tooadd клиента hello вашу учетную запись как пользователя в клиенте hello.</span><span class="sxs-lookup"><span data-stu-id="2c001-137">Ask hello tenant admin tooadd your account as a user in hello tenant.</span></span>

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a><span data-ttu-id="2c001-138">При запуске команды hello **azlog авторизовать**, возникает следующая ошибка hello?</span><span class="sxs-lookup"><span data-stu-id="2c001-138">When I run hello command **azlog authorize**, why do I get hello following error?</span></span>
<span data-ttu-id="2c001-139">Ошибка:</span><span class="sxs-lookup"><span data-stu-id="2c001-139">Error:</span></span>

  <span data-ttu-id="2c001-140">*Предупреждение назначение роли - AuthorizationFailed: hello клиента janedo@microsoft.com' с объектом «fe9e03e4-4dad-4328-910f-fd24a9660bd2» идентификатор не имеет авторизации tooperform действия «Microsoft.Authorization/roleAssignments/write» с областью "/ подписки и 70d 95299-d689-4c 97-b971-0d8ff0000000 ".*</span><span class="sxs-lookup"><span data-stu-id="2c001-140">*Warning creating Role Assignment - AuthorizationFailed: hello client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="2c001-141">Hello **авторизовать azlog** команда присваивает hello роль участника службы чтения toohello Azure AD (создан с **azlog createazureid**) toohello предоставленный подписок.</span><span class="sxs-lookup"><span data-stu-id="2c001-141">hello **azlog authorize** command assigns hello role of reader toohello Azure AD service principal (created with **azlog createazureid**) toohello provided subscriptions.</span></span> <span data-ttu-id="2c001-142">Если hello Azure имя входа не является администратором или владельцем подписки hello, происходит сбой с сообщением об ошибке «Ошибка авторизации».</span><span class="sxs-lookup"><span data-stu-id="2c001-142">If hello Azure login is not a co-administrator or an owner of hello subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="2c001-143">Azure на основе ролей управления доступом (RBAC) совместного администратора или владельца является необходимые toocomplete это действие.</span><span class="sxs-lookup"><span data-stu-id="2c001-143">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed toocomplete this action.</span></span>

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a><span data-ttu-id="2c001-144">Где можно найти hello определения свойств hello в журнал аудита hello</span><span class="sxs-lookup"><span data-stu-id="2c001-144">Where can I find hello definition of hello properties in hello audit log?</span></span>
<span data-ttu-id="2c001-145">См.:</span><span class="sxs-lookup"><span data-stu-id="2c001-145">See:</span></span>

* <span data-ttu-id="2c001-146">[Просмотр журналов действий для аудита действий с ресурсами](../azure-resource-manager/resource-group-audit.md);</span><span class="sxs-lookup"><span data-stu-id="2c001-146">[Audit operations with Azure Resource Manager](../azure-resource-manager/resource-group-audit.md)</span></span>
* [<span data-ttu-id="2c001-147">Перечисление событий управления hello в подписке в API REST Azure монитор hello</span><span class="sxs-lookup"><span data-stu-id="2c001-147">List hello management events in a subscription in hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="2c001-148">Где найти подробные сведения об оповещениях центра безопасности Azure?</span><span class="sxs-lookup"><span data-stu-id="2c001-148">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="2c001-149">В разделе [toosecurity управление и отвечает на запросы предупреждения в центр безопасности Azure](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="2c001-149">See [Managing and responding toosecurity alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="2c001-150">Как изменить, что именно должна собирать система диагностики виртуальных машин?</span><span class="sxs-lookup"><span data-stu-id="2c001-150">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="2c001-151">Подробные сведения о как tooget, изменять и установки конфигурации диагностики Azure hello, [tooenable с помощью PowerShell диагностики Azure в виртуальной машине под управлением Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c001-151">For details on how tooget, modify, and set hello Azure Diagnostics configuration, see [Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="2c001-152">Следующий пример Hello получает конфигурацию диагностики Azure hello:</span><span class="sxs-lookup"><span data-stu-id="2c001-152">hello following example gets hello Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="2c001-153">Следующий пример Hello изменяет конфигурацию системы диагностики Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2c001-153">hello following example modifies hello Azure Diagnostics configuration.</span></span> <span data-ttu-id="2c001-154">В этой конфигурации только идентификатор 4624 событие и идентификатор 4625 собираются из журнала событий безопасности hello.</span><span class="sxs-lookup"><span data-stu-id="2c001-154">In this configuration, only event ID 4624 and event ID 4625 are collected from hello security event log.</span></span> <span data-ttu-id="2c001-155">Microsoft Antimalware для событий Azure собираются из журнала событий системы hello.</span><span class="sxs-lookup"><span data-stu-id="2c001-155">Microsoft Antimalware for Azure events are collected from hello system event log.</span></span> <span data-ttu-id="2c001-156">При использовании hello выражений XPath Подробнее [потребление событий](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="2c001-156">For details on hello use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="2c001-157">Hello следующий пример задает конфигурацию диагностики Azure hello:</span><span class="sxs-lookup"><span data-stu-id="2c001-157">hello following example sets hello Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="2c001-158">После внесения изменений, проверьте tooensure учетной записи хранилища hello, исправьте события собираются hello.</span><span class="sxs-lookup"><span data-stu-id="2c001-158">After you make changes, check hello storage account tooensure that hello correct events are collected.</span></span>

<span data-ttu-id="2c001-159">При наличии проблем во время установки hello и конфигурации, откройте [запрос на получение поддержки](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span><span class="sxs-lookup"><span data-stu-id="2c001-159">If you have any issues during hello installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="2c001-160">Выберите **интеграции журнала** как служба hello, для которого запрашивается поддержка.</span><span class="sxs-lookup"><span data-stu-id="2c001-160">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="2c001-161">Можно использовать журналы Наблюдатель сети toointegrate журнала интеграции Azure в моей SIEM</span><span class="sxs-lookup"><span data-stu-id="2c001-161">Can I use Azure Log Integration toointegrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="2c001-162">Служба "Наблюдатель за сетями Azure" создает множество сведений о журналах.</span><span class="sxs-lookup"><span data-stu-id="2c001-162">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="2c001-163">Эти журналы не предназначены toobe отправляемых tooa SIEM.</span><span class="sxs-lookup"><span data-stu-id="2c001-163">These logs are not meant toobe sent tooa SIEM.</span></span> <span data-ttu-id="2c001-164">Назначение Hello поддерживается только для журналов Наблюдатель сети — учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="2c001-164">hello only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="2c001-165">Интеграция Azure журнала не поддерживает чтение этих журналов и сделать их доступными tooa SIEM.</span><span class="sxs-lookup"><span data-stu-id="2c001-165">Azure Log Integration does not support reading these logs and making them available tooa SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
