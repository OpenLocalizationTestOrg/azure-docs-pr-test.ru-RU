---
title: "вопросы и ответы для виртуальных машин Linux в Azure aaaFrequently | Документы Microsoft"
description: "Предоставляет ответы toosome hello часто задаваемых вопросов о виртуальных машинах Linux, созданных с помощью модели hello диспетчера ресурсов."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="66b96-103">Часто задаваемые вопросы по виртуальным машинам Linux</span><span class="sxs-lookup"><span data-stu-id="66b96-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="66b96-104">В этой статье рассматриваются некоторые распространенные вопросы о виртуальных машин Linux, созданных в Azure с помощью модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="66b96-104">This article addresses some common questions about Linux virtual machines created in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="66b96-105">Версию Windows hello в этом разделе см. в разделе [часто задаваемые вопросы о виртуальных машинах](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="66b96-105">For hello Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="66b96-106">Что можно запускать на виртуальной машине Azure?</span><span class="sxs-lookup"><span data-stu-id="66b96-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="66b96-107">Все подписчики могут запускать на виртуальной машине Azure серверное программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="66b96-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="66b96-108">Дополнительные сведения см. в статье [Linux в Azure — рекомендованные дистрибутивы](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66b96-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="66b96-109">Какой объем памяти можно использовать с виртуальной машиной?</span><span class="sxs-lookup"><span data-stu-id="66b96-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="66b96-110">Каждый диск данных может быть вверх too1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="66b96-110">Each data disk can be up too1 TB.</span></span> <span data-ttu-id="66b96-111">Hello количество дисков данных, которые можно использовать зависит от размера hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="66b96-111">hello number of data disks you can use depends on hello size of hello virtual machine.</span></span> <span data-ttu-id="66b96-112">Дополнительную информацию см. в статье [Размеры виртуальных машин](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66b96-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="66b96-113">Учетная запись хранилища Azure предоставляет хранилище для диска операционной системы hello и диски с данными.</span><span class="sxs-lookup"><span data-stu-id="66b96-113">An Azure storage account provides storage for hello operating system disk and any data disks.</span></span> <span data-ttu-id="66b96-114">Каждый из этих дисков представляет собой VHD-файл, хранящийся как страничный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="66b96-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="66b96-115">Информацию о ценах см. в статье [Информация о ценах на хранилища](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="66b96-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="66b96-116">Как получить доступ к своей виртуальной машине?</span><span class="sxs-lookup"><span data-stu-id="66b96-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="66b96-117">Установите подключение к удаленному toolog на toohello виртуальную машину, используя Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="66b96-117">Establish a remote connection toolog on toohello virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="66b96-118">В разделе hello инструкции о том, как tooconnect [из Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [из Mac и Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66b96-118">See hello instructions on how tooconnect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="66b96-119">По умолчанию SSH поддерживает не более 10 параллельных подключений.</span><span class="sxs-lookup"><span data-stu-id="66b96-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="66b96-120">Это число можно увеличить, изменив файл конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="66b96-120">You can increase this number by editing hello configuration file.</span></span>

<span data-ttu-id="66b96-121">Если возникают проблемы, ознакомьтесь со статьей об [устранении неполадок с подключением Secure Shell (SSH)](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66b96-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a><span data-ttu-id="66b96-122">Можно использовать (/ dev/sdb1) toostore hello временный диск данных?</span><span class="sxs-lookup"><span data-stu-id="66b96-122">Can I use hello temporary disk (/dev/sdb1) toostore data?</span></span>
<span data-ttu-id="66b96-123">Не следует использовать (/ dev/sdb1) toostore hello временный диск данных.</span><span class="sxs-lookup"><span data-stu-id="66b96-123">Don't use hello temporary disk (/dev/sdb1) toostore data.</span></span> <span data-ttu-id="66b96-124">Он обеспечивает лишь временное хранение.</span><span class="sxs-lookup"><span data-stu-id="66b96-124">It is only there for temporary storage.</span></span> <span data-ttu-id="66b96-125">Вы рискуете потерять данные, которые невозможно будет восстановить.</span><span class="sxs-lookup"><span data-stu-id="66b96-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="66b96-126">Можно ли копировать или клонировать существующую виртуальную машину Azure?</span><span class="sxs-lookup"><span data-stu-id="66b96-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="66b96-127">Да.</span><span class="sxs-lookup"><span data-stu-id="66b96-127">Yes.</span></span> <span data-ttu-id="66b96-128">Инструкции см. в разделе [как toocreate копию виртуальной машины Linux в hello модели развертывания диспетчера ресурсов](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66b96-128">For instructions, see [How toocreate a copy of a Linux virtual machine in hello Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="66b96-129">Почему в Azure Resource Manager не отображаются регионы центральной и восточной Канады?</span><span class="sxs-lookup"><span data-stu-id="66b96-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="66b96-130">две новые области Hello центра Канады и Восточная Канада автоматически не зарегистрированы для создания виртуальной машины для существующих подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="66b96-130">hello two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="66b96-131">Эта регистрация выполняется автоматически при развертывании виртуальной машины с помощью hello Azure портала tooany другой области, с помощью диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="66b96-131">This registration is done automatically when a virtual machine is deployed through hello Azure portal tooany other region using Azure Resource Manager.</span></span> <span data-ttu-id="66b96-132">После виртуальной машины не развернутой tooany другой регион Azure hello новые области должны быть доступны для последующих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="66b96-132">After a virtual machine is deployed tooany other Azure region, hello new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a><span data-ttu-id="66b96-133">Можно добавить toomy сетевого Адаптера виртуальной Машины после ее создания?</span><span class="sxs-lookup"><span data-stu-id="66b96-133">Can I add a NIC toomy VM after it's created?</span></span>
<span data-ttu-id="66b96-134">Да, теперь это возможно.</span><span class="sxs-lookup"><span data-stu-id="66b96-134">Yes, this is now possible.</span></span> <span data-ttu-id="66b96-135">Первый toobe потребностей Hello ВМ остановлена освобождена.</span><span class="sxs-lookup"><span data-stu-id="66b96-135">hello VM first needs toobe stopped deallocated.</span></span> <span data-ttu-id="66b96-136">Затем можно добавить или удалить сетевой Адаптер (если он не является последней сетевой Адаптер для виртуальной Машины hello hello).</span><span class="sxs-lookup"><span data-stu-id="66b96-136">Then you can add or remove a NIC (unless it's hello last NIC on hello VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="66b96-137">Есть ли какие-либо требования к имени компьютера?</span><span class="sxs-lookup"><span data-stu-id="66b96-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="66b96-138">Да.</span><span class="sxs-lookup"><span data-stu-id="66b96-138">Yes.</span></span> <span data-ttu-id="66b96-139">Имя компьютера Hello может быть более 64 символов.</span><span class="sxs-lookup"><span data-stu-id="66b96-139">hello computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="66b96-140">Дополнительные сведения об именовании ресурсов см. в [правилах и ограничениях соглашений об именовании](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66b96-140">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="66b96-141">Есть ли какие-либо требования к имени группы ресурсов?</span><span class="sxs-lookup"><span data-stu-id="66b96-141">Are there any resource group name requirements?</span></span>
<span data-ttu-id="66b96-142">Да.</span><span class="sxs-lookup"><span data-stu-id="66b96-142">Yes.</span></span> <span data-ttu-id="66b96-143">Имя группы ресурсов Hello может быть более 90 символов в длину.</span><span class="sxs-lookup"><span data-stu-id="66b96-143">hello resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="66b96-144">Дополнительные сведения о группах ресурсов см. в [правилах и ограничениях соглашений об именовании](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66b96-144">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a><span data-ttu-id="66b96-145">Каковы требования к имени пользователя hello, при создании виртуальной Машины?</span><span class="sxs-lookup"><span data-stu-id="66b96-145">What are hello username requirements when creating a VM?</span></span>
<span data-ttu-id="66b96-146">Длина имени пользователя должно быть от 1 до 64 знаков.</span><span class="sxs-lookup"><span data-stu-id="66b96-146">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="66b96-147">Hello следующие имена пользователей не разрешены:</span><span class="sxs-lookup"><span data-stu-id="66b96-147">hello following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="66b96-148">administrator</span><span class="sxs-lookup"><span data-stu-id="66b96-148">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-149">admin</span><span class="sxs-lookup"><span data-stu-id="66b96-149">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-150">user</span><span class="sxs-lookup"><span data-stu-id="66b96-150">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-151">user1</span><span class="sxs-lookup"><span data-stu-id="66b96-151">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="66b96-152">test</span><span class="sxs-lookup"><span data-stu-id="66b96-152">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-153">user2</span><span class="sxs-lookup"><span data-stu-id="66b96-153">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-154">test1</span><span class="sxs-lookup"><span data-stu-id="66b96-154">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-155">user3</span><span class="sxs-lookup"><span data-stu-id="66b96-155">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="66b96-156">admin1</span><span class="sxs-lookup"><span data-stu-id="66b96-156">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-157">1</span><span class="sxs-lookup"><span data-stu-id="66b96-157">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-158">123</span><span class="sxs-lookup"><span data-stu-id="66b96-158">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-159">a</span><span class="sxs-lookup"><span data-stu-id="66b96-159">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="66b96-160">actuser</span><span class="sxs-lookup"><span data-stu-id="66b96-160">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="66b96-161">adm</span><span class="sxs-lookup"><span data-stu-id="66b96-161">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-162">admin2</span><span class="sxs-lookup"><span data-stu-id="66b96-162">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-163">aspnet</span><span class="sxs-lookup"><span data-stu-id="66b96-163">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="66b96-164">backup</span><span class="sxs-lookup"><span data-stu-id="66b96-164">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-165">console</span><span class="sxs-lookup"><span data-stu-id="66b96-165">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-166">david</span><span class="sxs-lookup"><span data-stu-id="66b96-166">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-167">guest</span><span class="sxs-lookup"><span data-stu-id="66b96-167">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="66b96-168">john</span><span class="sxs-lookup"><span data-stu-id="66b96-168">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-169">владелец</span><span class="sxs-lookup"><span data-stu-id="66b96-169">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-170">root</span><span class="sxs-lookup"><span data-stu-id="66b96-170">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-171">server</span><span class="sxs-lookup"><span data-stu-id="66b96-171">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="66b96-172">sql</span><span class="sxs-lookup"><span data-stu-id="66b96-172">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-173">support</span><span class="sxs-lookup"><span data-stu-id="66b96-173">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-174">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="66b96-174">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-175">sys</span><span class="sxs-lookup"><span data-stu-id="66b96-175">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="66b96-176">test2</span><span class="sxs-lookup"><span data-stu-id="66b96-176">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-177">test3</span><span class="sxs-lookup"><span data-stu-id="66b96-177">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-178">user4</span><span class="sxs-lookup"><span data-stu-id="66b96-178">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="66b96-179">user5</span><span class="sxs-lookup"><span data-stu-id="66b96-179">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a><span data-ttu-id="66b96-180">Каковы требования к паролю hello при создании виртуальной Машины?</span><span class="sxs-lookup"><span data-stu-id="66b96-180">What are hello password requirements when creating a VM?</span></span>
<span data-ttu-id="66b96-181">Пароли необходимо 6 72 символов и удовлетворять 3 из следующих 4 требованиям сложности hello:</span><span class="sxs-lookup"><span data-stu-id="66b96-181">Passwords must be 6 - 72 characters in length and meet 3 out of hello following 4 complexity requirements:</span></span>

* <span data-ttu-id="66b96-182">используются строчные знаки;</span><span class="sxs-lookup"><span data-stu-id="66b96-182">Have lower characters</span></span>
* <span data-ttu-id="66b96-183">используются прописные знаки;</span><span class="sxs-lookup"><span data-stu-id="66b96-183">Have upper characters</span></span>
* <span data-ttu-id="66b96-184">используется цифра;</span><span class="sxs-lookup"><span data-stu-id="66b96-184">Have a digit</span></span>
* <span data-ttu-id="66b96-185">используется специальный знак (регулярное выражение [\W_]).</span><span class="sxs-lookup"><span data-stu-id="66b96-185">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="66b96-186">Hello следующие пароли не допускаются:</span><span class="sxs-lookup"><span data-stu-id="66b96-186">hello following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="66b96-187">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="66b96-187">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="66b96-188">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="66b96-188">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="66b96-189">Password!</span><span class="sxs-lookup"><span data-stu-id="66b96-189">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="66b96-190">Password1</span><span class="sxs-lookup"><span data-stu-id="66b96-190">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="66b96-191">Password22</span><span class="sxs-lookup"><span data-stu-id="66b96-191">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="66b96-192">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="66b96-192">iloveyou!</span></span></td>
    </tr>
</table>
