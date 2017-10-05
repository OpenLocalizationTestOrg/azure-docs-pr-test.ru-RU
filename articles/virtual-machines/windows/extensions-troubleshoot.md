---
title: "Устранение неполадок расширений виртуальной машины Windows | Документация Майкрософт"
description: "Узнайте об устранении неполадок в работе расширений виртуальной машины Windows в Azure."
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 4dba196e1b838f2092b30972fb070514bd2a4b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="91d58-103">Troubleshooting Azure Windows VM extension failures</span><span class="sxs-lookup"><span data-stu-id="91d58-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="91d58-104">Просмотр состояния расширения</span><span class="sxs-lookup"><span data-stu-id="91d58-104">Viewing extension status</span></span>
<span data-ttu-id="91d58-105">Шаблоны Azure Resource Manager можно выполнять из Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91d58-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="91d58-106">После выполнения шаблона состояние расширения можно узнать в обозревателе ресурсов Azure или с помощью средств командной строки.</span><span class="sxs-lookup"><span data-stu-id="91d58-106">Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.</span></span>

<span data-ttu-id="91d58-107">Пример:</span><span class="sxs-lookup"><span data-stu-id="91d58-107">Here is an example:</span></span>

<span data-ttu-id="91d58-108">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91d58-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="91d58-109">Пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="91d58-109">Here is the sample output:</span></span>

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  <span data-ttu-id="91d58-110">]</span><span class="sxs-lookup"><span data-stu-id="91d58-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="91d58-111">Устранение неполадок расширений</span><span class="sxs-lookup"><span data-stu-id="91d58-111">Troubleshooting extension failures</span></span>
### <a name="re-running-the-extension-on-the-vm"></a><span data-ttu-id="91d58-112">Повторное выполнение расширения на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="91d58-112">Re-running the extension on the VM</span></span>
<span data-ttu-id="91d58-113">При выполнении сценариев на виртуальной машине с помощью расширения пользовательских сценариев может возникать ошибка, указывающая на то, что виртуальная машина создана успешно, но сценарий не выполнен.</span><span class="sxs-lookup"><span data-stu-id="91d58-113">If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed.</span></span> <span data-ttu-id="91d58-114">В этом случае рекомендуется удалить соответствующее расширение и выполнить шаблон еще раз.</span><span class="sxs-lookup"><span data-stu-id="91d58-114">Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.</span></span>
<span data-ttu-id="91d58-115">Примечание. В будущем эта функция будет усовершенствована, что позволит устранить необходимость в удалении расширения.</span><span class="sxs-lookup"><span data-stu-id="91d58-115">Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.</span></span>

#### <a name="remove-the-extension-from-azure-powershell"></a><span data-ttu-id="91d58-116">Удаление расширения с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="91d58-116">Remove the extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="91d58-117">После удаления расширения шаблон можно выполнить повторно, чтобы запустить скрипты на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="91d58-117">Once the extension has been removed, the template can be re-executed to run the scripts on the VM.</span></span>

