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
# <a name="azure-log-integration-faq"></a>Часто задаваемые вопросы об интеграции журналов Azure
В этой статье содержатся ответы на некоторые часто задаваемые вопросы о службе интеграции журналов Azure. 

Интеграция Azure журнала является служба операционной системы Windows, можно использовать журналы необработанных toointegrate по вашим ресурсам Azure в вашей локальной безопасности сведения и событий (SIEM) систем управления. Такая интеграция обеспечивает единый панели мониторинга для каждого из ОС, локально или в облаке hello. Интеграция также позволяет выполнять статистическое вычисление, сопоставление и анализ, а также предупреждать о событиях безопасности, связанных с приложениями.

## <a name="is-hello-azure-log-integration-software-free"></a>— Это программное обеспечение интеграции Azure журнала hello бесплатно?
Да. Нет бесплатно hello программным обеспечением для интеграции журналов Azure.

## <a name="where-is-azure-log-integration-available"></a>Где доступна служба интеграции журналов Azure?

Сейчас служба доступна в рамках коммерческой лицензии Azure и лицензии Azure для государственных организаций и недоступна в Китае и в Германии.

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a>Просмотр учетных записей хранения hello, из которых интеграции Azure журнала запрашивает журналы виртуальной Машине Azure?
Выполните команду hello **azlog исходного списка**.

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a>Как узнать, какие подписки hello Azure Integration журнала записываются из?

В случае, когда hello журналы аудита, которые помещаются в hello **AzureResourcemanagerJson** каталоги, идентификатор подписки hello — в файле журнала hello. Это справедливо для журналов в hello **AzureSecurityCenterJson** папки. Например:

20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json

Журналы аудита Azure Active Directory включают hello идентификатор клиента как часть имени hello.

Журналы диагностики, которые считываются из концентратора событий не включают идентификатор подписки hello как часть имени hello. Вместо этого они включают hello понятное имя, указанное как часть создания hello источника концентратора событий hello. 

## <a name="how-can-i-update-hello-proxy-configuration"></a>Как обновить настройки прокси-сервера hello
Если параметра прокси не позволяет непосредственно для доступа к хранилищу Azure, откройте hello **AZLOG. EXE-ФАЙЛА. КОНФИГУРАЦИИ** файла в **c:\Program Files\Microsoft Azure журнала интеграции**. Обновление hello файл tooinclude hello **defaultProxy** раздел с hello адрес прокси-сервера в вашей организации. После завершения обновления hello остановить и запустить службу hello с помощью команд hello **azlog net stop** и **команда net start azlog**.

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

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a>Просмотр сведений о подписке hello в событиях Windows?
Понятное имя идентификатора подписки toohello hello добавьте при добавлении источника hello:

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
событие Hello XML имеет следующие метаданные, включая идентификатор подписки hello hello:

![XML-файл события][1]

## <a name="error-messages"></a>Сообщения об ошибках
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a>При запуске команды hello **azlog createazureid**, возникает следующая ошибка hello?
Ошибка:

  *Сбой toocreate AAD приложения - клиента 72f988bf-86f1-41af-91ab-2d7cd011db37 - причина = «Запрещено» — сообщение = «Недостаточно прав доступа операция toocomplete hello».*

Hello **azlog createazureid** toocreate участника службы на все клиенты hello Azure AD для hello подписок, которые hello Azure имя входа имеет доступ к предпринимается. Если имя входа Azure только гостя в этом клиенте Azure AD, hello команда выдает «операция hello toocomplete недостаточно прав доступа». Попросите администратора tooadd клиента hello вашу учетную запись как пользователя в клиенте hello.

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a>При запуске команды hello **azlog авторизовать**, возникает следующая ошибка hello?
Ошибка:

  *Предупреждение назначение роли - AuthorizationFailed: hello клиента janedo@microsoft.com' с объектом «fe9e03e4-4dad-4328-910f-fd24a9660bd2» идентификатор не имеет авторизации tooperform действия «Microsoft.Authorization/roleAssignments/write» с областью "/ подписки и 70d 95299-d689-4c 97-b971-0d8ff0000000 ".*

Hello **авторизовать azlog** команда присваивает hello роль участника службы чтения toohello Azure AD (создан с **azlog createazureid**) toohello предоставленный подписок. Если hello Azure имя входа не является администратором или владельцем подписки hello, происходит сбой с сообщением об ошибке «Ошибка авторизации». Azure на основе ролей управления доступом (RBAC) совместного администратора или владельца является необходимые toocomplete это действие.

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a>Где можно найти hello определения свойств hello в журнал аудита hello
См.:

* [Просмотр журналов действий для аудита действий с ресурсами](../azure-resource-manager/resource-group-audit.md);
* [Перечисление событий управления hello в подписке в API REST Azure монитор hello](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a>Где найти подробные сведения об оповещениях центра безопасности Azure?
В разделе [toosecurity управление и отвечает на запросы предупреждения в центр безопасности Azure](../security-center/security-center-managing-and-responding-alerts.md).

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a>Как изменить, что именно должна собирать система диагностики виртуальных машин?
Подробные сведения о как tooget, изменять и установки конфигурации диагностики Azure hello, [tooenable с помощью PowerShell диагностики Azure в виртуальной машине под управлением Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Следующий пример Hello получает конфигурацию диагностики Azure hello:

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

Следующий пример Hello изменяет конфигурацию системы диагностики Azure hello. В этой конфигурации только идентификатор 4624 событие и идентификатор 4625 собираются из журнала событий безопасности hello. Microsoft Antimalware для событий Azure собираются из журнала событий системы hello. При использовании hello выражений XPath Подробнее [потребление событий](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

Hello следующий пример задает конфигурацию диагностики Azure hello:

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

После внесения изменений, проверьте tooensure учетной записи хранилища hello, исправьте события собираются hello.

При наличии проблем во время установки hello и конфигурации, откройте [запрос на получение поддержки](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request). Выберите **интеграции журнала** как служба hello, для которого запрашивается поддержка.

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a>Можно использовать журналы Наблюдатель сети toointegrate журнала интеграции Azure в моей SIEM

Служба "Наблюдатель за сетями Azure" создает множество сведений о журналах. Эти журналы не предназначены toobe отправляемых tooa SIEM. Назначение Hello поддерживается только для журналов Наблюдатель сети — учетная запись хранения. Интеграция Azure журнала не поддерживает чтение этих журналов и сделать их доступными tooa SIEM.

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
