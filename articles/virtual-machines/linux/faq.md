---
title: "Часто задаваемые вопросы о виртуальных машинах Linux в Azure | Документация Майкрософт"
description: "В этой статье содержатся ответы на некоторые распространенные вопросы о виртуальных машинах Linux, созданных с помощью модели Resource Manager."
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
ms.openlocfilehash: 0e06d21bd0b6ef807f38e41dcd50c9cd715607a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="a6b27-103">Часто задаваемые вопросы по виртуальным машинам Linux</span><span class="sxs-lookup"><span data-stu-id="a6b27-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="a6b27-104">В этой статье содержатся ответы на некоторые распространенные вопросы о виртуальных машинах Linux, созданных в Azure посредством модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a6b27-104">This article addresses some common questions about Linux virtual machines created in Azure using the Resource Manager deployment model.</span></span> <span data-ttu-id="a6b27-105">Версия этой статьи для Windows — [Часто задаваемые вопросы по виртуальным машинам Windows](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6b27-105">For the Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="a6b27-106">Что можно запускать на виртуальной машине Azure?</span><span class="sxs-lookup"><span data-stu-id="a6b27-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="a6b27-107">Все подписчики могут запускать на виртуальной машине Azure серверное программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="a6b27-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="a6b27-108">Дополнительные сведения см. в статье [Linux в Azure — рекомендованные дистрибутивы](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6b27-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="a6b27-109">Какой объем памяти можно использовать с виртуальной машиной?</span><span class="sxs-lookup"><span data-stu-id="a6b27-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="a6b27-110">Каждый диск данных может иметь объем до 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="a6b27-110">Each data disk can be up to 1 TB.</span></span> <span data-ttu-id="a6b27-111">Количество дисков данных, которое можно использовать, зависит от размера виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a6b27-111">The number of data disks you can use depends on the size of the virtual machine.</span></span> <span data-ttu-id="a6b27-112">Дополнительную информацию см. в статье [Размеры виртуальных машин](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6b27-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="a6b27-113">Учетная запись хранения Azure предоставляет хранилище для диска операционной системы и любых дисков данных.</span><span class="sxs-lookup"><span data-stu-id="a6b27-113">An Azure storage account provides storage for the operating system disk and any data disks.</span></span> <span data-ttu-id="a6b27-114">Каждый из этих дисков представляет собой VHD-файл, хранящийся как страничный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="a6b27-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="a6b27-115">Информацию о ценах см. в статье [Информация о ценах на хранилища](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="a6b27-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="a6b27-116">Как получить доступ к своей виртуальной машине?</span><span class="sxs-lookup"><span data-stu-id="a6b27-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="a6b27-117">Установите удаленное подключение для входа на виртуальную машину с помощью Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="a6b27-117">Establish a remote connection to log on to the virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="a6b27-118">Ознакомьтесь с инструкциями по подключению [из Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [Linux и Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6b27-118">See the instructions on how to connect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="a6b27-119">По умолчанию SSH поддерживает не более 10 параллельных подключений.</span><span class="sxs-lookup"><span data-stu-id="a6b27-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="a6b27-120">Число доступных параллельных подключений можно увеличить, изменив файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a6b27-120">You can increase this number by editing the configuration file.</span></span>

<span data-ttu-id="a6b27-121">Если возникают проблемы, ознакомьтесь со статьей об [устранении неполадок с подключением Secure Shell (SSH)](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6b27-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-the-temporary-disk-devsdb1-to-store-data"></a><span data-ttu-id="a6b27-122">Можно ли использовать временный диск (/dev/sdb1) для хранения данных?</span><span class="sxs-lookup"><span data-stu-id="a6b27-122">Can I use the temporary disk (/dev/sdb1) to store data?</span></span>
<span data-ttu-id="a6b27-123">Не используйте временный диск (/dev/sdb1) для хранения данных.</span><span class="sxs-lookup"><span data-stu-id="a6b27-123">Don't use the temporary disk (/dev/sdb1) to store data.</span></span> <span data-ttu-id="a6b27-124">Он обеспечивает лишь временное хранение.</span><span class="sxs-lookup"><span data-stu-id="a6b27-124">It is only there for temporary storage.</span></span> <span data-ttu-id="a6b27-125">Вы рискуете потерять данные, которые невозможно будет восстановить.</span><span class="sxs-lookup"><span data-stu-id="a6b27-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="a6b27-126">Можно ли копировать или клонировать существующую виртуальную машину Azure?</span><span class="sxs-lookup"><span data-stu-id="a6b27-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="a6b27-127">Да.</span><span class="sxs-lookup"><span data-stu-id="a6b27-127">Yes.</span></span> <span data-ttu-id="a6b27-128">Указания доступны в статье [Создание копии виртуальной машины Linux, работающей в Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6b27-128">For instructions, see [How to create a copy of a Linux virtual machine in the Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="a6b27-129">Почему в Azure Resource Manager не отображаются регионы центральной и восточной Канады?</span><span class="sxs-lookup"><span data-stu-id="a6b27-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="a6b27-130">При создании виртуальных машин в существующих подписках Azure эти два новых региона не регистрируются автоматически.</span><span class="sxs-lookup"><span data-stu-id="a6b27-130">The two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="a6b27-131">Регистрация осуществляется автоматически при развертывании виртуальной машины на портале Azure в любом другом регионе с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a6b27-131">This registration is done automatically when a virtual machine is deployed through the Azure portal to any other region using Azure Resource Manager.</span></span> <span data-ttu-id="a6b27-132">После развертывания виртуальной машины в любом другом регионе Azure новые регионы станут доступными для последующих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a6b27-132">After a virtual machine is deployed to any other Azure region, the new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-to-my-vm-after-its-created"></a><span data-ttu-id="a6b27-133">Создав виртуальную машину, могу я добавить к ней сетевой адаптер?</span><span class="sxs-lookup"><span data-stu-id="a6b27-133">Can I add a NIC to my VM after it's created?</span></span>
<span data-ttu-id="a6b27-134">Да, теперь это возможно.</span><span class="sxs-lookup"><span data-stu-id="a6b27-134">Yes, this is now possible.</span></span> <span data-ttu-id="a6b27-135">Сначала виртуальную машину нужно остановить и отменить ее распределение.</span><span class="sxs-lookup"><span data-stu-id="a6b27-135">The VM first needs to be stopped deallocated.</span></span> <span data-ttu-id="a6b27-136">Затем можно добавить или удалить сетевую карту (за исключением последней сетевой карты на виртуальной машине).</span><span class="sxs-lookup"><span data-stu-id="a6b27-136">Then you can add or remove a NIC (unless it's the last NIC on the VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="a6b27-137">Есть ли какие-либо требования к имени компьютера?</span><span class="sxs-lookup"><span data-stu-id="a6b27-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="a6b27-138">Да.</span><span class="sxs-lookup"><span data-stu-id="a6b27-138">Yes.</span></span> <span data-ttu-id="a6b27-139">Длина имени компьютера не должна превышать 64 знака.</span><span class="sxs-lookup"><span data-stu-id="a6b27-139">The computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="a6b27-140">Дополнительные сведения об именовании ресурсов см. в [правилах и ограничениях соглашений об именовании](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6b27-140">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="a6b27-141">Есть ли какие-либо требования к имени группы ресурсов?</span><span class="sxs-lookup"><span data-stu-id="a6b27-141">Are there any resource group name requirements?</span></span>
<span data-ttu-id="a6b27-142">Да.</span><span class="sxs-lookup"><span data-stu-id="a6b27-142">Yes.</span></span> <span data-ttu-id="a6b27-143">Длина имени группы ресурсов не должна превышать 90 знаков.</span><span class="sxs-lookup"><span data-stu-id="a6b27-143">The resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="a6b27-144">Дополнительные сведения о группах ресурсов см. в [правилах и ограничениях соглашений об именовании](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6b27-144">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-the-username-requirements-when-creating-a-vm"></a><span data-ttu-id="a6b27-145">Какие требования к имени пользователя при создании виртуальной машины?</span><span class="sxs-lookup"><span data-stu-id="a6b27-145">What are the username requirements when creating a VM?</span></span>
<span data-ttu-id="a6b27-146">Длина имени пользователя должно быть от 1 до 64 знаков.</span><span class="sxs-lookup"><span data-stu-id="a6b27-146">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="a6b27-147">Не допускаются следующие имена пользователей:</span><span class="sxs-lookup"><span data-stu-id="a6b27-147">The following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="a6b27-148">administrator</span><span class="sxs-lookup"><span data-stu-id="a6b27-148">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-149">admin</span><span class="sxs-lookup"><span data-stu-id="a6b27-149">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-150">user</span><span class="sxs-lookup"><span data-stu-id="a6b27-150">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-151">user1</span><span class="sxs-lookup"><span data-stu-id="a6b27-151">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="a6b27-152">test</span><span class="sxs-lookup"><span data-stu-id="a6b27-152">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-153">user2</span><span class="sxs-lookup"><span data-stu-id="a6b27-153">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-154">test1</span><span class="sxs-lookup"><span data-stu-id="a6b27-154">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-155">user3</span><span class="sxs-lookup"><span data-stu-id="a6b27-155">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="a6b27-156">admin1</span><span class="sxs-lookup"><span data-stu-id="a6b27-156">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-157">1</span><span class="sxs-lookup"><span data-stu-id="a6b27-157">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-158">123</span><span class="sxs-lookup"><span data-stu-id="a6b27-158">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-159">a</span><span class="sxs-lookup"><span data-stu-id="a6b27-159">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="a6b27-160">actuser</span><span class="sxs-lookup"><span data-stu-id="a6b27-160">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="a6b27-161">adm</span><span class="sxs-lookup"><span data-stu-id="a6b27-161">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-162">admin2</span><span class="sxs-lookup"><span data-stu-id="a6b27-162">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-163">aspnet</span><span class="sxs-lookup"><span data-stu-id="a6b27-163">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="a6b27-164">backup</span><span class="sxs-lookup"><span data-stu-id="a6b27-164">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-165">console</span><span class="sxs-lookup"><span data-stu-id="a6b27-165">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-166">david</span><span class="sxs-lookup"><span data-stu-id="a6b27-166">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-167">guest</span><span class="sxs-lookup"><span data-stu-id="a6b27-167">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="a6b27-168">john</span><span class="sxs-lookup"><span data-stu-id="a6b27-168">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-169">владелец</span><span class="sxs-lookup"><span data-stu-id="a6b27-169">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-170">root</span><span class="sxs-lookup"><span data-stu-id="a6b27-170">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-171">server</span><span class="sxs-lookup"><span data-stu-id="a6b27-171">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="a6b27-172">sql</span><span class="sxs-lookup"><span data-stu-id="a6b27-172">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-173">support</span><span class="sxs-lookup"><span data-stu-id="a6b27-173">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-174">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="a6b27-174">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-175">sys</span><span class="sxs-lookup"><span data-stu-id="a6b27-175">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="a6b27-176">test2</span><span class="sxs-lookup"><span data-stu-id="a6b27-176">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-177">test3</span><span class="sxs-lookup"><span data-stu-id="a6b27-177">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-178">user4</span><span class="sxs-lookup"><span data-stu-id="a6b27-178">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="a6b27-179">user5</span><span class="sxs-lookup"><span data-stu-id="a6b27-179">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-the-password-requirements-when-creating-a-vm"></a><span data-ttu-id="a6b27-180">Какие требования к паролю при создании виртуальной машины?</span><span class="sxs-lookup"><span data-stu-id="a6b27-180">What are the password requirements when creating a VM?</span></span>
<span data-ttu-id="a6b27-181">Длина пароля должна быть от 6 до 72 знаков. Также должны удовлетворяться 3 из следующих 4 требований сложности:</span><span class="sxs-lookup"><span data-stu-id="a6b27-181">Passwords must be 6 - 72 characters in length and meet 3 out of the following 4 complexity requirements:</span></span>

* <span data-ttu-id="a6b27-182">используются строчные знаки;</span><span class="sxs-lookup"><span data-stu-id="a6b27-182">Have lower characters</span></span>
* <span data-ttu-id="a6b27-183">используются прописные знаки;</span><span class="sxs-lookup"><span data-stu-id="a6b27-183">Have upper characters</span></span>
* <span data-ttu-id="a6b27-184">используется цифра;</span><span class="sxs-lookup"><span data-stu-id="a6b27-184">Have a digit</span></span>
* <span data-ttu-id="a6b27-185">используется специальный знак (регулярное выражение [\W_]).</span><span class="sxs-lookup"><span data-stu-id="a6b27-185">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="a6b27-186">Не допускаются следующие пароли:</span><span class="sxs-lookup"><span data-stu-id="a6b27-186">The following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="a6b27-187">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="a6b27-187">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="a6b27-188">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="a6b27-188">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="a6b27-189">Password!</span><span class="sxs-lookup"><span data-stu-id="a6b27-189">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="a6b27-190">Password1</span><span class="sxs-lookup"><span data-stu-id="a6b27-190">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="a6b27-191">Password22</span><span class="sxs-lookup"><span data-stu-id="a6b27-191">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="a6b27-192">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="a6b27-192">iloveyou!</span></span></td>
    </tr>
</table>
