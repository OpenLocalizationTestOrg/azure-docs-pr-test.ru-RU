---
title: "Устранение неполадок SSH-подключения к виртуальной машине Azure | Документация Майкрософт"
description: "Диагностика ошибок, например \"ошибка SSH-подключения\" или \"в SSH-подключении отказано\", для виртуальной машины под управлением Linux."
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
ms.openlocfilehash: 3a282c8b2c2ba2749de6a2d3688bd57d75703b22
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-ssh-connections-to-an-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="eae33-104">Устранение неполадок с SSH-подключением к виртуальной машине Azure Linux: сбой, ошибка или отклонение</span><span class="sxs-lookup"><span data-stu-id="eae33-104">Troubleshoot SSH connections to an Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="eae33-105">При попытке подключения к виртуальной машине Azure под управлением Linux ошибка, сбой или отклонение подключения Secure Shell (SSH) может возникнуть по нескольким причинам.</span><span class="sxs-lookup"><span data-stu-id="eae33-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try to connect to a Linux virtual machine (VM).</span></span> <span data-ttu-id="eae33-106">В этой статье вы узнаете, как их выявить и устранить.</span><span class="sxs-lookup"><span data-stu-id="eae33-106">This article helps you find and correct the problems.</span></span> <span data-ttu-id="eae33-107">Для устранения неполадок и решения проблем с подключением можно воспользоваться порталом Azure, Azure CLI или расширением для доступа к виртуальной машине для Linux.</span><span class="sxs-lookup"><span data-stu-id="eae33-107">You can use the Azure portal, Azure CLI, or VM Access Extension for Linux to troubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="eae33-108">Если в любой момент при изучении этой статьи вам потребуется дополнительная помощь, вы можете обратиться к экспертам по Azure на [форумах MSDN Azure и Stack Overflow](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="eae33-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="eae33-109">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="eae33-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="eae33-110">Перейдите на [сайт поддержки Azure](http://azure.microsoft.com/support/options/) и щелкните **Получить поддержку**.</span><span class="sxs-lookup"><span data-stu-id="eae33-110">Go to the [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="eae33-111">Дополнительные сведения об использовании службы поддержки Azure см. в статье [Часто задаваемые вопросы о поддержке Microsoft Azure](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="eae33-111">For information about using Azure Support, read the [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="eae33-112">Действия по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="eae33-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="eae33-113">После выполнения каждого шага устранения неполадок попробуйте подключиться к виртуальной машине еще раз.</span><span class="sxs-lookup"><span data-stu-id="eae33-113">After each troubleshooting step, try reconnecting to the VM.</span></span>

