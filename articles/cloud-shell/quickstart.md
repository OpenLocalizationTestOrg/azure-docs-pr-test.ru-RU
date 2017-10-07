---
title: "Краткое руководство aaaAzure оболочки облака (Предварительная версия) | Документы Microsoft"
description: "Краткое руководство по hello оболочки облако Azure"
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
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a><span data-ttu-id="717c1-103">Краткое руководство по использованию hello оболочки облако Azure</span><span class="sxs-lookup"><span data-stu-id="717c1-103">Quickstart for using hello Azure Cloud Shell</span></span>

<span data-ttu-id="717c1-104">В этом документе описаны как toouse hello Azure облачной оболочки в hello [портал Azure](https://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="717c1-104">This document details how toouse hello Azure Cloud Shell in hello [Azure portal](https://ms.portal.azure.com/).</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="717c1-105">Запуск Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="717c1-105">Start Cloud Shell</span></span>
1. <span data-ttu-id="717c1-106">Запустите **оболочки облака** hello верхней панели навигации hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="717c1-106">Launch **Cloud Shell** from hello top navigation of hello Azure portal</span></span> <br>
![](media/shell-icon.png)
2. <span data-ttu-id="717c1-107">Выберите подписку toocreate учетной записи хранилища и Azure общей папки</span><span class="sxs-lookup"><span data-stu-id="717c1-107">Select a subscription toocreate a storage account and Azure file share</span></span>
3. <span data-ttu-id="717c1-108">Нажмите кнопку "Создать хранилище".</span><span class="sxs-lookup"><span data-stu-id="717c1-108">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="717c1-109">Вы автоматически проходите проверку подлинности для Azure CLI 2.0 в каждом сеансе.</span><span class="sxs-lookup"><span data-stu-id="717c1-109">You are automatically authenticated for Azure CLI 2.0 in every sesssion.</span></span>

### <a name="set-your-subscription"></a><span data-ttu-id="717c1-110">Настройка подписки</span><span class="sxs-lookup"><span data-stu-id="717c1-110">Set your subscription</span></span>
1. <span data-ttu-id="717c1-111">Выведите список подписок, к которым у вас есть доступ:</span><span class="sxs-lookup"><span data-stu-id="717c1-111">List subscriptions you have access to:</span></span> <br>
`az account list`
2. <span data-ttu-id="717c1-112">Задайте предпочитаемую подписку:</span><span class="sxs-lookup"><span data-stu-id="717c1-112">Set your preferred subscription:</span></span> <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> <span data-ttu-id="717c1-113">Подписка будет сохранена для последующих сеансов в файле `/home/<user>/.azure/azureProfile.json`.</span><span class="sxs-lookup"><span data-stu-id="717c1-113">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="717c1-114">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="717c1-114">Create a resource group</span></span>
<span data-ttu-id="717c1-115">Создайте группу ресурсов в WestUS с именем MyRG:</span><span class="sxs-lookup"><span data-stu-id="717c1-115">Create a new resource group in WestUS named "MyRG":</span></span> <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a><span data-ttu-id="717c1-116">Создание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="717c1-116">Create a Linux VM</span></span>
<span data-ttu-id="717c1-117">Создайте виртуальную машину Ubuntu в новой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="717c1-117">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="717c1-118">Hello Azure CLI 2.0 создаются ключи SSH и hello установки виртуальной Машины с ними.</span><span class="sxs-lookup"><span data-stu-id="717c1-118">hello Azure CLI 2.0 will create SSH keys and setup hello VM with them.</span></span> <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> <span data-ttu-id="717c1-119">Здравствуйте, открытый и закрытый ключи, используемые tooauthenticate ВМ, помещаются в `/User/.ssh/id_rsa` и `/User/.ssh/id_rsa.pub` Azure CLI 2.0 по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="717c1-119">hello public and private keys used tooauthenticate your VM are placed in `/User/.ssh/id_rsa` and `/User/.ssh/id_rsa.pub` by Azure CLI 2.0 by default.</span></span> <span data-ttu-id="717c1-120">Папка в формате SSH сохраняется в образе размером 5 ГБ, размещенном в подключенной общей папке Azure.</span><span class="sxs-lookup"><span data-stu-id="717c1-120">Your .ssh folder is persisted in your attached Azure file share's 5-GB image.</span></span>

<span data-ttu-id="717c1-121">Имя пользователя на этой виртуальной машине будет использоваться в Cloud Shell ($User@Azure:).</span><span class="sxs-lookup"><span data-stu-id="717c1-121">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="717c1-122">SSH-подключение к виртуальной машине Linux</span><span class="sxs-lookup"><span data-stu-id="717c1-122">SSH into your Linux VM</span></span>
1. <span data-ttu-id="717c1-123">Поиск по имени виртуальной Машины в строке поиска Azure портала hello</span><span class="sxs-lookup"><span data-stu-id="717c1-123">Search for your VM name in hello Azure portal search bar</span></span>
2. <span data-ttu-id="717c1-124">Щелкните "Подключить" и выполните `ssh username@ipaddress`.</span><span class="sxs-lookup"><span data-stu-id="717c1-124">Click "Connect" and run: `ssh username@ipaddress`</span></span>

![](media/sshcmd-copy.png)

<span data-ttu-id="717c1-125">После установки подключения SSH hello, вы должны увидеть hello Ubuntu приветствия приглашения.</span><span class="sxs-lookup"><span data-stu-id="717c1-125">Upon establishing hello SSH connection, you should see hello Ubuntu welcome prompt.</span></span>
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="717c1-126">Очистка.</span><span class="sxs-lookup"><span data-stu-id="717c1-126">Cleaning up</span></span> 
<span data-ttu-id="717c1-127">Удалите группу ресурсов и все ее ресурсы.</span><span class="sxs-lookup"><span data-stu-id="717c1-127">Delete your resource group and any resources within it:</span></span> <br>
<span data-ttu-id="717c1-128">Запустите `az group delete -n MyRG`</span><span class="sxs-lookup"><span data-stu-id="717c1-128">Run `az group delete -n MyRG`</span></span>

## <a name="next-steps"></a><span data-ttu-id="717c1-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="717c1-129">Next Steps</span></span>
[<span data-ttu-id="717c1-130">Сохранение файлов в Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="717c1-130">Learn about persisting storage on Cloud Shell</span></span>](persisting-shell-storage.md) <br><span data-ttu-id="717c1-131">
[Справочник команд Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="717c1-131">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br><span data-ttu-id="717c1-132">
[Знакомство с хранилищем файлов Azure](../storage/files/storage-files-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="717c1-132">
[Learn about Azure File storage](../storage/files/storage-files-introduction.md)</span></span> <br>