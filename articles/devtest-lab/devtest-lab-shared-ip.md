---
title: "Общие IP-адреса в Azure DevTest Labs | Документация Майкрософт"
description: "Узнайте, как с помощью общих IP-адресов в Azure DevTest Labs минимизировать количество общедоступных IP-адресов, необходимых для доступа к виртуальным машинам лаборатории."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 9f6e1980bf5ea5b41da98a135d89f1c5159921a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="8d92b-103">Общие IP-адреса в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8d92b-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="8d92b-104">Azure DevTest Labs позволяет виртуальным машинам лаборатории совместно использовать тот же общедоступный IP-адрес, чтобы минимизировать количество общедоступных IP-адресов, необходимых для доступа к отдельным виртуальным машинам лаборатории.</span><span class="sxs-lookup"><span data-stu-id="8d92b-104">Azure DevTest Labs lets lab VMs share the same public IP address to minimize the number of public IP addresses required to access your individual lab VMs.</span></span>  <span data-ttu-id="8d92b-105">В этой статье описывается принцип работы общих IP-адресов и варианты их настройки.</span><span class="sxs-lookup"><span data-stu-id="8d92b-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="8d92b-106">Настройка общих IP-адресов</span><span class="sxs-lookup"><span data-stu-id="8d92b-106">Shared IP setting</span></span>

<span data-ttu-id="8d92b-107">Когда создается лаборатория, она размещается в подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="8d92b-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="8d92b-108">При создании этой подсети параметру **Enable shared public IP** (Включить совместное использование общедоступного IP-адреса) по умолчанию задается значение *Yes* (Да).</span><span class="sxs-lookup"><span data-stu-id="8d92b-108">By default, this subnet is created with **Enable shared public IP** set to *Yes*.</span></span>  <span data-ttu-id="8d92b-109">При такой конфигурации создается общедоступный IP-адрес для всей подсети.</span><span class="sxs-lookup"><span data-stu-id="8d92b-109">This configuration creates one public IP address for the entire subnet.</span></span>  <span data-ttu-id="8d92b-110">Дополнительные сведения о настройке виртуальных сетей и подсетей см. в статье [Настройка виртуальной сети в Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="8d92b-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Создание подсети лаборатории](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="8d92b-112">Вы можете включить этот параметр для всех имеющихся лабораторий, выбрав **Configuration and Policies (Конфигурация и политики) > Virtual Networks (Виртуальные сети)**.</span><span class="sxs-lookup"><span data-stu-id="8d92b-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="8d92b-113">Затем выберите виртуальную сеть из списка и выберите **ENABLE SHARED PUBLIC IP** (Включить совместное использование общедоступного IP-адреса) для выбранной подсети.</span><span class="sxs-lookup"><span data-stu-id="8d92b-113">Then, select a virtual network from the list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="8d92b-114">Этот параметр можно отключить в любой лаборатории, если вы не хотите совместно использовать общедоступные IP-адреса на виртуальных машинах лаборатории.</span><span class="sxs-lookup"><span data-stu-id="8d92b-114">You can also disable this option in any lab if you don't want to share a public IP address across lab VMs.</span></span>

<span data-ttu-id="8d92b-115">На всех виртуальных машинах, созданных в этой лаборатории, по умолчанию используется общий IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="8d92b-115">Any VMs created in this lab default to using a shared IP.</span></span>  <span data-ttu-id="8d92b-116">При создании виртуальной машины этот параметр отображается в колонке **Дополнительные параметры** в разделе **Настройка IP-адреса**.</span><span class="sxs-lookup"><span data-stu-id="8d92b-116">When creating the VM, this setting can be observed in the **Advanced settings** blade under **IP address configuration**.</span></span>

![Создание виртуальной машины](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="8d92b-118">**Общий.** Все виртуальные машины, созданные в качестве **общедоступных**, помещаются в одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8d92b-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="8d92b-119">Этой группе ресурсов назначается отдельный IP-адрес, который будут использовать все виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="8d92b-119">A single IP address is assigned for that RG and all VMs in the RG will use that IP address.</span></span>
- <span data-ttu-id="8d92b-120">**Общедоступный.** Каждая созданная виртуальная машина имеет личный IP-адрес и создается в собственной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8d92b-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="8d92b-121">**Частный.** Каждая созданная виртуальная машина использует частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="8d92b-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="8d92b-122">Вы не сможете подключиться к этой виртуальной машины напрямую из Интернета с помощью удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="8d92b-122">You will not be able to connect to this VM directly from the internet with Remote Desktop.</span></span>

<span data-ttu-id="8d92b-123">Когда в подсеть добавляется виртуальная машина с включенным общим IP-адресом, DevTest Labs автоматически добавляет виртуальную машину в подсистему балансировки нагрузки и назначает номер TCP-порта общедоступному IP-адресу, который выполняет переадресацию на порт RDP на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="8d92b-123">Whenever a VM with shared IP enabled is added to the subnet, DevTest Labs automatically adds the VM to a load balancer and assigns a TCP port number on the public IP address, forwarding to the RDP port on the VM.</span></span>  

## <a name="using-the-shared-ip"></a><span data-ttu-id="8d92b-124">Использование общего IP-адреса</span><span class="sxs-lookup"><span data-stu-id="8d92b-124">Using the shared IP</span></span>

- <span data-ttu-id="8d92b-125">**Пользователи Linux.** Чтобы подключиться к виртуальной машине по протоколу SSH, введите IP-адрес или полное доменное имя, затем поставьте двоеточие и укажите номер порта.</span><span class="sxs-lookup"><span data-stu-id="8d92b-125">**Linux users:** SSH to the VM by using the IP address or fully qualified domain name, followed by a colon, followed by the port.</span></span> <span data-ttu-id="8d92b-126">Например, на приведенном ниже рисунке таким адресом RDP для подключения к виртуальной машине является `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="8d92b-126">For example, in the image below, the RDP address to connect to the VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![Пример виртуальной машины](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="8d92b-128">**Пользователи Windows.** Нажмите кнопку **Подключить** на портале Azure, чтобы скачать предварительно настроенный RDP-файл и получить доступ к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="8d92b-128">**Windows users:** Select the **Connect** button on the Azure portal to download a pre-configured RDP file and access the VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d92b-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8d92b-129">Next steps</span></span>

* [<span data-ttu-id="8d92b-130">Управление всеми политиками лаборатории в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8d92b-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="8d92b-131">Настройка виртуальной сети в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8d92b-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





