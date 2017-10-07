---
title: "Диагностика aaaBoot для виртуальных машин Linux в Azure | Документ Microsoft"
description: "Обзор возможностей отладки два hello для виртуальных машин Linux в Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="57432-103">Как toouse загрузки виртуальных машин Linux tootroubleshoot диагностики в Azure</span><span class="sxs-lookup"><span data-stu-id="57432-103">How toouse boot diagnostics tootroubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="57432-104">Теперь Azure поддерживает две функции отладки. Виртуальные машины Azure, созданные на основе модели развертывания с помощью Resource Manager, поддерживают выходные данные и снимки экрана консоли.</span><span class="sxs-lookup"><span data-stu-id="57432-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="57432-105">При повторном подключении tooAzure собственного образа или даже загрузки одного из образов платформы hello, может быть несколько причин, почему Возвращает виртуальную машину в состояние не является загрузочным.</span><span class="sxs-lookup"><span data-stu-id="57432-105">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="57432-106">Эти функции позволяют вам tooeasily Диагностика и восстановление сбоев загрузки виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="57432-106">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="57432-107">Для виртуальных машин Linux можно легко просмотреть hello выходные данные журналов консоли из hello портала:</span><span class="sxs-lookup"><span data-stu-id="57432-107">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Портал Azure](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="57432-109">Тем не менее для Windows и Linux виртуальных машин Azure также позволяет toosee снимок экрана приветствия виртуальных Машин из низкоуровневой оболочки hello:</span><span class="sxs-lookup"><span data-stu-id="57432-109">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Ошибка](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="57432-111">Обе эти функции доступны на виртуальных машинах Azure во всех регионах.</span><span class="sxs-lookup"><span data-stu-id="57432-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="57432-112">Обратите внимание, снимки экрана и выходных данных может занять tooappear минут too10 вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="57432-112">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="57432-113">Распространенные ошибки загрузки</span><span class="sxs-lookup"><span data-stu-id="57432-113">Common boot errors</span></span>

- [<span data-ttu-id="57432-114">Проблемы с файловой системой</span><span class="sxs-lookup"><span data-stu-id="57432-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="57432-115">Проблемы с ядром</span><span class="sxs-lookup"><span data-stu-id="57432-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="57432-116">Ошибки FSTAB</span><span class="sxs-lookup"><span data-stu-id="57432-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="57432-117">Включение диагностики на новой виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="57432-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="57432-118">При создании новой виртуальной машины из hello предварительной версии портала выберите hello **диспетчера ресурсов Azure** из раскрывающегося списка модели развертывания hello:</span><span class="sxs-lookup"><span data-stu-id="57432-118">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Диспетчер ресурсов](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="57432-120">Настройте hello мониторинг параметр tooselect hello учетной записи хранилища куда tooplace эти файлы диагностики.</span><span class="sxs-lookup"><span data-stu-id="57432-120">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![Создание виртуальной машины](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="57432-122">При развертывании на основе шаблона Azure Resource Manager перейдите tooyour ресурса виртуальной машины и добавить профиль раздел hello диагностики.</span><span class="sxs-lookup"><span data-stu-id="57432-122">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="57432-123">Не забывайте заголовок версии API «2015-06-15» hello toouse.</span><span class="sxs-lookup"><span data-stu-id="57432-123">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="57432-124">Hello диагностического профиля позволяет учетной записи хранилища hello tooselect место tooput эти журналы.</span><span class="sxs-lookup"><span data-stu-id="57432-124">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="57432-125">Обновление имеющейся виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="57432-125">Update an existing virtual machine</span></span>

<span data-ttu-id="57432-126">Диагностика загрузки tooenable через портал hello, можно также обновить существующую виртуальную машину через портал hello.</span><span class="sxs-lookup"><span data-stu-id="57432-126">tooenable boot diagnostics through hello portal, you can also update an existing virtual machine through hello portal.</span></span> <span data-ttu-id="57432-127">Выберите hello Диагностика загрузки и сохранить.</span><span class="sxs-lookup"><span data-stu-id="57432-127">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="57432-128">Перезапустите эффект tootake hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="57432-128">Restart hello VM tootake effect.</span></span>

![Обновление имеющейся виртуальной машины](./media/boot-diagnostics/screenshot5.png)