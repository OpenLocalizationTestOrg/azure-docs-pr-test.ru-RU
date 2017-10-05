---
title: "Диагностика загрузки виртуальных машин Linux в Azure | Документы Майкрософт"
description: "Общие сведения о двух функциях отладки для виртуальных машин Linux в Azure"
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
ms.openlocfilehash: 70254d39b5c6326166f7e29fdfc99533835502f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-boot-diagnostics-to-troubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="9e9f6-103">Использование диагностики загрузки для устранения неполадок виртуальных машин Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="9e9f6-103">How to use boot diagnostics to troubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="9e9f6-104">Теперь Azure поддерживает две функции отладки. Виртуальные машины Azure, созданные на основе модели развертывания с помощью Resource Manager, поддерживают выходные данные и снимки экрана консоли.</span><span class="sxs-lookup"><span data-stu-id="9e9f6-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="9e9f6-105">При передаче собственного образа в Azure или даже при загрузке одного из образов платформ могут возникать проблемы с загрузкой виртуальной машины. Это может происходить по разным причинам.</span><span class="sxs-lookup"><span data-stu-id="9e9f6-105">When bringing your own image to Azure or even booting one of the platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="9e9f6-106">Новые функции позволяют легко диагностировать и восстанавливать виртуальную машину после сбоев загрузки.</span><span class="sxs-lookup"><span data-stu-id="9e9f6-106">These features enable you to easily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="9e9f6-107">На виртуальных машинах Linux выходные данные журнала консоли можно легко просмотреть на портале:</span><span class="sxs-lookup"><span data-stu-id="9e9f6-107">For Linux Virtual Machines, you can easily view the output of your console log from the Portal:</span></span>

![Портал Azure](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="9e9f6-109">Но Azure также позволяет просматривать снимки экранов виртуальных машин Windows и Linux из гипервизора:</span><span class="sxs-lookup"><span data-stu-id="9e9f6-109">However, for both Windows and Linux Virtual Machines, Azure also enables you to see a screenshot of the VM from the hypervisor:</span></span>

![Ошибка](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="9e9f6-111">Обе эти функции доступны на виртуальных машинах Azure во всех регионах.</span><span class="sxs-lookup"><span data-stu-id="9e9f6-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="9e9f6-112">Обратите внимание, что отображение снимков экрана и выходных данных в учетной записи хранения может занять до 10 минут.</span><span class="sxs-lookup"><span data-stu-id="9e9f6-112">Note, screenshots, and output can take up to 10 minutes to appear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="9e9f6-113">Распространенные ошибки загрузки</span><span class="sxs-lookup"><span data-stu-id="9e9f6-113">Common boot errors</span></span>

- [<span data-ttu-id="9e9f6-114">Проблемы с файловой системой</span><span class="sxs-lookup"><span data-stu-id="9e9f6-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="9e9f6-115">Проблемы с ядром</span><span class="sxs-lookup"><span data-stu-id="9e9f6-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="9e9f6-116">Ошибки FSTAB</span><span class="sxs-lookup"><span data-stu-id="9e9f6-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="9e9f6-117">Включение диагностики на новой виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="9e9f6-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="9e9f6-118">При создании виртуальной машины на портале предварительной версии в раскрывающемся списке выбора модели развертывания выберите **Azure Resource Manager**:</span><span class="sxs-lookup"><span data-stu-id="9e9f6-118">When creating a new Virtual Machine from the Preview Portal, select the **Azure Resource Manager** from the deployment model dropdown:</span></span>
 
    ![Диспетчер ресурсов](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="9e9f6-120">Настройте параметр "Мониторинг", указав учетную запись хранения, в которую вы хотели бы поместить эти файлы диагностики.</span><span class="sxs-lookup"><span data-stu-id="9e9f6-120">Configure the Monitoring option to select the storage account where you would like to place these diagnostic files.</span></span>
 
    ![Создание виртуальной машины](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="9e9f6-122">При развертывании на основе шаблона Azure Resource Manager перейдите к ресурсу виртуальной машины и добавьте раздел профиля диагностики.</span><span class="sxs-lookup"><span data-stu-id="9e9f6-122">If you are deploying from an Azure Resource Manager template, navigate to your Virtual Machine resource and append the diagnostics profile section.</span></span> <span data-ttu-id="9e9f6-123">Не забудьте добавить заголовок версии API 2015-06-15.</span><span class="sxs-lookup"><span data-stu-id="9e9f6-123">Remember to use the “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="9e9f6-124">Профиль диагностики позволяет выбрать учетную запись хранения, в которую нужно поместить эти журналы.</span><span class="sxs-lookup"><span data-stu-id="9e9f6-124">The diagnostics profile enables you to select the storage account where you want to put these logs.</span></span>

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

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="9e9f6-125">Обновление имеющейся виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="9e9f6-125">Update an existing virtual machine</span></span>

<span data-ttu-id="9e9f6-126">Диагностику загрузки можно также включить на портале. Для этого обновите на портале имеющуюся виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="9e9f6-126">To enable boot diagnostics through the portal, you can also update an existing virtual machine through the portal.</span></span> <span data-ttu-id="9e9f6-127">Установите флажок "Диагностика загрузки" и нажмите кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="9e9f6-127">Select the Boot Diagnostics option and Save.</span></span> <span data-ttu-id="9e9f6-128">Чтобы изменения вступили в силу, перезапустите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="9e9f6-128">Restart the VM to take effect.</span></span>

![Обновление имеющейся виртуальной машины](./media/boot-diagnostics/screenshot5.png)