1. <span data-ttu-id="eae33-114">сбросить конфигурацию SSH.</span><span class="sxs-lookup"><span data-stu-id="eae33-114">Reset the SSH configuration.</span></span>
2. <span data-ttu-id="eae33-115">Сбросьте учетные данные пользователя.</span><span class="sxs-lookup"><span data-stu-id="eae33-115">Reset the credentials for the user.</span></span>
3. <span data-ttu-id="eae33-116">Убедитесь, что правила [группы безопасности сети](../../virtual-network/virtual-networks-nsg.md) разрешают трафик SSH.</span><span class="sxs-lookup"><span data-stu-id="eae33-116">Verify the [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="eae33-117">Убедитесь, что правило для разрешения трафика SSH есть в группе безопасности сети (по умолчанию — TCP-порт 22).</span><span class="sxs-lookup"><span data-stu-id="eae33-117">Ensure that a Network Security Group rule exists to permit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="eae33-118">Нельзя использовать перенаправление и сопоставление портов, не используя Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="eae33-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="eae33-119">Проверьте [работоспособность ресурсов виртуальной машины](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eae33-119">Check the [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="eae33-120">Убедитесь, что виртуальная машина работоспособна.</span><span class="sxs-lookup"><span data-stu-id="eae33-120">Ensure that the VM reports as being healthy.</span></span>
   * <span data-ttu-id="eae33-121">Если включена диагностика загрузки, убедитесь, что виртуальная машина не сообщала об ошибках загрузки в журналах.</span><span class="sxs-lookup"><span data-stu-id="eae33-121">If you have boot diagnostics enabled, verify the VM is not reporting boot errors in the logs.</span></span>
5. <span data-ttu-id="eae33-122">Перезапустите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="eae33-122">Restart the VM.</span></span>
6. <span data-ttu-id="eae33-123">Заново разверните виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="eae33-123">Redeploy the VM.</span></span>

<span data-ttu-id="eae33-124">Читайте статью дальше, если вам нужны более подробные инструкции или пояснения об исправлении неполадок.</span><span class="sxs-lookup"><span data-stu-id="eae33-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-to-troubleshoot-ssh-connection-issues"></a><span data-ttu-id="eae33-125">Доступные методы устранения неполадок подключения SSH</span><span class="sxs-lookup"><span data-stu-id="eae33-125">Available methods to troubleshoot SSH connection issues</span></span>
<span data-ttu-id="eae33-126">Вы можете сбросить учетные данные или конфигурацию SSH одним из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="eae33-126">You can reset credentials or SSH configuration using one of the following methods:</span></span>

* <span data-ttu-id="eae33-127">[Портал Azure](#use-the-azure-portal) отлично подходит, когда нужно быстро сбросить конфигурацию или ключ SSH, а у вас не установлены инструменты Azure.</span><span class="sxs-lookup"><span data-stu-id="eae33-127">[Azure portal](#use-the-azure-portal) - great if you need to quickly reset the SSH configuration or SSH key and you don't have the Azure tools installed.</span></span>
* <span data-ttu-id="eae33-128">[Azure CLI 2.0](#use-the-azure-cli-20). Если вы уже открыли командную строку, быстро сбросьте конфигурацию SSH или учетные данные.</span><span class="sxs-lookup"><span data-stu-id="eae33-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on the command line, quickly reset the SSH configuration or credentials.</span></span> <span data-ttu-id="eae33-129">Для этого можно также использовать [Azure CLI 1.0](#use-the-azure-cli-10).</span><span class="sxs-lookup"><span data-stu-id="eae33-129">You can also use the [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="eae33-130">[Расширение Azure VMAccessForLinux.](#use-the-vmaccess-extension) Создайте и повторно используйте файлы определения JSON для сброса учетных данных пользователя или конфигурации SSH.</span><span class="sxs-lookup"><span data-stu-id="eae33-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files to reset the SSH configuration or user credentials.</span></span>

<span data-ttu-id="eae33-131">После выполнения каждого шага устранения неполадок попробуйте подключиться к виртуальной машине еще раз.</span><span class="sxs-lookup"><span data-stu-id="eae33-131">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="eae33-132">Если все еще не удается подключиться, то попробуйте выполнить следующее действие.</span><span class="sxs-lookup"><span data-stu-id="eae33-132">If you still cannot connect, try the next step.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="eae33-133">Использование портала Azure</span><span class="sxs-lookup"><span data-stu-id="eae33-133">Use the Azure portal</span></span>
<span data-ttu-id="eae33-134">На портале Azure предусмотрена возможность быстрого сброса конфигурации SSH или учетных данных пользователей без установки каких-либо инструментов на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="eae33-134">The Azure portal provides a quick way to reset the SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="eae33-135">Выберите свою виртуальную машину на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="eae33-135">Select your VM in the Azure portal.</span></span> <span data-ttu-id="eae33-136">Прокрутите вниз до раздела **Поддержка и устранение неполадок** и выберите **Сбросить пароль**, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="eae33-136">Scroll down to the **Support + Troubleshooting** section and select **Reset password** as in the following example:</span></span>

![Сброс конфигурации SSH или учетных данных на портале Azure](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-the-ssh-configuration"></a><span data-ttu-id="eae33-138">Сброс конфигурации SSH</span><span class="sxs-lookup"><span data-stu-id="eae33-138">Reset the SSH configuration</span></span>
<span data-ttu-id="eae33-139">Сначала в раскрывающемся меню **Режим** выберите `Reset configuration only`, как на предыдущем снимке экрана, и нажмите кнопку **Сброс**.</span><span class="sxs-lookup"><span data-stu-id="eae33-139">As a first step, select `Reset configuration only` from the **Mode** drop-down menu as in the preceding screenshot, then click the **Reset** button.</span></span> <span data-ttu-id="eae33-140">Сделав это, попытайтесь снова войти в виртуальною машину.</span><span class="sxs-lookup"><span data-stu-id="eae33-140">Once this action has completed, try to access your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="eae33-141">Сброс учетных данных SSH пользователя</span><span class="sxs-lookup"><span data-stu-id="eae33-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="eae33-142">Чтобы сбросить учетные данные имеющегося пользователя, в раскрывающемся меню **Режим** выберите `Reset SSH public key` или `Reset password`, как на приведенном выше снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="eae33-142">To reset the credentials of an existing user, select either `Reset SSH public key` or `Reset password` from the **Mode** drop-down menu as in the preceding screenshot.</span></span> <span data-ttu-id="eae33-143">Укажите имя пользователя и ключ SSH или новый пароль, а затем нажмите кнопку **Сброс**.</span><span class="sxs-lookup"><span data-stu-id="eae33-143">Specify the username and an SSH key or new password, then click the **Reset** button.</span></span>

<span data-ttu-id="eae33-144">Кроме того, в этом меню можно создать пользователя с привилегиями sudo на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="eae33-144">You can also create a user with sudo privileges on the VM from this menu.</span></span> <span data-ttu-id="eae33-145">Введите новое имя пользователя и соответствующий пароль или ключ SSH, а затем нажмите кнопку **Сброс**.</span><span class="sxs-lookup"><span data-stu-id="eae33-145">Enter a new username and associated password or SSH key, and then click the **Reset** button.</span></span>

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="eae33-146">Использование Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="eae33-146">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="eae33-147">Установите последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) (если вы еще этого не сделали) и войдите в учетную запись Azure, выполнив команду [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="eae33-147">If you haven't already, install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="eae33-148">Если вы создали и отправили пользовательский образ диска Linux, убедитесь, что установлен [агент Linux для Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) версии 2.0.5 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="eae33-148">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="eae33-149">В виртуальных машинах, созданных с помощью образов из коллекции, это расширение для доступа уже установлено и настроено.</span><span class="sxs-lookup"><span data-stu-id="eae33-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="eae33-150">Сбросьте конфигурацию SSH.</span><span class="sxs-lookup"><span data-stu-id="eae33-150">Reset SSH configuration</span></span>
<span data-ttu-id="eae33-151">Вы можете сначала попробовать сбросить конфигурацию SSH к значениям по умолчанию и перезагрузить сервер SSH на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="eae33-151">You can initially try resetting the SSH configuration to default values and rebooting the SSH server on the VM.</span></span> <span data-ttu-id="eae33-152">Обратите внимание, что при этом не изменяется имя учетной записи пользователя, пароль или ключи SSH.</span><span class="sxs-lookup"><span data-stu-id="eae33-152">Note that this does not change the user account name, password, or SSH keys.</span></span>
<span data-ttu-id="eae33-153">В следующем примере используется команда [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) для сброса конфигурации SSH на виртуальной машине с именем `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="eae33-153">The following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) to reset the SSH configuration on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="eae33-154">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="eae33-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="eae33-155">Сброс учетных данных SSH пользователя</span><span class="sxs-lookup"><span data-stu-id="eae33-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="eae33-156">В следующем примере используется команда [aaz vm user update](/cli/azure/vm/user#update), чтобы сбросить учетные данные для `myUsername` к значению, указанному в `myPassword` на виртуальной машине `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="eae33-156">The following example uses [az vm user update](/cli/azure/vm/user#update) to reset the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="eae33-157">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="eae33-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="eae33-158">При использовании аутентификации с помощью ключа SSH можно сбросить ключ SSH для отдельного пользователя.</span><span class="sxs-lookup"><span data-stu-id="eae33-158">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="eae33-159">В следующем примере используется команда **az vm access set-linux-user**, чтобы сбросить учетные данные для `~/.ssh/id_rsa.pub` к значению, указанному в `myUsername` на виртуальной машине `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="eae33-159">The following example uses **az vm access set-linux-user** to update the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="eae33-160">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="eae33-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-the-vmaccess-extension"></a><span data-ttu-id="eae33-161">Использование расширения VMAccess</span><span class="sxs-lookup"><span data-stu-id="eae33-161">Use the VMAccess extension</span></span>
<span data-ttu-id="eae33-162">Расширение для доступа к виртуальной машине для Linux выполняет чтение в JSON-файле. При этом сбрасывается SSHD и ключ SSH или добавляется пользователь.</span><span class="sxs-lookup"><span data-stu-id="eae33-162">The VM Access Extension for Linux reads in a json file that defines actions to carry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="eae33-163">Azure CLI по-прежнему используется для вызова расширения VMAccess, но при необходимости JSON-файлы можно использовать повторно в нескольких виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="eae33-163">You still use the Azure CLI to call the VMAccess extension, but you can reuse the json files across multiple VMs if desired.</span></span> <span data-ttu-id="eae33-164">Такой подход позволяет создать репозиторий JSON-файлов, которые можно впоследствии вызывать для заданных сценариев.</span><span class="sxs-lookup"><span data-stu-id="eae33-164">This approach allows you to create a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="eae33-165">Сброс SSHD</span><span class="sxs-lookup"><span data-stu-id="eae33-165">Reset SSHD</span></span>
<span data-ttu-id="eae33-166">Создайте файл `settings.json` со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="eae33-166">Create a file named `settings.json` with the following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="eae33-167">С помощью Azure CLI вызовите расширение `VMAccessForLinux` для сброса подключения SSHD, указав JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="eae33-167">Using the Azure CLI, you then call the `VMAccessForLinux` extension to reset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="eae33-168">В следующем примере используется команда [az vm extension set](/cli/azure/vm/extension#set) для сброса SSHD на виртуальной машине с именем `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="eae33-168">The following example uses [az vm extension set](/cli/azure/vm/extension#set) to reset SSHD on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="eae33-169">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="eae33-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="eae33-170">Сброс учетных данных SSH пользователя</span><span class="sxs-lookup"><span data-stu-id="eae33-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="eae33-171">Если SSHD работает корректно, можно сбросить учетные данные для отдельного пользователя.</span><span class="sxs-lookup"><span data-stu-id="eae33-171">If SSHD appears to function correctly, you can reset the credentials for a giver user.</span></span> <span data-ttu-id="eae33-172">Чтобы сбросить пароль для пользователя, создайте файл с именем `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="eae33-172">To reset the password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="eae33-173">В следующем примере сбрасываются учетные данные для имени пользователя `myUsername` до значения, указанного в пароле `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="eae33-173">The following example resets the credentials for `myUsername` to the value specified in `myPassword`.</span></span> <span data-ttu-id="eae33-174">Введите следующие строки в файл `settings.json`, используя свои значения:</span><span class="sxs-lookup"><span data-stu-id="eae33-174">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="eae33-175">Чтобы сбросить ключ SSH для пользователя, сначала создайте файл с именем `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="eae33-175">Or to reset the SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="eae33-176">В следующем примере сбрасываются учетные данные для имени пользователя `myUsername` до значения, указанного в пароле `myPassword` на виртуальной машине `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="eae33-176">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="eae33-177">Введите следующие строки в файл `settings.json`, используя свои значения:</span><span class="sxs-lookup"><span data-stu-id="eae33-177">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="eae33-178">Создав JSON-файл, используйте Azure CLI, чтобы вызвать расширение `VMAccessForLinux` для сброса учетных данных пользователя SSH, указав JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="eae33-178">After creating your json file, use the Azure CLI to call the `VMAccessForLinux` extension to reset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="eae33-179">В следующем примере сбрасываются учетные данные на виртуальной машине `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="eae33-179">The following example resets credentials on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="eae33-180">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="eae33-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="eae33-181">Использование Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="eae33-181">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="eae33-182">[Установите Azure CLI 1.0 и подключитесь к подписке Azure](../../cli-install-nodejs.md) (если вы еще этого не сделали).</span><span class="sxs-lookup"><span data-stu-id="eae33-182">If you haven't already, [install the Azure CLI 1.0 and connect to your Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="eae33-183">Убедитесь, что используется режим Resource Manager следующим образом:</span><span class="sxs-lookup"><span data-stu-id="eae33-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="eae33-184">Если вы создали и отправили пользовательский образ диска Linux, убедитесь, что установлен [агент Linux для Microsoft Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) версии 2.0.5 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="eae33-184">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="eae33-185">В виртуальных машинах, созданных с помощью образов из коллекции, это расширение для доступа уже установлено и настроено.</span><span class="sxs-lookup"><span data-stu-id="eae33-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="eae33-186">Сбросьте конфигурацию SSH.</span><span class="sxs-lookup"><span data-stu-id="eae33-186">Reset SSH configuration</span></span>
<span data-ttu-id="eae33-187">Может быть неправильно настроена сама конфигурация SSHD, или в службе произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="eae33-187">The SSHD configuration itself may be misconfigured or the service encountered an error.</span></span> <span data-ttu-id="eae33-188">Чтобы убедиться, что конфигурация SSH действительна, можно выполнить сброс SSHD.</span><span class="sxs-lookup"><span data-stu-id="eae33-188">You can reset SSHD to make sure the SSH configuration itself is valid.</span></span> <span data-ttu-id="eae33-189">При устранении неполадок сначала нужно сбросить SSHD.</span><span class="sxs-lookup"><span data-stu-id="eae33-189">Resetting SSHD should be the first troubleshooting step you take.</span></span>

<span data-ttu-id="eae33-190">В следующем примере перезапускается SSHD на виртуальной машине `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="eae33-190">The following example resets SSHD on a VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="eae33-191">Используйте собственные имена для виртуальной машины и группы ресурсов следующим образом:</span><span class="sxs-lookup"><span data-stu-id="eae33-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="eae33-192">Сброс учетных данных SSH пользователя</span><span class="sxs-lookup"><span data-stu-id="eae33-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="eae33-193">Если SSHD работает корректно, можно сбросить пароль для отдельного пользователя.</span><span class="sxs-lookup"><span data-stu-id="eae33-193">If SSHD appears to function correctly, you can reset the password for a giver user.</span></span> <span data-ttu-id="eae33-194">В следующем примере сбрасываются учетные данные для имени пользователя `myUsername` до значения, указанного в пароле `myPassword` на виртуальной машине `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="eae33-194">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="eae33-195">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="eae33-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="eae33-196">При использовании аутентификации с помощью ключа SSH можно сбросить ключ SSH для отдельного пользователя.</span><span class="sxs-lookup"><span data-stu-id="eae33-196">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="eae33-197">В следующем примере обновляется ключ SSH, хранящийся в файле `~/.ssh/id_rsa.pub`, для пользователя с именем `myUsername` на виртуальной машине `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="eae33-197">The following example updates the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="eae33-198">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="eae33-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="eae33-199">Перезапуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="eae33-199">Restart a VM</span></span>
<span data-ttu-id="eae33-200">Если вы сбросили учетные данные пользователя и конфигурацию SSH или столкнулись с ошибкой при этом, попробуйте перезапустить виртуальную машину, чтобы устранить неполадки с базовыми вычислительными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="eae33-200">If you have reset the SSH configuration and user credentials, or encountered an error in doing so, you can try restarting the VM to address underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="eae33-201">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="eae33-201">Azure portal</span></span>
<span data-ttu-id="eae33-202">Чтобы перезапустить виртуальную машину с помощью портала Azure, выберите виртуальную машину и нажмите кнопку **Перезапуск**, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="eae33-202">To restart a VM using the Azure portal, select your VM and click the **Restart** button as in the following example:</span></span>

![Перезапуск виртуальной машины на портале Azure](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="eae33-204">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="eae33-204">Azure CLI 1.0</span></span>
<span data-ttu-id="eae33-205">В следующем примере перезапускается виртуальная машина `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="eae33-205">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="eae33-206">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="eae33-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="eae33-207">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="eae33-207">Azure CLI 2.0</span></span>
<span data-ttu-id="eae33-208">В следующем примере используется команда [az vm restart](/cli/azure/vm#restart), чтобы перезапустить виртуальную машину `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="eae33-208">The following example uses [az vm restart](/cli/azure/vm#restart) to restart the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="eae33-209">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="eae33-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="eae33-210">Повторное развертывание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="eae33-210">Redeploy a VM</span></span>
<span data-ttu-id="eae33-211">Виртуальную машину можно повторно развернуть на другом узле в Azure, что поможет устранить любые базовые сетевые проблемы.</span><span class="sxs-lookup"><span data-stu-id="eae33-211">You can redeploy a VM to another node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="eae33-212">Сведения о повторном развертывании виртуальной машины на новом узле Azure см. [здесь](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eae33-212">For information about redeploying a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="eae33-213">Обратите внимание, что после этой операции будут потеряны данные на временном диске, а также изменятся динамические IP-адреса, связанные с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="eae33-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="eae33-214">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="eae33-214">Azure portal</span></span>
<span data-ttu-id="eae33-215">Чтобы повторно развернуть виртуальную машину с помощью портала Azure, выберите виртуальную машину и прокрутите вниз до раздела **Поддержка и устранение неполадок**.</span><span class="sxs-lookup"><span data-stu-id="eae33-215">To redeploy a VM using the Azure portal, select your VM and scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="eae33-216">Нажмите кнопку **Повторить развертывание**, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="eae33-216">Click the **Redeploy** button as in the following example:</span></span>

![Повторное развертывание виртуальной машины на портале Azure](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="eae33-218">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="eae33-218">Azure CLI 1.0</span></span>
<span data-ttu-id="eae33-219">В следующем примере повторно развертывается виртуальная машина `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="eae33-219">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="eae33-220">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="eae33-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="eae33-221">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="eae33-221">Azure CLI 2.0</span></span>
<span data-ttu-id="eae33-222">В следующем примере используется команда [az vm restart](/cli/azure/vm#redeploy), чтобы повторно развернуть виртуальную машину `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="eae33-222">The following example use [az vm redeploy](/cli/azure/vm#redeploy) to redeploy the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="eae33-223">Используйте свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="eae33-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-the-classic-deployment-model"></a><span data-ttu-id="eae33-224">Виртуальные машины, созданные с использованием классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="eae33-224">VMs created by using the Classic deployment model</span></span>
<span data-ttu-id="eae33-225">Для устранения наиболее распространенных сбоев SSH-подключения для виртуальных машин, созданных с помощью классической модели развертывания, попробуйте выполнить указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="eae33-225">Try these steps to resolve the most common SSH connection failures for VMs that were created by using the classic deployment model.</span></span> <span data-ttu-id="eae33-226">После выполнения каждого шага попробуйте подключиться к виртуальной машине еще раз.</span><span class="sxs-lookup"><span data-stu-id="eae33-226">After each step, try reconnecting to the VM.</span></span>

* <span data-ttu-id="eae33-227">Выполните сброс удаленного доступа на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eae33-227">Reset remote access from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="eae33-228">На портале Azure выберите свою виртуальную машину и нажмите кнопку **Reset Remote...** (Удаленный сброс...).</span><span class="sxs-lookup"><span data-stu-id="eae33-228">On the Azure portal, select your VM and click the **Reset Remote...** button.</span></span>
* <span data-ttu-id="eae33-229">Перезапустите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="eae33-229">Restart the VM.</span></span> <span data-ttu-id="eae33-230">На [портале Azure](https://portal.azure.com) выберите свою виртуальную машину и нажмите кнопку **Перезапуск**.</span><span class="sxs-lookup"><span data-stu-id="eae33-230">On the [Azure portal](https://portal.azure.com), select your VM and click the **Restart** button.</span></span>
    
* <span data-ttu-id="eae33-231">Повторно разверните виртуальную машину на новом узле Azure.</span><span class="sxs-lookup"><span data-stu-id="eae33-231">Redeploy the VM to a new Azure node.</span></span> <span data-ttu-id="eae33-232">Сведения о повторном развертывании виртуальной машины на новом узле Azure см. [здесь](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eae33-232">For information about how to redeploy a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="eae33-233">Обратите внимание, что после этой операции будут потеряны данные на временном диске, а также изменятся динамические IP-адреса, связанные с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="eae33-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
* <span data-ttu-id="eae33-234">Следуйте указаниям в статье о [сбросе пароля или ключа SSH в виртуальных машинах Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json), чтобы сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="eae33-234">Follow the instructions in [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="eae33-235">сбросить пароль или ключ SSH;</span><span class="sxs-lookup"><span data-stu-id="eae33-235">Reset the password or SSH key.</span></span>
  * <span data-ttu-id="eae33-236">Создайте учетную запись пользователя *sudo*.</span><span class="sxs-lookup"><span data-stu-id="eae33-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="eae33-237">сбросить конфигурацию SSH.</span><span class="sxs-lookup"><span data-stu-id="eae33-237">Reset the SSH configuration.</span></span>
* <span data-ttu-id="eae33-238">Проверьте работоспособность ресурсов виртуальной машины, чтобы выявить любые проблемы, связанные с платформой.</span><span class="sxs-lookup"><span data-stu-id="eae33-238">Check the VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="eae33-239">Выберите свою виртуальную машину и прокрутите вниз до раздела **Параметры** > **Проверка работоспособности**.</span><span class="sxs-lookup"><span data-stu-id="eae33-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eae33-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="eae33-240">Additional resources</span></span>
* <span data-ttu-id="eae33-241">Если вам по-прежнему не удается выполнить SSH-подключение к виртуальной машине, см. [дополнительные действия по устранению неполадок](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), которые позволят просмотреть дополнительные шаги по устранению проблемы.</span><span class="sxs-lookup"><span data-stu-id="eae33-241">If you are still unable to SSH to your VM after following the after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to review additional steps to resolve your issue.</span></span>
* <span data-ttu-id="eae33-242">Дополнительные сведения об устранении неполадок с доступом к приложению см. в статье [Устранение неполадок доступа к приложению, выполняющемуся в виртуальной машине Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eae33-242">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="eae33-243">Дополнительные сведения об устранении неполадок на виртуальных машинах, созданных с помощью классической модели развертывания, см. в статье о [сбросе пароля или ключа SSH в виртуальных машинах Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eae33-243">For more information about troubleshooting virtual machines that were created by using the classic deployment model, see [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

