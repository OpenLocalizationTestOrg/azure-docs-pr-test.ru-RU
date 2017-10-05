---
title: " Управление сервером обработки масштабирования в Azure Site Recovery | Документация Майкрософт"
description: "В этой статье описывается настройка сервера обработки масштабирования в Azure Site Recovery и управление им."
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
ms.openlocfilehash: e5c01de19917235c34c035415df86291b9152bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="ed3d6-103">Управление сервером обработки масштабирования</span><span class="sxs-lookup"><span data-stu-id="ed3d6-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="ed3d6-104">Сервер обработки масштабирования выполняет роль координатора передачи данных между службами Site Recovery и локальной инфраструктурой.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-104">Scale-out Process Server acts as a coordinator for data transfer between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="ed3d6-105">В этой статье описывается, как выполнить установку, настройку и администрирование серверов обработки масштабирования.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed3d6-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ed3d6-106">Prerequisites</span></span>
<span data-ttu-id="ed3d6-107">Ниже перечислены рекомендуемые требования к оборудованию, программному обеспечению и сети для установки сервера обработки масштабирования.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-107">The following are the recommended hardware, software, and network configuration required to set up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="ed3d6-108">[Планирование мощности](site-recovery-capacity-planner.md) — это важный шаг для развертывания сервера обработки масштабирования, соответствующего требованиям нагрузки.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="ed3d6-109">Дополнительные сведения см. в разделе с [требованиями к масштабированию для сервера обработки масштабирования](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="ed3d6-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-scale-out-process-server-software"></a><span data-ttu-id="ed3d6-110">Скачивание программного обеспечения сервера обработки масштабирования</span><span class="sxs-lookup"><span data-stu-id="ed3d6-110">Downloading the Scale-out Process Server software</span></span>
1. <span data-ttu-id="ed3d6-111">Войдите на портал Azure и перейдите в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="ed3d6-112">Откройте **Инфраструктура Site Recovery** > **Серверы конфигурации** (в разделе VMware и физических компьютеров).</span><span class="sxs-lookup"><span data-stu-id="ed3d6-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="ed3d6-113">Выберите сервер конфигурации, чтобы перейти на страницу подробных сведений о нем.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-113">Select your configuration server to drill down into the configuration server's details page.</span></span>
4. <span data-ttu-id="ed3d6-114">Нажмите кнопку **+ Сервер обработки**.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-114">Click the **+ Process Server** button.</span></span>
5. <span data-ttu-id="ed3d6-115">На странице **Добавление сервера обработки** в раскрывающемся списке **Укажите, где следует развернуть сервер обработки** выберите **Локальное развертывание сервера обработки масштабирования**.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-115">In the **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from the **Choose where you want to deploy your process server** drop-down.</span></span>

  ![Страница "Добавление серверов"](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="ed3d6-117">Щелкните ссылку **Download the Microsoft Azure Site Recovery Unified Setup** (Скачать единый файл установки Microsoft Azure Site Recovery), чтобы скачать последнюю версию файла установки сервера обработки масштабирования.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="ed3d6-118">Версия сервера обработки масштабирования должна соответствовать версии сервера конфигурации, работающего в среде, или быть меньше ее.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-118">The version of your Scale-out Process Server should be equal to or lesser than the Configuration Server version running in your environment.</span></span> <span data-ttu-id="ed3d6-119">Простой способ обеспечить совместимость версий — использовать те же средства установки, которые недавно использовались для установки и обновления сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-119">A simple way to ensure version compatibility is to use the same installer bits that you recently used to install/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="ed3d6-120">Установка и регистрация сервера обработки масштабирования из графического пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="ed3d6-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="ed3d6-121">Если вы увеличите развертывание так, что количество компьютеров-источников превысит 200 или объем ежедневно изменяемых данных превысит 2 ТБ, для обработки такой нагрузки потребуются дополнительные серверы обработки.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-121">If you have to scale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers to handle the traffic volume.</span></span>

<span data-ttu-id="ed3d6-122">Ознакомьтесь с [рекомендациями по выбору размера серверов обработки](#size-recommendations-for-the-process-server) и выполните приведенные ниже инструкции по настройке сервера обработки.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-122">Check the [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions to set up the process server.</span></span> <span data-ttu-id="ed3d6-123">После настройки сервера необходимо перевести исходные компьютеры на его использование.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-123">After setting up the server, you migrate source machines to use it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="ed3d6-124">Установка и регистрация сервера обработки масштабирования с помощью командной строки</span><span class="sxs-lookup"><span data-stu-id="ed3d6-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="ed3d6-125">Пример использования</span><span class="sxs-lookup"><span data-stu-id="ed3d6-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="ed3d6-126">Аргументы командной строки установщика сервера обработки масштабирования</span><span class="sxs-lookup"><span data-stu-id="ed3d6-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="ed3d6-127">Создание файла конфигурации параметров прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="ed3d6-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="ed3d6-128">Параметр ProxySettingsFilePath принимает в качестве входных данных файл.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="ed3d6-129">Создайте файл, используя следующий формат, и передайте его в качестве входных данных для параметра ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-129">Create file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="ed3d6-130">Изменение параметров прокси-сервера для сервера обработки масштабирования</span><span class="sxs-lookup"><span data-stu-id="ed3d6-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="ed3d6-131">Войдите на сервер обработки масштабирования.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="ed3d6-132">Откройте командную строку PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="ed3d6-133">Выполните следующую команду</span><span class="sxs-lookup"><span data-stu-id="ed3d6-133">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="ed3d6-134">Затем перейдите в каталог **%PROGRAMDATA%\ASR\Agent** и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ed3d6-134">Next browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="ed3d6-135">Повторная регистрация сервера обработки масштабирования</span><span class="sxs-lookup"><span data-stu-id="ed3d6-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="ed3d6-136">Далее откройте командную строку с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="ed3d6-137">Перейдите в каталог **%PROGRAMDATA%\ASR\Agent** и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ed3d6-137">Browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="ed3d6-138">Обновление сервера обработки масштабирования</span><span class="sxs-lookup"><span data-stu-id="ed3d6-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="ed3d6-139">Прекращение использования сервера обработки масштабирования</span><span class="sxs-lookup"><span data-stu-id="ed3d6-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="ed3d6-140">Убедитесь в следующем:</span><span class="sxs-lookup"><span data-stu-id="ed3d6-140">Ensure that:</span></span>
  - <span data-ttu-id="ed3d6-141">на портале Azure показано, что подключение сервера конфигурации установлено (состояние **Подключено**);</span><span class="sxs-lookup"><span data-stu-id="ed3d6-141">Configuration Server's connection state shows as **Connected** in the Azure portal</span></span>
  - <span data-ttu-id="ed3d6-142">сервер обработки по-прежнему может обмениваться данными с сервером конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-142">Process Server's is still able to communicate with the Configuration server.</span></span>
2. <span data-ttu-id="ed3d6-143">Войдите на сервер обработки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-143">Log in to the process server as an administrator</span></span>
3. <span data-ttu-id="ed3d6-144">Откройте "Панель управления > Программы > Удалить программы".</span><span class="sxs-lookup"><span data-stu-id="ed3d6-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="ed3d6-145">Удалите программы в следующей последовательности:</span><span class="sxs-lookup"><span data-stu-id="ed3d6-145">Uninstall the programs in the sequence given following:</span></span>
  * <span data-ttu-id="ed3d6-146">серверы конфигурации и обработки Microsoft Azure Site Recovery;</span><span class="sxs-lookup"><span data-stu-id="ed3d6-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="ed3d6-147">зависимости сервера конфигурации Microsoft Azure Site Recovery;</span><span class="sxs-lookup"><span data-stu-id="ed3d6-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="ed3d6-148">агент служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="ed3d6-149">Чтобы удаление сервера обработки отобразилось на портале Azure, может потребоваться около 15 минут.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-149">It can take up-to 15 minutes for the Process Server deletion to reflect in the Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="ed3d6-150">Если серверу обработки не удалось связаться с сервером конфигурации (на портале показано состояние подключения "Отключено"), необходимо выполнить следующие действия, чтобы удалить его с сервера конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ed3d6-150">If the Process server is unable to communicate with the Configuration Server (Connection State in portal is Disconnected), then you need to follow the following steps to purge it from the Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="ed3d6-151">Отмена регистрации отключенного сервера обработки масштабирования на сервере конфигурации</span><span class="sxs-lookup"><span data-stu-id="ed3d6-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="ed3d6-152">Требования к размеру для сервера обработки масштабирования</span><span class="sxs-lookup"><span data-stu-id="ed3d6-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="ed3d6-153">**Дополнительный сервер обработки**</span><span class="sxs-lookup"><span data-stu-id="ed3d6-153">**Additional process server**</span></span> | <span data-ttu-id="ed3d6-154">**Размер диска кэша**</span><span class="sxs-lookup"><span data-stu-id="ed3d6-154">**Cache disk size**</span></span> | <span data-ttu-id="ed3d6-155">**Частота изменения данных**</span><span class="sxs-lookup"><span data-stu-id="ed3d6-155">**Data change rate**</span></span> | <span data-ttu-id="ed3d6-156">**Защищенные компьютеры**</span><span class="sxs-lookup"><span data-stu-id="ed3d6-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="ed3d6-157">4 виртуальных ЦП (2 сокета * 2 ядра с частотой 2,5 ГГц), 8 ГБ памяти</span><span class="sxs-lookup"><span data-stu-id="ed3d6-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="ed3d6-158">300 ГБ</span><span class="sxs-lookup"><span data-stu-id="ed3d6-158">300 GB</span></span> |<span data-ttu-id="ed3d6-159">250 ГБ или менее</span><span class="sxs-lookup"><span data-stu-id="ed3d6-159">250 GB or less</span></span> |<span data-ttu-id="ed3d6-160">Репликация до 85 компьютеров</span><span class="sxs-lookup"><span data-stu-id="ed3d6-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="ed3d6-161">8 виртуальных ЦП (2 сокета * 4 ядра с частотой 2,5 ГГц), 12 ГБ памяти</span><span class="sxs-lookup"><span data-stu-id="ed3d6-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="ed3d6-162">600 ГБ</span><span class="sxs-lookup"><span data-stu-id="ed3d6-162">600 GB</span></span> |<span data-ttu-id="ed3d6-163">От 250 ГБ до 1 ТБ</span><span class="sxs-lookup"><span data-stu-id="ed3d6-163">250 GB to 1 TB</span></span> |<span data-ttu-id="ed3d6-164">Репликация от 85 до 150 компьютеров</span><span class="sxs-lookup"><span data-stu-id="ed3d6-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="ed3d6-165">12 виртуальных ЦП (2 сокета * 6 ядер с частотой 2,5 ГГц), 24 ГБ памяти</span><span class="sxs-lookup"><span data-stu-id="ed3d6-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="ed3d6-166">1 TБ</span><span class="sxs-lookup"><span data-stu-id="ed3d6-166">1 TB</span></span> |<span data-ttu-id="ed3d6-167">От 1 ТБ до 2 ТБ</span><span class="sxs-lookup"><span data-stu-id="ed3d6-167">1 TB to 2 TB</span></span> |<span data-ttu-id="ed3d6-168">Репликация от 150 до 225 компьютеров</span><span class="sxs-lookup"><span data-stu-id="ed3d6-168">Replicate between 150-225 machines.</span></span> |
