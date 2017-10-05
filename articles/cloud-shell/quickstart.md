---
title: "Краткое руководство по Azure Cloud Shell (предварительная версия) | Документация Майкрософт"
description: "Краткое руководство по Azure Cloud Shell"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 75676eb0ab784e2adbfd27b170c1dee5599b74ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-for-using-the-azure-cloud-shell"></a><span data-ttu-id="93d6c-103">Краткое руководство по использованию Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="93d6c-103">Quickstart for using the Azure Cloud Shell</span></span>

<span data-ttu-id="93d6c-104">В этой статье объясняется, как использовать Azure Cloud Shell на [портале Azure](https://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="93d6c-104">This document details how to use the Azure Cloud Shell in the [Azure portal](https://ms.portal.azure.com/).</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="93d6c-105">Запуск Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="93d6c-105">Start Cloud Shell</span></span>
1. <span data-ttu-id="93d6c-106">Запустите **Cloud Shell** в верхней панели навигации портала Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6c-106">Launch **Cloud Shell** from the top navigation of the Azure portal</span></span> <br>
![](media/shell-icon.png)
2. <span data-ttu-id="93d6c-107">Выберите подписку для создания учетной записи хранения и общей папки Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6c-107">Select a subscription to create a storage account and Azure file share</span></span>
3. <span data-ttu-id="93d6c-108">Нажмите кнопку "Создать хранилище".</span><span class="sxs-lookup"><span data-stu-id="93d6c-108">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="93d6c-109">Вы автоматически проходите проверку подлинности для Azure CLI 2.0 в каждом сеансе.</span><span class="sxs-lookup"><span data-stu-id="93d6c-109">You are automatically authenticated for Azure CLI 2.0 in every sesssion.</span></span>

### <a name="set-your-subscription"></a><span data-ttu-id="93d6c-110">Настройка подписки</span><span class="sxs-lookup"><span data-stu-id="93d6c-110">Set your subscription</span></span>
1. <span data-ttu-id="93d6c-111">Выведите список подписок, к которым у вас есть доступ:</span><span class="sxs-lookup"><span data-stu-id="93d6c-111">List subscriptions you have access to:</span></span> <br>
`az account list`
2. <span data-ttu-id="93d6c-112">Задайте предпочитаемую подписку:</span><span class="sxs-lookup"><span data-stu-id="93d6c-112">Set your preferred subscription:</span></span> <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> <span data-ttu-id="93d6c-113">Подписка будет сохранена для последующих сеансов в файле `/home/<user>/.azure/azureProfile.json`.</span><span class="sxs-lookup"><span data-stu-id="93d6c-113">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="93d6c-114">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="93d6c-114">Create a resource group</span></span>
<span data-ttu-id="93d6c-115">Создайте группу ресурсов в WestUS с именем MyRG:</span><span class="sxs-lookup"><span data-stu-id="93d6c-115">Create a new resource group in WestUS named "MyRG":</span></span> <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a><span data-ttu-id="93d6c-116">Создание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="93d6c-116">Create a Linux VM</span></span>
<span data-ttu-id="93d6c-117">Создайте виртуальную машину Ubuntu в новой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="93d6c-117">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="93d6c-118">Azure CLI 2.0 создаст ключи SSH и настроит с их помощью виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="93d6c-118">The Azure CLI 2.0 will create SSH keys and setup the VM with them.</span></span> <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> <span data-ttu-id="93d6c-119">Открытый и закрытый ключи, используемые для проверки подлинности виртуальной машины, помещаются в `/User/.ssh/id_rsa` и `/User/.ssh/id_rsa.pub` с помощью Azure CLI 2.0 по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="93d6c-119">The public and private keys used to authenticate your VM are placed in `/User/.ssh/id_rsa` and `/User/.ssh/id_rsa.pub` by Azure CLI 2.0 by default.</span></span> <span data-ttu-id="93d6c-120">Папка в формате SSH сохраняется в образе размером 5 ГБ, размещенном в подключенной общей папке Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6c-120">Your .ssh folder is persisted in your attached Azure file share's 5-GB image.</span></span>

<span data-ttu-id="93d6c-121">Имя пользователя на этой виртуальной машине будет использоваться в Cloud Shell ($User@Azure:).</span><span class="sxs-lookup"><span data-stu-id="93d6c-121">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="93d6c-122">SSH-подключение к виртуальной машине Linux</span><span class="sxs-lookup"><span data-stu-id="93d6c-122">SSH into your Linux VM</span></span>
1. <span data-ttu-id="93d6c-123">Найдите имя виртуальной машины на панели поиска портала Azure.</span><span class="sxs-lookup"><span data-stu-id="93d6c-123">Search for your VM name in the Azure portal search bar</span></span>
2. <span data-ttu-id="93d6c-124">Щелкните "Подключить" и выполните `ssh username@ipaddress`.</span><span class="sxs-lookup"><span data-stu-id="93d6c-124">Click "Connect" and run: `ssh username@ipaddress`</span></span>

![](media/sshcmd-copy.png)

<span data-ttu-id="93d6c-125">После установки SSH-подключения отобразится строка приветствия Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="93d6c-125">Upon establishing the SSH connection, you should see the Ubuntu welcome prompt.</span></span>
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="93d6c-126">Очистка.</span><span class="sxs-lookup"><span data-stu-id="93d6c-126">Cleaning up</span></span> 
<span data-ttu-id="93d6c-127">Удалите группу ресурсов и все ее ресурсы.</span><span class="sxs-lookup"><span data-stu-id="93d6c-127">Delete your resource group and any resources within it:</span></span> <br>
<span data-ttu-id="93d6c-128">Запустите `az group delete -n MyRG`</span><span class="sxs-lookup"><span data-stu-id="93d6c-128">Run `az group delete -n MyRG`</span></span>

## <a name="next-steps"></a><span data-ttu-id="93d6c-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="93d6c-129">Next Steps</span></span>
[<span data-ttu-id="93d6c-130">Сохранение файлов в Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="93d6c-130">Learn about persisting storage on Cloud Shell</span></span>](persisting-shell-storage.md) <br><span data-ttu-id="93d6c-131">
[Справочник команд Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="93d6c-131">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br><span data-ttu-id="93d6c-132">
[Знакомство с хранилищем файлов Azure](../storage/files/storage-files-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="93d6c-132">
[Learn about Azure File storage](../storage/files/storage-files-introduction.md)</span></span> <br>