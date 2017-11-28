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
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="15625-103">Управление сервером обработки масштабирования</span><span class="sxs-lookup"><span data-stu-id="15625-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="15625-104">Сервер обработки масштабирования выступает в качестве координатора для передачи данных между службами Site Recovery hello и локальной инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="15625-104">Scale-out Process Server acts as a coordinator for data transfer between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="15625-105">В этой статье описывается, как выполнить установку, настройку и администрирование серверов обработки масштабирования.</span><span class="sxs-lookup"><span data-stu-id="15625-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15625-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="15625-106">Prerequisites</span></span>
<span data-ttu-id="15625-107">Hello ниже приведены hello рекомендуется оборудования, программного обеспечения и tooset требуется настройка сети сервер процесс масштабирования.</span><span class="sxs-lookup"><span data-stu-id="15625-107">hello following are hello recommended hardware, software, and network configuration required tooset up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="15625-108">[Планирование мощности](site-recovery-capacity-planner.md) является важным этапом tooensure развертывание сервера обработки масштабирования с конфигурацией hello, наборы требований нагрузки.</span><span class="sxs-lookup"><span data-stu-id="15625-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="15625-109">Дополнительные сведения см. в разделе с [требованиями к масштабированию для сервера обработки масштабирования](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="15625-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a><span data-ttu-id="15625-110">Загрузка программного обеспечения сервера обработки масштабирования hello</span><span class="sxs-lookup"><span data-stu-id="15625-110">Downloading hello Scale-out Process Server software</span></span>
1. <span data-ttu-id="15625-111">Войдите в систему toohello Azure tooyour портал и обзор хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="15625-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="15625-112">Обзор слишком**инфраструктура Site Recovery** > **серверы конфигурации** (в разделе For VMware и физических компьютеров).</span><span class="sxs-lookup"><span data-stu-id="15625-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="15625-113">Выберите toodrill сервера вашей конфигурации списка на странице сведений о конфигурации сервера hello.</span><span class="sxs-lookup"><span data-stu-id="15625-113">Select your configuration server toodrill down into hello configuration server's details page.</span></span>
4. <span data-ttu-id="15625-114">Нажмите кнопку hello **+ сервера обработки** кнопки.</span><span class="sxs-lookup"><span data-stu-id="15625-114">Click hello **+ Process Server** button.</span></span>
5. <span data-ttu-id="15625-115">В hello **сервер обработки, добавьте** выберите **масштабное развертывание сервера обработки в локальной** параметр из hello **выберите место toodeploy сервера обработки** раскрывающийся список.</span><span class="sxs-lookup"><span data-stu-id="15625-115">In hello **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from hello **Choose where you want toodeploy your process server** drop-down.</span></span>

  ![Страница "Добавление серверов"](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="15625-117">Нажмите кнопку hello **загрузки hello установка единой Microsoft Azure Site Recovery** ссылку toodownload hello последнюю версию установки сервера обработки hello горизонтального масштабирования.</span><span class="sxs-lookup"><span data-stu-id="15625-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="15625-118">Hello версия сервера обработки масштабирования должна быть равна tooor меньше, чем версия сервера конфигурации hello в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="15625-118">hello version of your Scale-out Process Server should be equal tooor lesser than hello Configuration Server version running in your environment.</span></span> <span data-ttu-id="15625-119">Совместимость версий tooensure простой способ — toouse hello же установщика бит, что вы недавно использовали tooinstall или обновить сервер конфигурации.</span><span class="sxs-lookup"><span data-stu-id="15625-119">A simple way tooensure version compatibility is toouse hello same installer bits that you recently used tooinstall/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="15625-120">Установка и регистрация сервера обработки масштабирования из графического пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="15625-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="15625-121">При наличии tooscale out развертывания за пределы 200 исходных компьютеров, или общее ежедневно обработка скорость более 2 ТБ, необходимо объем трафика hello toohandle серверы дополнительные процедуры.</span><span class="sxs-lookup"><span data-stu-id="15625-121">If you have tooscale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers toohandle hello traffic volume.</span></span>

<span data-ttu-id="15625-122">Проверьте hello [размер рекомендации для внутренних серверов](#size-recommendations-for-the-process-server), а затем выполните эти инструкции tooset hello процесса сервера.</span><span class="sxs-lookup"><span data-stu-id="15625-122">Check hello [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions tooset up hello process server.</span></span> <span data-ttu-id="15625-123">После настройки сервера hello, переносе исходной машины toouse его.</span><span class="sxs-lookup"><span data-stu-id="15625-123">After setting up hello server, you migrate source machines toouse it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="15625-124">Установка и регистрация сервера обработки масштабирования с помощью командной строки</span><span class="sxs-lookup"><span data-stu-id="15625-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="15625-125">Пример использования</span><span class="sxs-lookup"><span data-stu-id="15625-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="15625-126">Аргументы командной строки установщика сервера обработки масштабирования</span><span class="sxs-lookup"><span data-stu-id="15625-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="15625-127">Создание файла конфигурации параметров прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="15625-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="15625-128">Параметр ProxySettingsFilePath принимает в качестве входных данных файл.</span><span class="sxs-lookup"><span data-stu-id="15625-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="15625-129">Создание файла с использованием hello ниже форматирования и передайте его в качестве входного параметра ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="15625-129">Create file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="15625-130">Изменение параметров прокси-сервера для сервера обработки масштабирования</span><span class="sxs-lookup"><span data-stu-id="15625-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="15625-131">Войдите на сервер обработки масштабирования.</span><span class="sxs-lookup"><span data-stu-id="15625-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="15625-132">Откройте командную строку PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="15625-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="15625-133">Запустите следующую команду hello</span><span class="sxs-lookup"><span data-stu-id="15625-133">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="15625-134">После просмотра каталога toohello **%PROGRAMDATA%\ASR\Agent** и выполнения hello следующую команду</span><span class="sxs-lookup"><span data-stu-id="15625-134">Next browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="15625-135">Повторная регистрация сервера обработки масштабирования</span><span class="sxs-lookup"><span data-stu-id="15625-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="15625-136">Далее откройте командную строку с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="15625-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="15625-137">Обзор каталога toohello **%PROGRAMDATA%\ASR\Agent** и выполните команду hello</span><span class="sxs-lookup"><span data-stu-id="15625-137">Browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="15625-138">Обновление сервера обработки масштабирования</span><span class="sxs-lookup"><span data-stu-id="15625-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="15625-139">Прекращение использования сервера обработки масштабирования</span><span class="sxs-lookup"><span data-stu-id="15625-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="15625-140">Убедитесь в следующем:</span><span class="sxs-lookup"><span data-stu-id="15625-140">Ensure that:</span></span>
  - <span data-ttu-id="15625-141">Состояние подключения сервера конфигурации показано, как **подключен** в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="15625-141">Configuration Server's connection state shows as **Connected** in hello Azure portal</span></span>
  - <span data-ttu-id="15625-142">Сервера обработки — все еще может toocommunicate с сервера конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="15625-142">Process Server's is still able toocommunicate with hello Configuration server.</span></span>
2. <span data-ttu-id="15625-143">Войдите в сервер обработки toohello в качестве администратора</span><span class="sxs-lookup"><span data-stu-id="15625-143">Log in toohello process server as an administrator</span></span>
3. <span data-ttu-id="15625-144">Откройте "Панель управления > Программы > Удалить программы".</span><span class="sxs-lookup"><span data-stu-id="15625-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="15625-145">Удалите программы hello в последовательности hello, учитывая следующие:</span><span class="sxs-lookup"><span data-stu-id="15625-145">Uninstall hello programs in hello sequence given following:</span></span>
  * <span data-ttu-id="15625-146">серверы конфигурации и обработки Microsoft Azure Site Recovery;</span><span class="sxs-lookup"><span data-stu-id="15625-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="15625-147">зависимости сервера конфигурации Microsoft Azure Site Recovery;</span><span class="sxs-lookup"><span data-stu-id="15625-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="15625-148">агент служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="15625-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="15625-149">Он может занять too15 вверх минут для удаления tooreflect hello сервера обработки в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="15625-149">It can take up-too15 minutes for hello Process Server deletion tooreflect in hello Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="15625-150">Если сервера обработки hello — не удается toocommunicate с hello конфигурации сервера (подключение на портале имеет состояние Disconnected), потребуется toofollow hello следующие шаги toopurge его из hello сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="15625-150">If hello Process server is unable toocommunicate with hello Configuration Server (Connection State in portal is Disconnected), then you need toofollow hello following steps toopurge it from hello Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="15625-151">Отмена регистрации отключенного сервера обработки масштабирования на сервере конфигурации</span><span class="sxs-lookup"><span data-stu-id="15625-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="15625-152">Требования к размеру для сервера обработки масштабирования</span><span class="sxs-lookup"><span data-stu-id="15625-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="15625-153">**Дополнительный сервер обработки**</span><span class="sxs-lookup"><span data-stu-id="15625-153">**Additional process server**</span></span> | <span data-ttu-id="15625-154">**Размер диска кэша**</span><span class="sxs-lookup"><span data-stu-id="15625-154">**Cache disk size**</span></span> | <span data-ttu-id="15625-155">**Частота изменения данных**</span><span class="sxs-lookup"><span data-stu-id="15625-155">**Data change rate**</span></span> | <span data-ttu-id="15625-156">**Защищенные компьютеры**</span><span class="sxs-lookup"><span data-stu-id="15625-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="15625-157">4 виртуальных ЦП (2 сокета * 2 ядра с частотой 2,5 ГГц), 8 ГБ памяти</span><span class="sxs-lookup"><span data-stu-id="15625-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="15625-158">300 ГБ</span><span class="sxs-lookup"><span data-stu-id="15625-158">300 GB</span></span> |<span data-ttu-id="15625-159">250 ГБ или менее</span><span class="sxs-lookup"><span data-stu-id="15625-159">250 GB or less</span></span> |<span data-ttu-id="15625-160">Репликация до 85 компьютеров</span><span class="sxs-lookup"><span data-stu-id="15625-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="15625-161">8 виртуальных ЦП (2 сокета * 4 ядра с частотой 2,5 ГГц), 12 ГБ памяти</span><span class="sxs-lookup"><span data-stu-id="15625-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="15625-162">600 ГБ</span><span class="sxs-lookup"><span data-stu-id="15625-162">600 GB</span></span> |<span data-ttu-id="15625-163">250 ГБ too1 ТБ</span><span class="sxs-lookup"><span data-stu-id="15625-163">250 GB too1 TB</span></span> |<span data-ttu-id="15625-164">Репликация от 85 до 150 компьютеров</span><span class="sxs-lookup"><span data-stu-id="15625-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="15625-165">12 виртуальных ЦП (2 сокета * 6 ядер с частотой 2,5 ГГц), 24 ГБ памяти</span><span class="sxs-lookup"><span data-stu-id="15625-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="15625-166">1 TБ</span><span class="sxs-lookup"><span data-stu-id="15625-166">1 TB</span></span> |<span data-ttu-id="15625-167">1 ТБ too2 ТБ</span><span class="sxs-lookup"><span data-stu-id="15625-167">1 TB too2 TB</span></span> |<span data-ttu-id="15625-168">Репликация от 150 до 225 компьютеров</span><span class="sxs-lookup"><span data-stu-id="15625-168">Replicate between 150-225 machines.</span></span> |
