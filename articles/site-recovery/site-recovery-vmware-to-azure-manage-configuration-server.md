---
title: " Управление сервером конфигурации в службе Azure Site Recovery | Документация Майкрософт"
description: "В этой статье описывается как tooset и управления сервером конфигурации."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a>Управление сервером конфигурации

Сервер конфигурации выступает в качестве координатора между службами Site Recovery hello и локальной инфраструктуры. Этой статье описывается, как установить, настроить и управление hello сервер конфигурации.

## <a name="prerequisites"></a>Предварительные требования
Hello ниже приведены hello минимумом оборудования, программного обеспечения и tooset требуется настройка сетевой конфигурации сервера.

> [!NOTE]
> [Планирование мощности](site-recovery-capacity-planner.md) является важным этапом tooensure развертывание hello конфигурации сервера с конфигурацией, наборы требований нагрузки. Дополнительные сведения см. в разделе [Требования к размерам сервера конфигурации](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a>Загрузка программного обеспечения сервера конфигурации hello
1. Войдите в систему toohello Azure tooyour портал и обзор хранилище служб восстановления.
2. Обзор слишком**инфраструктура Site Recovery** > **серверы конфигурации** (в разделе For VMware и физических компьютеров).

  ![Страница "Добавление серверов"](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. Нажмите кнопку hello **+ серверы** кнопки.
4. На hello **добавить сервер** щелкните hello кнопку загрузки toodownload hello регистрационный ключ. Этот ключ необходим во время установки tooregister hello конфигурации сервера с помощью службы Azure Site Recovery.
5. Нажмите кнопку hello **загрузки hello установка единой Microsoft Azure Site Recovery** ссылку toodownload hello последнюю версию hello сервера конфигурации.

  ![Страница загрузки](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  Последняя версия сервера конфигурации hello можно загрузить непосредственно с [загрузки страницы центра загрузки Майкрософт](http://aka.ms/unifiedsetup)

## <a name="installing-and-registering-a-configuration-server-from-gui"></a>Установка и регистрация сервера конфигурации и графического пользовательского интерфейса
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a>Установка и регистрация сервера конфигурации с помощью командой строки

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a>Пример использования
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a>Аргументы командной строки установщика сервера конфигурации
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a>Создание файла учетных данных MySQL
Параметр MySQLCredsFilePath принимает в качестве входных данных файл. Создайте файл hello, используя hello ниже форматирования и передайте его в качестве входного параметра MySQLCredsFilePath.
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a>Создание файла конфигурации параметров прокси-сервера
Параметр ProxySettingsFilePath принимает в качестве входных данных файл. Создайте файл hello, используя hello ниже форматирования и передайте его в качестве входного параметра ProxySettingsFilePath.

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a>Изменение параметров прокси-сервера для сервера конфигурации
1. Tooyour входа сервера конфигурации.
2. Запустите cspsconfigtool.exe hello использованием клавиш hello на ваш.
3. Нажмите кнопку hello **регистрации хранилища** вкладки.
4. Загрузите новый файл регистрации хранилища с портала hello и предоставить ему в качестве входного toohello средства.

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. Укажите сведения о новом прокси-сервера hello и нажмите кнопку hello **зарегистрировать** кнопки.
6. Откройте командную строку PowerShell с правами администратора.
7. Запустите следующую команду hello
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  Если серверы обработки масштабирования присоединенного toothis сервер конфигурации, необходимые слишком[Устранение hello параметры прокси-сервера на всех серверах процесса горизонтального масштабирования hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) в вашем развертывании.

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a>Повторно зарегистрируйте сервер конфигурации с hello же хранилище служб восстановления
  1. Tooyour входа сервера конфигурации.
  2. Запустите cspsconfigtool.exe hello помощью hello ярлыка на рабочем столе.
  3. Нажмите кнопку hello **регистрации хранилища** вкладки.
  4. Загрузите новый файл регистрации с портала hello и предоставить ему в качестве входного toohello средства.
        ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
  5. Укажите сведения hello прокси-сервера и нажмите кнопку hello **зарегистрировать** кнопки.  
  6. Откройте командную строку PowerShell с правами администратора.
  7. Запустите следующую команду hello

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  Если серверы обработки масштабирования присоединенного toothis сервер конфигурации, необходимые слишком[повторно зарегистрировать все серверы обработки масштабирования hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) в вашем развертывании.

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a>Регистрация сервера конфигурации в другом хранилище служб восстановления.
1. Tooyour входа сервера конфигурации.
2. из командной строки администратора, выполните команду hello

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. Запустите cspsconfigtool.exe hello использованием клавиш hello на ваш.
4. Нажмите кнопку hello **регистрации хранилища** вкладки.
5. Загрузите новый файл регистрации с портала hello и предоставить ему в качестве входного toohello средства.

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. Укажите сведения hello прокси-сервера и нажмите кнопку hello **зарегистрировать** кнопки.  
7. Откройте командную строку PowerShell с правами администратора.
8. Запустите следующую команду hello
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a>Списание сервера конфигурации
Убедитесь, следующих hello перед началом ликвидации сервер конфигурации.
1. Отключите защиту для всех виртуальных машин на сервере конфигурации.
2. Отмените регистрацию всех политик репликации из hello сервера конфигурации.
3. Удалите все узлы серверов/vSphere v-Center, toohello связанный сервер конфигурации.

### <a name="delete-hello-configuration-server-from-azure-portal"></a>Удалить сервер конфигурации hello из портала Azure
1. На портале Azure перейдите слишком**инфраструктура Site Recovery** > **серверы конфигурации** hello хранилище меню.
2. Выберите сервер конфигурации, которые должны toodecommission hello.
3. На странице приветствия конфигурации сервера нажмите кнопку Удалить hello.

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. Нажмите кнопку **Да** tooconfirm hello удаления сервера hello.

  >[!WARNING]
  Если вы используете виртуальные машины, политики репликации или узлов vCenter серверов/vSphere, связанный с этим сервером конфигурации, невозможно удалить сервер hello. Удалите эти сущности, прежде чем пытаться toodelete hello хранилища.

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a>Удаление программного обеспечения сервера конфигурации hello и его зависимостей
  > [!TIP]
  Если планируется hello tooreuse сервер конфигурации с помощью Azure Site Recovery, то можно пропустить toostep 4 напрямую

1. Войдите на сервер конфигурации toohello с правами администратора.
2. Откройте "Панель управления > Программы > Удалить программы".
3. Удалите программы hello в hello следующая последовательность:
  * агент служб восстановления Microsoft Azure.
  * Microsoft Azure Site Recovery Mobility Service/Master Target Server (Microsoft Azure Site Recovery Mobility Service/главный целевой сервер)
  * Microsoft Azure Site Recovery Provider (Поставщик Microsoft Azure Site Recovery)
  * серверы конфигурации и обработки Microsoft Azure Site Recovery;
  * зависимости сервера конфигурации Microsoft Azure Site Recovery;
  * MySQL Server 5.5
4. Выполните следующую команду из hello и командную строку администратора.
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a>Обновление сертификатов Secure Socket Layer (SSL) конфигурации сервера
Сервер конфигурации Hello встроенных веб-сервер, который координирует действия hello hello службы Mobility Service серверы обработки и главные целевые серверы подключение toohello сервер конфигурации. Hello конфигурации сервера веб-сервер использует сертификат SSL tooauthenticate своих клиентов. Этот сертификат содержит срока действия составляет три года и могут быть обновлены в любое время с помощью hello следующий метод:

> [!WARNING]
Сертификат можно обновить до окончания его срока действия для версии 9.4.XXXX.X и выше. Обновить все компоненты hello Azure Site Recovery (сервер конфигурации, сервер обработки, главного целевого сервера, служба Mobility Service) перед запуском рабочего процесса обновления сертификатов hello.

1. В hello портал Azure — Обзор tooyour хранилище > инфраструктура Site Recovery > сервер конфигурации.
2. Выберите сервер конфигурации hello, для которого требуется toorenew SSL-сертификат для hello.
3. Под hello работоспособности конфигурации сервера вы увидите hello даты истечения срока действия для hello SSL-сертификат.
4. Обновить сертификат hello, щелкнув hello **обновить сертификаты** действие, как показано в hello после изображения:

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a>Предупреждение об окончании срока сертификата Secure Socket Layer

> [!NOTE]
Hello действия сертификата SSL для всех установок, которые произошли перед май 2016 г. было задано tooone года. Вы запустили видеть уведомления о срока действия сертификатов, отображаются в hello портал Azure.

1. Если SSL-сертификата сервера конфигурации hello будут tooexpire в hello следующих двух месяцев, hello служба запускается, связанные с уведомлением пользователей через портал Azure hello & электронной почты (вам нужна подписка toobe tooAzure Site Recovery уведомления). Сначала отображается баннер на странице приветствия хранилище ресурсов.

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. Щелкните hello баннер tooget получения дополнительной информации об окончания срока действия сертификата hello.

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  Если вместо кнопки **Обновить сейчас** отображается кнопка **Обновить**, Это означает, что отсутствуют некоторые компоненты в вашей среде, которые еще не были обновленного too9.4.xxxx.x или более поздних версий.

## <a name="sizing-requirements-for-a-configuration-server"></a>Требования к размерам сервера конфигурации

| **ЦП** | **Память** | **Размер диска кэша** | **Частота изменения данных** | **Защищенные компьютеры** |
| --- | --- | --- | --- | --- |
| 8 виртуальных ЦП (2 сокета * 4 ядра с частотой 2,5 ГГц) |16 ГБ |300 ГБ |500 ГБ или менее |Репликация не более 100 компьютеров |
| 12 виртуальных ЦП (2 сокета * 6 ядер с частотой 2,5 ГГц) |18 ГБ |600 ГБ |500 ГБ too1 ТБ |Репликация от 100 до 150 компьютеров |
| 16 виртуальных ЦП (2 сокета * 8 ядер с частотой 2,5 ГГц) |32 ГБ |1 TБ |1 ТБ too2 ТБ |Репликация от 150 до 200 компьютеров |

  >[!TIP]
  Если планируется tooreplicate более 200 виртуальных машин вашей ежедневного обновления данных превышает 2 ТБ, рекомендуется дополнительных процессов toodeploy серверы баланс tooload hello трафик репликации. Дополнительные сведения о как серверы toodeploy процесса горизонтального масштабирования.


## <a name="common-issues"></a>Распространенные проблемы
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
