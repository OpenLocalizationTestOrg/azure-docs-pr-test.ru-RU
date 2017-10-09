---
title: "aaaRemove серверы и отключите защиту | Документы Microsoft"
description: "Эта статья описывает, как хранилище toounregister серверы из Site Recovery и toodisable защиты для виртуальных машин и физических серверов."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a>Удаление серверов и отключение защиты

вносит свой вклад Hello службы Azure Site Recovery, tooyour бесперебойной работе и стратегии аварийного восстановления (BCDR). управляет служба Hello, репликации, отработки отказа и восстановления виртуальных машин и физических серверов. Машины могут быть реплицированной tooAzure или tooa получателя на локальном центре обработки данных. Краткий обзор см. в статье [Что такое Azure Site Recovery?](site-recovery-overview.md)

Эта статья описывает, как серверы toounregister из служб восстановления хранилище в hello портал Azure, и как toodisable защиту для машин защищена службой восстановления сайтов.

Отправьте все комментарии или вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="unregister-a-connected-configuration-server"></a>Отмена регистрации подключенного сервера конфигурации

Если выполняется репликация виртуальных машин VMware или tooAzure физических серверов Windows и Linux, подключенных конфигурации сервера в хранилище можно отменить регистрацию следующим образом:

1. Отключите защиту виртуальной машины. В **защищенные элементы** > **реплицируются элементы**, машину правой кнопкой мыши hello > **удалить**.
2. Отмените связь для всех политик. В **инфраструктура Site Recovery** > **для VMWare и физических машин** > **политики репликации**, дважды щелкните hello связанные политики. Щелкните правой кнопкой мыши сервер конфигурации hello > **Disassociate**.
3. Удалите дополнительные локальные процессы или главные целевые серверы. В **инфраструктура Site Recovery** > **для VMWare и физических машин** > **серверы конфигурации**, щелкните правой кнопкой мыши сервер hello > **Удалить**.
4. Удалите сервер конфигурации hello.
5. Вручную удалить hello Mobility service на главном целевом сервере hello (это будет либо отдельный сервер или на сервере конфигурации hello).
6. Удалите все дополнительные серверы обработки.
7. Удалите сервер конфигурации hello.
8. На сервере конфигурации hello удаления hello экземпляра MySQL, установленной с Site Recovery.
9. В реестре hello сервера конфигурации hello удалить ключ hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-unconnected-configuration-server"></a>Отмена регистрации неподключенного сервера конфигурации

Если выполняется репликация виртуальных машин VMware или tooAzure физических серверов Windows и Linux, изолированной конфигурации сервера в хранилище можно отменить регистрацию следующим образом:

1. Отключите защиту виртуальной машины. В **защищенные элементы** > **реплицируются элементы**, машину правой кнопкой мыши hello > **удалить**. Выберите **прекратить управление машиной hello**.
2. Удалите дополнительные локальные процессы или главные целевые серверы. В **инфраструктура Site Recovery** > **для VMWare и физических машин** > **серверы конфигурации**, щелкните правой кнопкой мыши сервер hello > **Удалить**.
3. Удалите сервер конфигурации hello.
4. Вручную удалить hello Mobility service на главном целевом сервере hello (это будет либо отдельный сервер или на сервере конфигурации hello).
5. Удалите все дополнительные серверы обработки.
6. Удалите сервер конфигурации hello.
7. На сервере конфигурации hello удаления hello экземпляра MySQL, установленной с Site Recovery.
8. В реестре hello сервера конфигурации hello удалить ключ hello ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-connected-vmm-server"></a>Отмена регистрации подключенного сервера VMM

По соображениям рекомендуется отменить регистрацию сервера VMM hello при tooAzure соединения. Это гарантирует, что параметры на серверах VMM hello (и на других серверах VMM с облаками парной) будут правильно удалены. Удалять неподключенный сервер рекомендуется только в случае постоянных проблем с соединением. Если сервер VMM hello не подключен, вам потребуется toomanually запуска сценария tooclean параметров.

