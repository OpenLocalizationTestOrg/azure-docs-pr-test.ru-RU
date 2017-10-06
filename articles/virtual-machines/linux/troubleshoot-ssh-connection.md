---
title: "SSH-подключения aaaTroubleshoot выдает tooan виртуальной Машины Azure | Документы Microsoft"
description: "Как tootroubleshoot проблемы, например, «сбоем подключения SSH» или «SSH-подключение отклонено» для виртуальной Машины Azure под управлением Linux."
keywords: "отклонение SSH-подключения, ошибка SSH, Azure SSH, ошибка SSH-подключения"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="230e3-104">Устранение неполадок подключения SSH tooan виртуальной Машине Linux Azure, происходит сбой, ошибки, или отклонен</span><span class="sxs-lookup"><span data-stu-id="230e3-104">Troubleshoot SSH connections tooan Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="230e3-105">Существует несколько причин, возникнут ошибки Secure Shell (SSH), ошибками соединения SSH, или SSH отклонено, при попытке tooconnect tooa Linux виртуальной машины (VM).</span><span class="sxs-lookup"><span data-stu-id="230e3-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try tooconnect tooa Linux virtual machine (VM).</span></span> <span data-ttu-id="230e3-106">Эта статья поможет вам найти и правильный hello проблем.</span><span class="sxs-lookup"><span data-stu-id="230e3-106">This article helps you find and correct hello problems.</span></span> <span data-ttu-id="230e3-107">Можно использовать для Linux tootroubleshoot hello портал Azure, Azure CLI или расширение доступа виртуальной Машины и решения проблем с подключением.</span><span class="sxs-lookup"><span data-stu-id="230e3-107">You can use hello Azure portal, Azure CLI, or VM Access Extension for Linux tootroubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="230e3-108">Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello форумы MSDN Azure и переполнения стека](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="230e3-108">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="230e3-109">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="230e3-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="230e3-110">Go toohello [сайт поддержки Azure](http://azure.microsoft.com/support/options/) и выберите **получение поддержки**.</span><span class="sxs-lookup"><span data-stu-id="230e3-110">Go toohello [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="230e3-111">Дополнительные сведения об использовании Azure поддерживает чтение hello [поддержки Microsoft Azure часто задаваемые вопросы о](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="230e3-111">For information about using Azure Support, read hello [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="230e3-112">Действия по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="230e3-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="230e3-113">После каждого действия по устранению неполадок выполните повторное подключение toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="230e3-113">After each troubleshooting step, try reconnecting toohello VM.</span></span>

1. <span data-ttu-id="230e3-114">Сброс конфигурации SSH hello.</span><span class="sxs-lookup"><span data-stu-id="230e3-114">Reset hello SSH configuration.</span></span>
2. <span data-ttu-id="230e3-115">Сбросьте учетные данные пользователя hello hello.</span><span class="sxs-lookup"><span data-stu-id="230e3-115">Reset hello credentials for hello user.</span></span>
3. <span data-ttu-id="230e3-116">Проверьте hello [сетевой группы безопасности](../../virtual-network/virtual-networks-nsg.md) правила разрешают трафик SSH.</span><span class="sxs-lookup"><span data-stu-id="230e3-116">Verify hello [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="230e3-117">Убедитесь, что правило группы безопасности сети существует toopermit SSH трафика (по умолчанию, TCP-порт 22).</span><span class="sxs-lookup"><span data-stu-id="230e3-117">Ensure that a Network Security Group rule exists toopermit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="230e3-118">Нельзя использовать перенаправление и сопоставление портов, не используя Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="230e3-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="230e3-119">Проверьте hello [исправности ресурсов для виртуальной Машины](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="230e3-119">Check hello [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="230e3-120">Убедитесь, что hello ВМ отчеты как состоянию работоспособности.</span><span class="sxs-lookup"><span data-stu-id="230e3-120">Ensure that hello VM reports as being healthy.</span></span>
   * <span data-ttu-id="230e3-121">Если включена Диагностика загрузки, убедитесь, что hello виртуальной Машины, не предоставляет загрузки ошибки в журналах hello.</span><span class="sxs-lookup"><span data-stu-id="230e3-121">If you have boot diagnostics enabled, verify hello VM is not reporting boot errors in hello logs.</span></span>
5. <span data-ttu-id="230e3-122">Перезапустите hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="230e3-122">Restart hello VM.</span></span>
6. <span data-ttu-id="230e3-123">Повторное развертывание hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="230e3-123">Redeploy hello VM.</span></span>

<span data-ttu-id="230e3-124">Читайте статью дальше, если вам нужны более подробные инструкции или пояснения об исправлении неполадок.</span><span class="sxs-lookup"><span data-stu-id="230e3-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a><span data-ttu-id="230e3-125">Доступные методы tootroubleshoot SSH с подключением</span><span class="sxs-lookup"><span data-stu-id="230e3-125">Available methods tootroubleshoot SSH connection issues</span></span>
<span data-ttu-id="230e3-126">Можно сбросить учетные данные или с помощью одного из следующих методов hello конфигурации SSH:</span><span class="sxs-lookup"><span data-stu-id="230e3-126">You can reset credentials or SSH configuration using one of hello following methods:</span></span>

* <span data-ttu-id="230e3-127">[Портал Azure](#use-the-azure-portal) - нормально, если вам требуется tooquickly Сброс конфигурации SSH hello или ключ SSH, и не hello установлены средства Azure.</span><span class="sxs-lookup"><span data-stu-id="230e3-127">[Azure portal](#use-the-azure-portal) - great if you need tooquickly reset hello SSH configuration or SSH key and you don't have hello Azure tools installed.</span></span>
* <span data-ttu-id="230e3-128">[Azure CLI 2.0](#use-the-azure-cli-20) — Если вы уже находитесь в командной строке hello быстро Сброс конфигурации SSH hello или учетные данные.</span><span class="sxs-lookup"><span data-stu-id="230e3-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on hello command line, quickly reset hello SSH configuration or credentials.</span></span> <span data-ttu-id="230e3-129">Можно также использовать hello [Azure CLI 1.0](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="230e3-129">You can also use hello [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="230e3-130">[Azure расширение VMAccessForLinux](#use-the-vmaccess-extension) — создайте и повторно использовать json определения файлов tooreset hello SSH конфигурации или учетные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="230e3-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files tooreset hello SSH configuration or user credentials.</span></span>

<span data-ttu-id="230e3-131">После каждого действия по устранению неполадок повторите попытку подключения tooyour виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="230e3-131">After each troubleshooting step, try connecting tooyour VM again.</span></span> <span data-ttu-id="230e3-132">Если вы по-прежнему не удается подключиться, попробуйте hello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="230e3-132">If you still cannot connect, try hello next step.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="230e3-133">Использовать hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="230e3-133">Use hello Azure portal</span></span>
<span data-ttu-id="230e3-134">Hello портал Azure предоставляет быстрый способ tooreset hello SSH конфигурации или учетные данные пользователя без установки средства на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="230e3-134">hello Azure portal provides a quick way tooreset hello SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="230e3-135">Выберите виртуальную Машину в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="230e3-135">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="230e3-136">Прокрутите вниз toohello **поддержки + Устранение неполадок** , выберите **сброс пароля** как hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="230e3-136">Scroll down toohello **Support + Troubleshooting** section and select **Reset password** as in hello following example:</span></span>

![Сброс конфигурации SSH или учетные данные в hello портал Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a><span data-ttu-id="230e3-138">Сброс конфигурации SSH hello</span><span class="sxs-lookup"><span data-stu-id="230e3-138">Reset hello SSH configuration</span></span>
<span data-ttu-id="230e3-139">В качестве первого шага, выберите `Reset configuration only` из hello **режим** раскрывающееся меню как hello предшествующий экрана, а затем нажмите кнопку hello **Сброс** кнопки.</span><span class="sxs-lookup"><span data-stu-id="230e3-139">As a first step, select `Reset configuration only` from hello **Mode** drop-down menu as in hello preceding screenshot, then click hello **Reset** button.</span></span> <span data-ttu-id="230e3-140">После завершения этого действия повторите tooaccess ВМ.</span><span class="sxs-lookup"><span data-stu-id="230e3-140">Once this action has completed, try tooaccess your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="230e3-141">Сброс учетных данных SSH пользователя</span><span class="sxs-lookup"><span data-stu-id="230e3-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="230e3-142">Выберите tooreset hello учетные данные существующего пользователя, либо `Reset SSH public key` или `Reset password` из hello **режим** раскрывающееся меню, как предшествующий экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="230e3-142">tooreset hello credentials of an existing user, select either `Reset SSH public key` or `Reset password` from hello **Mode** drop-down menu as in hello preceding screenshot.</span></span> <span data-ttu-id="230e3-143">Укажите имя пользователя hello и SSH-ключ или новый пароль, а затем щелкните hello **Сброс** кнопки.</span><span class="sxs-lookup"><span data-stu-id="230e3-143">Specify hello username and an SSH key or new password, then click hello **Reset** button.</span></span>

<span data-ttu-id="230e3-144">Можно также создать пользователя с правами sudo на hello виртуальной Машины из этого меню.</span><span class="sxs-lookup"><span data-stu-id="230e3-144">You can also create a user with sudo privileges on hello VM from this menu.</span></span> <span data-ttu-id="230e3-145">Введите новое имя пользователя и соответствующий пароль или ключ SSH и нажмите кнопку hello **Сброс** кнопки.</span><span class="sxs-lookup"><span data-stu-id="230e3-145">Enter a new username and associated password or SSH key, and then click hello **Reset** button.</span></span>

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="230e3-146">Использовать hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="230e3-146">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="230e3-147">Если это еще не сделано, установите hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="230e3-147">If you haven't already, install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="230e3-148">Если создан и загружен пользовательского образа диска Linux, убедитесь, что hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) версии 2.0.5 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="230e3-148">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="230e3-149">В виртуальных машинах, созданных с помощью образов из коллекции, это расширение для доступа уже установлено и настроено.</span><span class="sxs-lookup"><span data-stu-id="230e3-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="230e3-150">Сбросьте конфигурацию SSH.</span><span class="sxs-lookup"><span data-stu-id="230e3-150">Reset SSH configuration</span></span>
<span data-ttu-id="230e3-151">Изначально можно toodefault значения try Сброс hello SSH конфигурации и перезагрузку сервера SSH hello на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="230e3-151">You can initially try resetting hello SSH configuration toodefault values and rebooting hello SSH server on hello VM.</span></span> <span data-ttu-id="230e3-152">Обратите внимание, что это не изменяет hello имя учетной записи пользователя, пароль или ключей SSH.</span><span class="sxs-lookup"><span data-stu-id="230e3-152">Note that this does not change hello user account name, password, or SSH keys.</span></span>
<span data-ttu-id="230e3-153">Hello следующий пример использует [сброса пользователей виртуальной машины az-ssh](/cli/azure/vm/user#reset-ssh) tooreset конфигурации SSH hello на Виртуальную машину с именем hello `myVM` в `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="230e3-153">hello following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH configuration on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="230e3-154">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="230e3-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="230e3-155">Сброс учетных данных SSH пользователя</span><span class="sxs-lookup"><span data-stu-id="230e3-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="230e3-156">Hello следующий пример использует [обновление пользователя виртуальной машины az](/cli/azure/vm/user#update) tooreset hello учетные данные для `myUsername` toohello значение, указанное в `myPassword`, на Виртуальную машину с именем hello `myVM` в `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="230e3-156">hello following example uses [az vm user update](/cli/azure/vm/user#update) tooreset hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="230e3-157">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="230e3-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="230e3-158">Если используется проверка подлинности ключа SSH, можно сбросить hello SSH-ключ для данного пользователя.</span><span class="sxs-lookup"><span data-stu-id="230e3-158">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="230e3-159">Hello следующий пример использует **az ВМ доступа пользователей для linux набор** tooupdate hello SSH ключа, хранимого в `~/.ssh/id_rsa.pub` для hello пользователя с именем `myUsername`, на Виртуальную машину с именем hello `myVM` в `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="230e3-159">hello following example uses **az vm access set-linux-user** tooupdate hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="230e3-160">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="230e3-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a><span data-ttu-id="230e3-161">Использовать расширение VMAccess hello</span><span class="sxs-lookup"><span data-stu-id="230e3-161">Use hello VMAccess extension</span></span>
<span data-ttu-id="230e3-162">в файле json, определяющий действия toocarry out считывает Hello расширения Access ВМ для Linux. При этом сбрасывается SSHD и ключ SSH или добавляется пользователь.</span><span class="sxs-lookup"><span data-stu-id="230e3-162">hello VM Access Extension for Linux reads in a json file that defines actions toocarry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="230e3-163">По-прежнему использовать hello Azure CLI toocall hello расширения VMAccess, но можно повторно использовать файлы json hello в нескольких виртуальных машинах при необходимости.</span><span class="sxs-lookup"><span data-stu-id="230e3-163">You still use hello Azure CLI toocall hello VMAccess extension, but you can reuse hello json files across multiple VMs if desired.</span></span> <span data-ttu-id="230e3-164">Такой подход позволяет toocreate хранилищем файлов json, которые можно вызывать для заданной сценариев.</span><span class="sxs-lookup"><span data-stu-id="230e3-164">This approach allows you toocreate a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="230e3-165">Сброс SSHD</span><span class="sxs-lookup"><span data-stu-id="230e3-165">Reset SSHD</span></span>
<span data-ttu-id="230e3-166">Создайте файл с именем `settings.json` с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="230e3-166">Create a file named `settings.json` with hello following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="230e3-167">С помощью hello Azure CLI, затем вызовите hello `VMAccessForLinux` tooreset расширения SSHD подключение, указав json-файла.</span><span class="sxs-lookup"><span data-stu-id="230e3-167">Using hello Azure CLI, you then call hello `VMAccessForLinux` extension tooreset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="230e3-168">Hello следующий пример использует [набор расширения ВМ az](/cli/azure/vm/extension#set) tooreset SSHD на Виртуальную машину с именем hello `myVM` в `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="230e3-168">hello following example uses [az vm extension set](/cli/azure/vm/extension#set) tooreset SSHD on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="230e3-169">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="230e3-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="230e3-170">Сброс учетных данных SSH пользователя</span><span class="sxs-lookup"><span data-stu-id="230e3-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="230e3-171">Если SSHD toofunction правильно, можно сбросить учетные данные пользователя жабль hello.</span><span class="sxs-lookup"><span data-stu-id="230e3-171">If SSHD appears toofunction correctly, you can reset hello credentials for a giver user.</span></span> <span data-ttu-id="230e3-172">tooreset hello пароля для пользователя, создайте файл с именем `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="230e3-172">tooreset hello password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="230e3-173">Hello следующий пример сбрасывает hello учетные данные для `myUsername` toohello значение, указанное в `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="230e3-173">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`.</span></span> <span data-ttu-id="230e3-174">Введите следующие строки в hello вашей `settings.json` файл, используя свои собственные значения:</span><span class="sxs-lookup"><span data-stu-id="230e3-174">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="230e3-175">Или tooreset Здравствуйте SSH-ключ для пользователя, сначала создайте файл с именем `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="230e3-175">Or tooreset hello SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="230e3-176">Hello следующий пример сбрасывает hello учетные данные для `myUsername` toohello значение, указанное в `myPassword`, на Виртуальную машину с именем hello `myVM` в `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="230e3-176">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="230e3-177">Введите следующие строки в hello вашей `settings.json` файл, используя свои собственные значения:</span><span class="sxs-lookup"><span data-stu-id="230e3-177">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="230e3-178">После создания json-файла используйте hello Azure CLI toocall hello `VMAccessForLinux` расширения tooreset учетные данные пользователя SSH, указав json-файла.</span><span class="sxs-lookup"><span data-stu-id="230e3-178">After creating your json file, use hello Azure CLI toocall hello `VMAccessForLinux` extension tooreset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="230e3-179">Hello следующий пример сбрасывает учетных данных на Виртуальную машину с именем hello `myVM` в `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="230e3-179">hello following example resets credentials on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="230e3-180">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="230e3-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="230e3-181">Использовать hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="230e3-181">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="230e3-182">Если это еще не сделано, [Установка hello Azure CLI 1.0 и подключение tooyour подписки Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="230e3-182">If you haven't already, [install hello Azure CLI 1.0 and connect tooyour Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="230e3-183">Убедитесь, что используется режим Resource Manager следующим образом:</span><span class="sxs-lookup"><span data-stu-id="230e3-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="230e3-184">Если создан и загружен пользовательского образа диска Linux, убедитесь, что hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) версии 2.0.5 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="230e3-184">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="230e3-185">В виртуальных машинах, созданных с помощью образов из коллекции, это расширение для доступа уже установлено и настроено.</span><span class="sxs-lookup"><span data-stu-id="230e3-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="230e3-186">Сбросьте конфигурацию SSH.</span><span class="sxs-lookup"><span data-stu-id="230e3-186">Reset SSH configuration</span></span>
<span data-ttu-id="230e3-187">неправильно сама конфигурация SSHD Hello, или произошла ошибка службы hello.</span><span class="sxs-lookup"><span data-stu-id="230e3-187">hello SSHD configuration itself may be misconfigured or hello service encountered an error.</span></span> <span data-ttu-id="230e3-188">Вы можете сбросить SSHD toomake убедиться, что конфигурация SSH hello сам является допустимой.</span><span class="sxs-lookup"><span data-stu-id="230e3-188">You can reset SSHD toomake sure hello SSH configuration itself is valid.</span></span> <span data-ttu-id="230e3-189">Сброс SSHD должно быть hello устранения этой проблемы сначала выполнить.</span><span class="sxs-lookup"><span data-stu-id="230e3-189">Resetting SSHD should be hello first troubleshooting step you take.</span></span>

<span data-ttu-id="230e3-190">Hello следующий пример сбрасывает SSHD на виртуальной Машине с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="230e3-190">hello following example resets SSHD on a VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="230e3-191">Используйте собственные имена для виртуальной машины и группы ресурсов следующим образом:</span><span class="sxs-lookup"><span data-stu-id="230e3-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="230e3-192">Сброс учетных данных SSH пользователя</span><span class="sxs-lookup"><span data-stu-id="230e3-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="230e3-193">Если SSHD toofunction правильно, вы можете сбросить пароль hello жабль пользователя.</span><span class="sxs-lookup"><span data-stu-id="230e3-193">If SSHD appears toofunction correctly, you can reset hello password for a giver user.</span></span> <span data-ttu-id="230e3-194">Hello следующий пример сбрасывает hello учетные данные для `myUsername` toohello значение, указанное в `myPassword`, на Виртуальную машину с именем hello `myVM` в `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="230e3-194">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="230e3-195">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="230e3-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="230e3-196">Если используется проверка подлинности ключа SSH, можно сбросить hello SSH-ключ для данного пользователя.</span><span class="sxs-lookup"><span data-stu-id="230e3-196">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="230e3-197">Следующий пример обновляет Hello hello SSH-ключ, хранящийся в `~/.ssh/id_rsa.pub` для hello пользователя с именем `myUsername`, на Виртуальную машину с именем hello `myVM` в `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="230e3-197">hello following example updates hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="230e3-198">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="230e3-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="230e3-199">Перезапуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="230e3-199">Restart a VM</span></span>
<span data-ttu-id="230e3-200">Если вы сбросить hello SSH конфигурации и учетные данные пользователя, или произошла ошибка при этом, попробуйте перезапуска tooaddress ВМ hello основной проблемы вычислений.</span><span class="sxs-lookup"><span data-stu-id="230e3-200">If you have reset hello SSH configuration and user credentials, or encountered an error in doing so, you can try restarting hello VM tooaddress underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="230e3-201">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="230e3-201">Azure portal</span></span>
<span data-ttu-id="230e3-202">toorestart виртуальной Машины с помощью hello Azure портала, выберите hello вашей виртуальной Машины и нажмите кнопку **перезапустите** кнопки как hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="230e3-202">toorestart a VM using hello Azure portal, select your VM and click hello **Restart** button as in hello following example:</span></span>

![Перезапустите виртуальную Машину в hello портал Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="230e3-204">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="230e3-204">Azure CLI 1.0</span></span>
<span data-ttu-id="230e3-205">Следующий пример перезапускается Hello hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="230e3-205">hello following example restarts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="230e3-206">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="230e3-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="230e3-207">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="230e3-207">Azure CLI 2.0</span></span>
<span data-ttu-id="230e3-208">Hello следующий пример использует [перезапуска ВМ az](/cli/azure/vm#restart) toorestart hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="230e3-208">hello following example uses [az vm restart](/cli/azure/vm#restart) toorestart hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="230e3-209">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="230e3-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="230e3-210">Повторное развертывание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="230e3-210">Redeploy a VM</span></span>
<span data-ttu-id="230e3-211">Можно повторно развернуть узел tooanother ВМ в Azure, который может исправить проблемы с базовой сети.</span><span class="sxs-lookup"><span data-stu-id="230e3-211">You can redeploy a VM tooanother node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="230e3-212">Сведения о повторного развертывания виртуальной Машины см. в разделе [повторного развертывания виртуальной машины toonew узла Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="230e3-212">For information about redeploying a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="230e3-213">После завершения этой операции эфемерных диске данные будут потеряны и динамических IP-адресов, связанных с виртуальной машиной hello будет обновляться.</span><span class="sxs-lookup"><span data-stu-id="230e3-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="230e3-214">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="230e3-214">Azure portal</span></span>
<span data-ttu-id="230e3-215">tooredeploy виртуальной Машины с помощью hello Azure портала, выберите ВМ и прокрутите вниз toohello **поддержки + Устранение неполадок** раздела.</span><span class="sxs-lookup"><span data-stu-id="230e3-215">tooredeploy a VM using hello Azure portal, select your VM and scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="230e3-216">Нажмите кнопку hello **повторно развернуть** кнопки как hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="230e3-216">Click hello **Redeploy** button as in hello following example:</span></span>

![Повторное развертывание виртуальной Машины в hello портал Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="230e3-218">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="230e3-218">Azure CLI 1.0</span></span>
<span data-ttu-id="230e3-219">Следующий пример повторно развертывает Hello hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="230e3-219">hello following example redeploys hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="230e3-220">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="230e3-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="230e3-221">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="230e3-221">Azure CLI 2.0</span></span>
<span data-ttu-id="230e3-222">Следующий пример использования Hello [повторного развертывания виртуальной машины az](/cli/azure/vm#redeploy) tooredeploy hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="230e3-222">hello following example use [az vm redeploy](/cli/azure/vm#redeploy) tooredeploy hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="230e3-223">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="230e3-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a><span data-ttu-id="230e3-224">Виртуальные машины, созданные с помощью hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="230e3-224">VMs created by using hello Classic deployment model</span></span>
<span data-ttu-id="230e3-225">Повторите эти шаги tooresolve hello наиболее распространенные SSH сбоев подключения для виртуальных машин, которые были созданы с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="230e3-225">Try these steps tooresolve hello most common SSH connection failures for VMs that were created by using hello classic deployment model.</span></span> <span data-ttu-id="230e3-226">После выполнения каждого шага выполните повторное подключение toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="230e3-226">After each step, try reconnecting toohello VM.</span></span>

* <span data-ttu-id="230e3-227">Сбросьте удаленный доступ из hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="230e3-227">Reset remote access from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="230e3-228">На hello портал Azure, выберите виртуальную Машину и щелкните hello **удаленный сброс...**  кнопки.</span><span class="sxs-lookup"><span data-stu-id="230e3-228">On hello Azure portal, select your VM and click hello **Reset Remote...** button.</span></span>
* <span data-ttu-id="230e3-229">Перезапустите hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="230e3-229">Restart hello VM.</span></span> <span data-ttu-id="230e3-230">На hello [портал Azure](https://portal.azure.com), выберите виртуальную Машину и щелкните hello **перезапустите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="230e3-230">On hello [Azure portal](https://portal.azure.com), select your VM and click hello **Restart** button.</span></span>
    
* <span data-ttu-id="230e3-231">Повторное развертывание hello ВМ tooa новый узел Azure.</span><span class="sxs-lookup"><span data-stu-id="230e3-231">Redeploy hello VM tooa new Azure node.</span></span> <span data-ttu-id="230e3-232">Сведения о том, как tooredeploy виртуальной Машины, в разделе [повторного развертывания виртуальной машины toonew узла Azure](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="230e3-232">For information about how tooredeploy a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="230e3-233">После завершения этой операции эфемерных диске данные будут потеряны и динамических IP-адресов, связанных с виртуальной машиной hello будет обновляться.</span><span class="sxs-lookup"><span data-stu-id="230e3-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
* <span data-ttu-id="230e3-234">Следуйте инструкциям в разделе hello [как tooreset пароль или SSH для виртуальных машин под управлением Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) для:</span><span class="sxs-lookup"><span data-stu-id="230e3-234">Follow hello instructions in [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="230e3-235">Hello сброс пароля или ключа SSH.</span><span class="sxs-lookup"><span data-stu-id="230e3-235">Reset hello password or SSH key.</span></span>
  * <span data-ttu-id="230e3-236">Создайте учетную запись пользователя *sudo*.</span><span class="sxs-lookup"><span data-stu-id="230e3-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="230e3-237">Сброс конфигурации SSH hello.</span><span class="sxs-lookup"><span data-stu-id="230e3-237">Reset hello SSH configuration.</span></span>
* <span data-ttu-id="230e3-238">Проверьте работоспособность ресурсов виртуальной Машины hello для выявления проблем с платформой.</span><span class="sxs-lookup"><span data-stu-id="230e3-238">Check hello VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="230e3-239">Выберите свою виртуальную машину и прокрутите вниз до раздела **Параметры** > **Проверка работоспособности**.</span><span class="sxs-lookup"><span data-stu-id="230e3-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="230e3-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="230e3-240">Additional resources</span></span>
* <span data-ttu-id="230e3-241">Если по-прежнему не удается tooSSH tooyour ВМ после Здравствуйте, следующие после выполнения шагов, см. [дополнительные действия по устранению неполадок](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview дополнительных шагов tooresolve проблему.</span><span class="sxs-lookup"><span data-stu-id="230e3-241">If you are still unable tooSSH tooyour VM after following hello after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview additional steps tooresolve your issue.</span></span>
* <span data-ttu-id="230e3-242">Дополнительные сведения об устранении неполадок доступа к приложениям см. в разделе [устранить неполадки доступа tooan приложение, работающее на виртуальной машине Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="230e3-242">For more information about troubleshooting application access, see [Troubleshoot access tooan application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="230e3-243">Дополнительные сведения об устранении неполадок виртуальных машин, которые были созданы с помощью hello классической модели развертывания см. в разделе [как tooreset пароль или SSH для виртуальных машин под управлением Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="230e3-243">For more information about troubleshooting virtual machines that were created by using hello classic deployment model, see [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

