---
title: "aaaCannot подключения с tooa протокола удаленного рабочего СТОЛА виртуальной Машины Windows в Azure | Документы Microsoft"
description: "Устранение неполадок при подключении виртуальной машины Windows tooyour в Azure с помощью удаленного рабочего стола"
keywords: "Ошибка удаленного рабочего стола, ошибка подключения удаленного рабочего стола не удается подключиться к tooVM, удаленного рабочего стола устранения неполадок"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 0d740f8e-98b8-4e55-bb02-520f604f5b18
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: bbb36136e7a4b187fe8deea621d2b8d46d8aa102
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-remote-desktop-connections-tooan-azure-virtual-machine"></a>Устранение неполадок подключения удаленного рабочего стола tooan виртуальной машины Azure
Hello удаленного рабочего стола (RDP) подключения tooyour на основе Windows Azure виртуальной машины (VM) может завершиться ошибкой по различным причинам, позволяя невозможно tooaccess ВМ. Hello проблему можно с помощью hello службы удаленного рабочего стола на hello виртуальной Машины, hello сетевого подключения или hello клиента удаленного рабочего стола на компьютере узла. В этой статье поможет выполнить некоторые hello наиболее распространенных методов tooresolve RDP проблем с подключением. 

Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/support/forums/). Кроме того, можно зарегистрировать обращение в службу поддержки Azure. Go toohello [сайт поддержки Azure](https://azure.microsoft.com/support/options/) и выберите **получения поддержки**.

<a id="quickfixrdp"></a>

## <a name="quick-troubleshooting-steps"></a>Действия по устранению неполадок
После каждого действия по устранению неполадок попробуйте подключиться toohello виртуальной Машины:

1. Выполните сброс конфигурации удаленного рабочего стола.
2. Проверьте правила групп безопасности сети или конечные точки облачных служб.
3. Проверьте журналы консоли виртуальной машины.
4. Сброс hello сетевой Адаптер для виртуальной Машины hello.
5. Здравствуйте, проверьте работоспособность ресурсов виртуальной Машины.
6. Сбросьте пароль виртуальной машины.
7. Перезапустите виртуальную машину.
8. Заново разверните виртуальную машину.

Читайте статью дальше, если вам нужны более подробные инструкции или пояснения. Убедитесь, что локальное сетевое оборудование, такое как маршрутизаторы и брандмауэры, не блокирует исходящий TCP-порт 3389, как указано в [подробных сценариях устранения неполадок RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!TIP]
> Если hello **Connect** кнопку ВМ помещает неактивен hello портале и вы не подключенных tooAzure через [Express Route](../../expressroute/expressroute-introduction.md) или [через виртуальную Частную сеть для](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) подключения, необходимо toocreate и назначение адресов ВМ общедоступный IP-адрес перед могли использовать RDP. Дополнительные сведения см. в статье [IP-адреса в Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).


## <a name="ways-tootroubleshoot-rdp-issues"></a>Выдает tootroubleshoot способы протокола удаленного рабочего СТОЛА
Виртуальные машины, созданные с помощью модели развертывания диспетчера ресурсов hello с помощью одного из следующих методов hello устранения:

* [Портал Azure](#using-the-azure-portal) - нормально, если вам требуется tooquickly Сброс hello RDP конфигурации или учетные данные пользователя и не hello установлены средства Azure.
* [Azure PowerShell](#using-azure-powershell) — Если вы знакомы с командную строку PowerShell быстро сброса hello RDP конфигурации или учетные данные пользователя с помощью командлетов Azure PowerShell hello.

Можно также найти шаги по устранению неполадок виртуальных машин, созданных с помощью hello [классической модели развертывания](#troubleshoot-vms-created-using-the-classic-deployment-model).

<a id="fix-common-remote-desktop-errors"></a>

## <a name="troubleshoot-using-hello-azure-portal"></a>Устранение неполадок с помощью портала Azure hello
После каждого действия по устранению неполадок повторите попытку подключения tooyour виртуальной Машины. Если вы по-прежнему не удается подключиться, попробуйте hello следующий шаг.

1. **Сбросьте подключение к удаленному рабочему столу**. Этот шаг по устранению неполадок Сброс конфигурации протокола удаленного рабочего СТОЛА hello, удаленные соединения отключены или правила брандмауэра Windows блокируют RDP, например.
   
    Выберите виртуальную Машину в hello портал Azure. Прокрутите вниз hello параметры области toohello **поддержки + Устранение неполадок** раздела нижней части списка hello. Нажмите кнопку hello **сброс пароля** кнопки. Набор hello **режим** слишком**сброса конфигурации только** и нажмите кнопку hello **обновление** кнопки:
   
    ![Сброс конфигурации протокола удаленного рабочего СТОЛА hello в hello портал Azure](./media/troubleshoot-rdp-connection/reset-rdp.png)
2. **Проверьте правила группы безопасности сети**. Используйте [проверить поток IP](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) tooconfirm, если правила в группе безопасности сети блокирует tooor трафик от виртуальной машины. Можно также просмотреть действующие безопасности группы, которую правила входящих подключений tooensure NSG «разрешить» правило существует и приоритет для порта протокола удаленного рабочего СТОЛА (по умолчанию 3389). Дополнительные сведения см. в разделе [поток трафика с помощью действующие правила безопасности tootroubleshoot виртуальной Машины](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

3. **Просмотрите данные диагностики загрузки виртуальной машины**. Этот шаг по устранению неполадок проверки toodetermine журналы консоли виртуальной Машины hello, если hello виртуальной Машины сообщение о проблеме. Не на всех виртуальных машинах включена диагностика загрузки, поэтому это действие может быть необязательным.
   
    Конкретные действия по устранению неполадок выходят за рамки данной статьи hello, но также может указывать на проблему шире, затрагивающее подключение RDP. Дополнительные сведения о просмотре журналов консоли hello или снимок виртуальной Машины см. в разделе [Диагностика загрузки для виртуальных машин](boot-diagnostics.md).

4. **Сброс hello сетевой Адаптер для виртуальной Машины hello**. Дополнительные сведения см. в разделе [как сетевой Адаптер для виртуальной Машины Windows Azure tooreset](reset-network-interface.md).
5. **Проверьте hello исправности ресурсов для виртуальной Машины**. Этот шаг по устранению неполадок, подтверждает, что нет известных проблем с hello платформы Azure может оказать влияние на toohello подключения к виртуальной Машине.
   
    Выберите виртуальную Машину в hello портал Azure. Прокрутите вниз hello параметры области toohello **поддержки + Устранение неполадок** раздела нижней части списка hello. Нажмите кнопку hello **исправности ресурсов** кнопки. Если виртуальная машина работоспособна, то отобразится состояние **Доступно**:
   
    ![Проверьте работоспособность ресурсов виртуальной Машины в hello портал Azure](./media/troubleshoot-rdp-connection/check-resource-health.png)
6. **Сбросьте учетные данные пользователей**. Этот шаг по устранению неполадок сбрасывает hello пароля учетной записи локального администратора при неизвестна или забыл hello учетные данные.
   
    Выберите виртуальную Машину в hello портал Azure. Прокрутите вниз hello параметры области toohello **поддержки + Устранение неполадок** раздела нижней части списка hello. Нажмите кнопку hello **сброс пароля** кнопки. Убедитесь, что hello **режим** задано слишком**сброс пароля** и введите свое имя пользователя и новый пароль. Наконец, нажмите кнопку hello **обновление** кнопки:
   
    ![Сброс учетных данных пользователя hello в hello портал Azure](./media/troubleshoot-rdp-connection/reset-password.png)
7. **Перезапустите виртуальную машину**. Это можно исправить проблемы с базовой испытывает hello самой ВМ.
   
    Выберите виртуальную Машину в hello портал Azure и щелкните hello **Обзор** вкладки. Нажмите кнопку hello **перезапустите** кнопки:
   
    ![Перезапустите hello виртуальной Машины в hello портал Azure](./media/troubleshoot-rdp-connection/restart-vm.png)
8. **Заново разверните виртуальную машину**. Этот шаг по устранению неполадок повторно развертывает tooanother узла виртуальной Машины в Azure toocorrect проблем базовой платформе или в сети.
   
    Выберите виртуальную Машину в hello портал Azure. Прокрутите вниз hello параметры области toohello **поддержки + Устранение неполадок** раздела нижней части списка hello. Нажмите кнопку hello **повторно развернуть** , а затем нажмите **повторно развернуть**:
   
    ![Повторное развертывание hello виртуальной Машины в hello портал Azure](./media/troubleshoot-rdp-connection/redeploy-vm.png)
   
    После завершения этой операции временных диска данных — потеряны и динамических IP-адресов, связанных с виртуальной Машины обновляются hello.

Если у вас по-прежнему возникают проблемы с протоколом RDP, то вы можете [отправить запрос в службу поддержки](https://azure.microsoft.com/support/options/) или прочитать [более подробные сведения об основных понятиях и этапах устранения неполадок RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-using-azure-powershell"></a>Устранение неполадок с помощью Azure PowerShell
Если это еще не сделано, [Установка и настройка hello последнюю версию Azure PowerShell](/powershell/azure/overview).

Hello следующих примерах используются переменные например `myResourceGroup`, `myVM`, и `myVMAccessExtension`. Замените имена этих переменных и расположения собственными значениями.

> [!NOTE]
> Сброс учетных данных пользователя hello и hello конфигурации протокола удаленного рабочего СТОЛА с помощью hello [AzureRmVMAccessExtension набор](/powershell/module/azurerm.compute/set-azurermvmaccessextension) командлета PowerShell. В следующие примеры, hello `myVMAccessExtension` — это имя, укажите в рамках процесса hello. Если вы ранее работали с hello VMAccessAgent, можно получить имя hello hello существующего модуля с помощью `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` свойств hello toocheck hello виртуальной Машины. Имя tooview hello, найдите в разделе "" hello «расширения» hello выходных данных.

После каждого действия по устранению неполадок повторите попытку подключения tooyour виртуальной Машины. Если вы по-прежнему не удается подключиться, попробуйте hello следующий шаг.

1. **Сбросьте подключение к удаленному рабочему столу**. Этот шаг по устранению неполадок Сброс конфигурации протокола удаленного рабочего СТОЛА hello, удаленные соединения отключены или правила брандмауэра Windows блокируют RDP, например.
   
    Выполните пример Hello сбрасывает hello RDP-подключение на виртуальной Машине с именем `myVM` в hello `WestUS` расположение и в группе ресурсов hello с именем `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location Westus -Name "myVMAccessExtension"
    ```
2. **Проверьте правила группы безопасности сети**. Проверяет, имеется правило в группы безопасности сети трафик протокола удаленного рабочего СТОЛА toopermit ли этот шаг по устранению неполадок. Hello по умолчанию для протокола удаленного рабочего СТОЛА используется порт TCP-порт 3389. Трафик RDP toopermit правило может быть создан автоматически при создании ВМ.
   
    Во-первых, назначьте все данные конфигурации hello для вашей группы безопасности сети toohello `$rules` переменной. Hello следующий пример извлекает сведения о сетевой группы безопасности с именем hello `myNetworkSecurityGroup` в группе ресурсов hello с именем `myResourceGroup`:
   
    ```powershell
    $rules = Get-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
        -Name "myNetworkSecurityGroup"
    ```
   
    Теперь Просмотр hello правил, настроенных для этой группы безопасности сети. Убедитесь, что правило существует tooallow TCP-порт 3389 для входящих подключений следующим образом:
   
    ```powershell
    $rules.SecurityRules
    ```
   
    Hello примере показан допустимый безопасности правило, разрешающее трафик RDP. Можно увидеть, что параметры `Protocol`, `DestinationPortRange`, `Access` и `Direction` настроены правильно:
   
    ```powershell
    Name                     : default-allow-rdp
    Id                       : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/default-allow-rdp
    Etag                     : 
    ProvisioningState        : Succeeded
    Description              : 
    Protocol                 : TCP
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : *
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 1000
    Direction                : Inbound
    ```
   
    Если у вас нет правила, разрешающего трафик RDP, [создайте правило группы безопасности сети](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Разрешите использование TCP-порта 3389.
3. **Сбросьте учетные данные пользователей**. Этот шаг по устранению неполадок сбрасывает hello пароль для учетной записи локального администратора hello, указываемой при неизвестен или забыл hello учетные данные.
   
    Во-первых, укажите Здравствуйте, имя пользователя и новый пароль, назначив учетные данные toohello `$cred` переменной следующим образом:
   
    ```powershell
    $cred=Get-Credential
    ```
   
    Теперь обновите учетные данные hello на ВМ. Hello следующий пример обновляет hello учетные данные на виртуальной Машине с именем `myVM` в hello `WestUS` расположение и в группе ресурсов hello с именем `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location WestUS -Name "myVMAccessExtension" `
        -UserName $cred.GetNetworkCredential().Username `
        -Password $cred.GetNetworkCredential().Password
    ```
4. **Перезапустите виртуальную машину**. Это можно исправить проблемы с базовой испытывает hello самой ВМ.
   
    Следующий пример перезапускается Hello hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`:
   
    ```powershell
    Restart-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
    ```
5. **Заново разверните виртуальную машину**. Этот шаг по устранению неполадок повторно развертывает tooanother узла виртуальной Машины в Azure toocorrect проблем базовой платформе или в сети.
   
    Следующий пример повторно развертывает Hello hello виртуальной Машины с именем `myVM` в hello `WestUS` расположение и в группе ресурсов hello с именем `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

Если у вас по-прежнему возникают проблемы с протоколом RDP, то вы можете [отправить запрос в службу поддержки](https://azure.microsoft.com/support/options/) или прочитать [более подробные сведения об основных понятиях и этапах устранения неполадок RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-vms-created-using-hello-classic-deployment-model"></a>Устранение неполадок виртуальных машин, созданных с помощью hello классической модели развертывания
После каждого действия по устранению неполадок выполните повторное подключение toohello виртуальной Машины.

1. **Сбросьте подключение к удаленному рабочему столу**. Этот шаг по устранению неполадок Сброс конфигурации протокола удаленного рабочего СТОЛА hello, удаленные соединения отключены или правила брандмауэра Windows блокируют RDP, например.
   
    Выберите виртуальную Машину в hello портал Azure. Нажмите кнопку hello **... Дополнительные** , а затем нажмите кнопку **сброса удаленного доступа**:
   
    ![Сброс конфигурации протокола удаленного рабочего СТОЛА hello в hello портал Azure](./media/troubleshoot-rdp-connection/classic-reset-rdp.png)
2. **Проверьте конечные точки облачных служб**. Этот шаг по устранению неполадок проверяет, имеют конечные точки в трафика RDP toopermit облачных служб. Hello по умолчанию для протокола удаленного рабочего СТОЛА используется порт TCP-порт 3389. Трафик RDP toopermit правило может быть создан автоматически при создании ВМ.
   
   Выберите виртуальную Машину в hello портал Azure. Нажмите кнопку hello **конечные точки** кнопку hello tooview конечных точек, настроенных для вашей виртуальной Машины. Убедитесь, что существуют конечные точки, разрешающие трафик RDP через TCP-порт 3389.
   
   Следующий пример Hello показаны допустимые конечные точки, которые разрешают трафик RDP.
   
   ![Проверка конечных точек облачных служб в hello портал Azure](./media/troubleshoot-rdp-connection/classic-verify-cloud-services-endpoints.png)
   
   Если у вас нет конечной точки, разрешающей трафик RDP, [создайте конечную точку облачных служб](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Разрешить tooprivate порт 3389 TCP-подключения.
3. **Просмотрите данные диагностики загрузки виртуальной машины**. Этот шаг по устранению неполадок проверки toodetermine журналы консоли виртуальной Машины hello, если hello виртуальной Машины сообщение о проблеме. Не на всех виртуальных машинах включена диагностика загрузки, поэтому это действие может быть необязательным.
   
    Конкретные действия по устранению неполадок выходят за рамки данной статьи hello, но также может указывать на проблему шире, затрагивающее подключение RDP. Дополнительные сведения о просмотре журналов консоли hello или снимок виртуальной Машины см. в разделе [Диагностика загрузки для виртуальных машин](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).
4. **Проверьте hello исправности ресурсов для виртуальной Машины**. Этот шаг по устранению неполадок, подтверждает, что нет известных проблем с hello платформы Azure может оказать влияние на toohello подключения к виртуальной Машине.
   
    Выберите виртуальную Машину в hello портал Azure. Прокрутите вниз hello параметры области toohello **поддержки + Устранение неполадок** раздела нижней части списка hello. Нажмите кнопку hello **исправности ресурсов** кнопки. Если виртуальная машина работоспособна, то отобразится состояние **Доступно**:
   
    ![Проверьте работоспособность ресурсов виртуальной Машины в hello портал Azure](./media/troubleshoot-rdp-connection/classic-check-resource-health.png)
5. **Сбросьте учетные данные пользователей**. Этот шаг по устранению неполадок сбрасывает hello пароль учетной записи локального администратора hello, если есть сомнения в том или забыл hello учетные данные.
   
    Выберите виртуальную Машину в hello портал Azure. Прокрутите вниз hello параметры области toohello **поддержки + Устранение неполадок** раздела нижней части списка hello. Нажмите кнопку hello **сброс пароля** кнопки. Введите свое имя пользователя и новый пароль. Наконец, нажмите кнопку hello **Сохранить** кнопки:
   
    ![Сброс учетных данных пользователя hello в hello портал Azure](./media/troubleshoot-rdp-connection/classic-reset-password.png)
6. **Перезапустите виртуальную машину**. Это можно исправить проблемы с базовой испытывает hello самой ВМ.
   
    Выберите виртуальную Машину в hello портал Azure и щелкните hello **Обзор** вкладки. Нажмите кнопку hello **перезапустите** кнопки:
   
    ![Перезапустите hello виртуальной Машины в hello портал Azure](./media/troubleshoot-rdp-connection/classic-restart-vm.png)

Если у вас по-прежнему возникают проблемы с протоколом RDP, то вы можете [отправить запрос в службу поддержки](https://azure.microsoft.com/support/options/) или прочитать [более подробные сведения об основных понятиях и этапах устранения неполадок RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-specific-rdp-errors"></a>Устранение определенных ошибок RDP
Может появиться сообщение об ошибке при попытке tooconnect tooyour ВМ через RDP. Hello ниже приведены распространенные сообщения об ошибках hello.

* [Hello удаленный сеанс был отключен, поскольку отсутствуют лицензии не tooprovide доступные серверы лицензирования удаленных рабочих столов](troubleshoot-specific-rdp-errors.md#rdplicense).
* [Удаленный рабочий стол не может найти hello компьютера «name»](troubleshoot-specific-rdp-errors.md#rdpname).
* [Ошибка проверки подлинности. Hello локального администратора безопасности не удается связаться с](troubleshoot-specific-rdp-errors.md#rdpauth).
* [Ошибка безопасности Windows: учетные данные не работают](troubleshoot-specific-rdp-errors.md#wincred).
* [Этот компьютер не удается подключиться к удаленному компьютеру toohello](troubleshoot-specific-rdp-errors.md#rdpconnect).

## <a name="additional-resources"></a>Дополнительные ресурсы
Когда ни один из этих ошибок и toohello виртуальной Машине через удаленный рабочий стол не удается подключиться, чтение hello подробные [поиск и устранение неисправностей для удаленного рабочего стола](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Действия по устранению неполадок при доступе к приложениям, выполняемым на виртуальной Машине, в разделе [Устранение неполадок доступа tooan приложение, работающее на Виртуальной машине Azure](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Если возникают проблемы с помощью tooa tooconnect Secure Shell (SSH) виртуальной Машины с Linux в Azure, см. раздел [Устранение SSH подключений tooa виртуальных Машин Linux в Azure](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