1. Остановите репликацию виртуальных машин в облаках на сервер VMM требуется tooremove hello.
2. Удалите все сопоставления сетей, используемых облаков на сервер VMM требуется toodelete hello. В **инфраструктура Site Recovery** > **для System Center VMM** > **сетевое сопоставление**, щелкните правой кнопкой мыши сетевое сопоставление hello >  **Удалить**.
3. Отмена связи политики репликации из облака на сервер VMM требуется tooremove hello.  В **инфраструктура Site Recovery** > **для System Center VMM** >  **политики репликации**, дважды щелкните политику связанные hello. Щелкните правой кнопкой мыши облака hello > **Disassociate**.
4. Удалите сервер VMM hello или активного узла VMM. В **инфраструктура Site Recovery** > **для System Center VMM** > **серверов VMM**, щелкните правой кнопкой мыши сервер hello >  **Удалить**.
5. Удалите hello поставщик вручную на сервере VMM hello. При наличии кластера удалите его со всех узлов.
6. При реплицировании tooAzure, вручную удалите агент служб восстановления Microsoft hello из узлов Hyper-V в облаках hello удален.



### <a name="unregister-an-unconnected-vmm-server"></a>Отмена регистрации неподключенного сервера VMM

1. Остановите репликацию виртуальных машин в облаках на сервер VMM требуется tooremove hello.
2. Удалите все сопоставления сетей, используемых облаков на сервере VMM hello, которое следует toodelete. В **инфраструктура Site Recovery** > **для System Center VMM** > **сетевое сопоставление**, щелкните правой кнопкой мыши сетевое сопоставление hello >  **Удалить**.
3. Обратите внимание, идентификатор hello hello сервера VMM.
4. Отмена связи политики репликации из облака на сервер VMM требуется tooremove hello.  В **инфраструктура Site Recovery** > **для System Center VMM** >  **политики репликации**, дважды щелкните политику связанные hello. Щелкните правой кнопкой мыши облака hello > **Disassociate**.
5. Удалите сервер VMM hello или активного узла. В **инфраструктура Site Recovery** > **для System Center VMM** > **серверов VMM**, щелкните правой кнопкой мыши сервер hello >  **Удалить**.
6. Загрузите и запустите hello [скрипт очистки](http://aka.ms/asr-cleanup-script-vmm) на сервере VMM hello. Откройте PowerShell с hello **Запуск от имени администратора** параметр политики выполнения hello toochange для области по умолчанию (LocalMachine) hello. В сценарии hello укажите идентификатор hello hello требуется tooremove сервера VMM. сценарий Hello Удаляет регистрацию и связывания с сервера hello облаков.
5. Выполните сценарий очистки hello на других серверах VMM, содержащие облака, связывать с облаками на сервер VMM требуется tooremove hello.
6. Выполните сценарий очистки hello на любые другие пассивных узлах кластера VMM, имеющих приветствия установлен поставщик.
7. Удалите hello поставщик вручную на сервере VMM hello. При наличии кластера удалите его со всех узлов.
8. Если вы tooAzure репликации можно удалить агент служб восстановления Microsoft hello из узлов Hyper-V в облаках hello удален.

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a>Отмена регистрации узла Hyper-V на сайте Hyper-V

Узлы Hyper-V, которые не управляются с помощью VMM, расположены на сайте Hyper-V. Удалите узел на сайте Hyper-V следующим образом:

1. Отключите репликацию для виртуальных машин Hyper-V, расположенных в узле hello.
2. Отмена связи политики для узла Hyper-V hello. В **инфраструктура Site Recovery** > **для узлов Hyper-V** >  **политики репликации**, дважды щелкните политику связанные hello. Щелкните правой кнопкой мыши узел hello > **Disassociate**.
3. Удалите узлы Hyper-V. В **инфраструктура Site Recovery** > **для System Center VMM** > **узлов Hyper-V**, щелкните правой кнопкой мыши сервер hello >  **Удалить**.
4. Удалите узел hello Hyper-V, после все узлы будут удалены из него. В **инфраструктура Site Recovery** > **для System Center VMM** > **узлов Hyper-V**, щелкните правой кнопкой мыши узел hello >  **Удалить**.
5. Запустите следующий сценарий на каждом узле Hyper-V, который вы удалили hello. Hello скрипт очищает параметры сервера hello и отменяет его регистрацию в хранилище hello.


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a>Отключение защиты для виртуальной машины VMware или физического сервера

1. В **защищенные элементы** > **реплицируются элементы**, машину правой кнопкой мыши hello > **удалить**.
2. В разделе **Удалить виртуальную машину** выберите один из следующих параметров.
    - **Отключите защиту для машины hello (рекомендуется)**. Используйте этот параметр toostop, репликация машины hello. Параметры Site Recovery будут очищены автоматически. Вы увидите только этот параметр в hello при следующих обстоятельствах:
        - **Вы изменили размер тома виртуальной Машины hello**— при изменении размера тома hello виртуальной машина переходит в критическое состояние. Выберите этот параметр toodisables защиту, а также сохранения точек восстановления в Azure. Если вы снова включите защиту для машины hello, hello данные для hello изменения размера тома будут переносятся tooAzure.
        - **После недавно выполнения отработки отказа**— после запуска tootest отработки отказа среды, выберите этот параметр toostart, снова защиты локальных компьютеров. Он отключает каждой виртуальной машины, а затем необходимо tooenable защиты для них еще раз. Отключение компьютера hello, этот параметр не влияет на hello реплики виртуальной машины в Azure. Не удаляйте hello Mobility service из машины hello.
    - **Прекратить управление машиной hello**. Если этот флажок установлен, hello машина будет удалена только из хранилища hello. Параметры защиты в локальной машины hello не будут затронуты. Параметры tooremove на компьютере hello и tooremove машины hello из hello подписки Azure, требуется задать tooclean hello параметры путем удаления hello Mobility service.

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a>Отключение защиты для виртуальной машины Hyper-V в облаке VMM

1. В **защищенные элементы** > **реплицируются элементы**, машину правой кнопкой мыши hello > **удалить**.
2. В разделе **Удалить виртуальную машину** выберите один из следующих параметров.

    - **Отключите защиту для машины hello (рекомендуется)**. Используйте этот параметр toostop, репликация машины hello. Параметры Site Recovery будут очищены автоматически.
    - **Прекратить управление машиной hello**. Если этот флажок установлен, hello машина будет удалена только из хранилища hello. Параметры защиты в локальной машины hello не будут затронуты. Параметры tooremove на компьютере hello и tooremove машины hello из hello подписки Azure, требуется tooclean hello параметры копирования вручную, hello приведенным ниже инструкциям. Обратите внимание, что если выбрать toodelete hello виртуальной машины и ее жестких дисков, они будут удалены из hello целевое расположение.

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a>Очистить параметры защиты — вторичный сайт VMM репликации tooa

Если вы выбрали **прекратить управление машиной hello** и репликация tooa вторичного сайта, выполнения этого скрипта в tooclean сервера-источника hello hello параметров hello основной виртуальной машины. В консоли VMM hello щелкните консоль VMM PowerShell hello tooopen кнопку hello PowerShell. Замените SQLVM1 hello имя виртуальной машины.

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. На вторичном сервере VMM hello выполните этот сценарий tooclean параметров hello hello дополнительная виртуальная машина:

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. На вторичном сервере VMM hello обновите hello виртуальных машин на сервере узла Hyper-V hello, позволяя hello вторичная виртуальная машина получает обнаружил попытку в консоли VMM hello.
4. Hello выше шаги очистить hello параметры репликации на сервере VMM hello. Если требуется toostop репликации для виртуальной машины hello, запустите следующий сценарий ах hello hello первичных и вторичных виртуальных машин. Замените SQLVM1 hello имя виртуальной машины.

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a>Очистить параметры защиты - tooAzure репликации

1. Если вы выбрали **прекратить управление машиной hello** и реплицировать tooAzure, запустите этот скрипт на hello исходном сервере VMM, с помощью PowerShell из консоли VMM hello.
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Hello выше шаги снимите hello параметры репликации на сервере VMM hello. репликация toostop для hello виртуальная машина, работающая на сервере узла Hyper-V hello, запустите этот скрипт. Замените SQLVM1 hello имя виртуальной машины и host01.contoso.com с именем hello hello сервера узла Hyper-V.

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a>Отключение защиты для виртуальной машины Hyper-V на сайте Hyper-V

Эта процедура используется в том случае, если выполняется репликация виртуальных машин Hyper-V tooAzure без сервера VMM.

1. В **защищенные элементы** > **реплицируются элементы**, машину правой кнопкой мыши hello > **удалить**.
2. В **удалить машины**, можно выбрать hello следующие параметры:

   - **Отключите защиту для машины hello (рекомендуется)**. Используйте этот параметр toostop, репликация машины hello. Параметры Site Recovery будут очищены автоматически.
   - **Прекратить управление машиной hello**. Если выбран этот параметр hello машина будет удалена только из хранилища hello. Параметры защиты в локальной машины hello не будут затронуты. Параметры tooremove на компьютере hello и tooremove hello виртуальную машину из hello подписки Azure, требуется tooclean hello параметры копирования вручную. При выборе toodelete hello виртуальной машины и ее жестких дисков, они будут удалены из целевого расположения hello.
3. Если вы выбрали **прекратить управление машиной hello**, запустите этот сценарий на сервере узла Hyper-V источника hello, tooremove репликации для виртуальной машины hello. Замените SQLVM1 hello имя виртуальной машины.

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
