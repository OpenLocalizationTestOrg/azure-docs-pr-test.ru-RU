---
title: " Управление сервером обработки масштабирования в Azure Site Recovery | Документация Майкрософт"
description: "В этой статье описывается как tooset и управление ею сервер обработки горизонтального масштабирования в Azure Site Recovery."
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a>Управление сервером обработки масштабирования

Сервер обработки масштабирования выступает в качестве координатора для передачи данных между службами Site Recovery hello и локальной инфраструктуры. В этой статье описывается, как выполнить установку, настройку и администрирование серверов обработки масштабирования.

## <a name="prerequisites"></a>Предварительные требования
Hello ниже приведены hello рекомендуется оборудования, программного обеспечения и tooset требуется настройка сети сервер процесс масштабирования.

> [!NOTE]
> [Планирование мощности](site-recovery-capacity-planner.md) является важным этапом tooensure развертывание сервера обработки масштабирования с конфигурацией hello, наборы требований нагрузки. Дополнительные сведения см. в разделе с [требованиями к масштабированию для сервера обработки масштабирования](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a>Загрузка программного обеспечения сервера обработки масштабирования hello
1. Войдите в систему toohello Azure tooyour портал и обзор хранилище служб восстановления.
2. Обзор слишком**инфраструктура Site Recovery** > **серверы конфигурации** (в разделе For VMware и физических компьютеров).
3. Выберите toodrill сервера вашей конфигурации списка на странице сведений о конфигурации сервера hello.
4. Нажмите кнопку hello **+ сервера обработки** кнопки.
5. В hello **сервер обработки, добавьте** выберите **масштабное развертывание сервера обработки в локальной** параметр из hello **выберите место toodeploy сервера обработки** раскрывающийся список.

  ![Страница "Добавление серверов"](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. Нажмите кнопку hello **загрузки hello установка единой Microsoft Azure Site Recovery** ссылку toodownload hello последнюю версию установки сервера обработки hello горизонтального масштабирования.

  > [!WARNING]
  Hello версия сервера обработки масштабирования должна быть равна tooor меньше, чем версия сервера конфигурации hello в вашей среде. Совместимость версий tooensure простой способ — toouse hello же установщика бит, что вы недавно использовали tooinstall или обновить сервер конфигурации.

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a>Установка и регистрация сервера обработки масштабирования из графического пользовательского интерфейса
При наличии tooscale out развертывания за пределы 200 исходных компьютеров, или общее ежедневно обработка скорость более 2 ТБ, необходимо объем трафика hello toohandle серверы дополнительные процедуры.

Проверьте hello [размер рекомендации для внутренних серверов](#size-recommendations-for-the-process-server), а затем выполните эти инструкции tooset hello процесса сервера. После настройки сервера hello, переносе исходной машины toouse его.

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a>Установка и регистрация сервера обработки масштабирования с помощью командной строки

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a>Пример использования
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a>Аргументы командной строки установщика сервера обработки масштабирования
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a>Создание файла конфигурации параметров прокси-сервера
Параметр ProxySettingsFilePath принимает в качестве входных данных файл. Создание файла с использованием hello ниже форматирования и передайте его в качестве входного параметра ProxySettingsFilePath.
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a>Изменение параметров прокси-сервера для сервера обработки масштабирования
1. Войдите на сервер обработки масштабирования.
2. Откройте командную строку PowerShell с правами администратора.
3. Запустите следующую команду hello
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. После просмотра каталога toohello **%PROGRAMDATA%\ASR\Agent** и выполнения hello следующую команду
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a>Повторная регистрация сервера обработки масштабирования
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* Далее откройте командную строку с правами администратора.
* Обзор каталога toohello **%PROGRAMDATA%\ASR\Agent** и выполните команду hello

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a>Обновление сервера обработки масштабирования
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a>Прекращение использования сервера обработки масштабирования
1. Убедитесь в следующем:
  - Состояние подключения сервера конфигурации показано, как **подключен** в hello портал Azure
  - Сервера обработки — все еще может toocommunicate с сервера конфигурации hello.
2. Войдите в сервер обработки toohello в качестве администратора
3. Откройте "Панель управления > Программы > Удалить программы".
4. Удалите программы hello в последовательности hello, учитывая следующие:
  * серверы конфигурации и обработки Microsoft Azure Site Recovery;
  * зависимости сервера конфигурации Microsoft Azure Site Recovery;
  * агент служб восстановления Microsoft Azure.

Он может занять too15 вверх минут для удаления tooreflect hello сервера обработки в hello портал Azure.

  > [!NOTE]
  Если сервера обработки hello — не удается toocommunicate с hello конфигурации сервера (подключение на портале имеет состояние Disconnected), потребуется toofollow hello следующие шаги toopurge его из hello сервера конфигурации.

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a>Отмена регистрации отключенного сервера обработки масштабирования на сервере конфигурации

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a>Требования к размеру для сервера обработки масштабирования

| **Дополнительный сервер обработки** | **Размер диска кэша** | **Частота изменения данных** | **Защищенные компьютеры** |
| --- | --- | --- | --- |
|4 виртуальных ЦП (2 сокета * 2 ядра с частотой 2,5 ГГц), 8 ГБ памяти |300 ГБ |250 ГБ или менее |Репликация до 85 компьютеров |
|8 виртуальных ЦП (2 сокета * 4 ядра с частотой 2,5 ГГц), 12 ГБ памяти |600 ГБ |250 ГБ too1 ТБ |Репликация от 85 до 150 компьютеров |
|12 виртуальных ЦП (2 сокета * 6 ядер с частотой 2,5 ГГц), 24 ГБ памяти |1 TБ |1 ТБ too2 ТБ |Репликация от 150 до 225 компьютеров |
