---
title: "ошибки расширения виртуальной Машины Windows aaaTroubleshooting | Документы Microsoft"
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
ms.openlocfilehash: d24544743d9e0cb1a68ec9ab7718716f918054f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="5cf28-103">Troubleshooting Azure Windows VM extension failures</span><span class="sxs-lookup"><span data-stu-id="5cf28-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="5cf28-104">Просмотр состояния расширения</span><span class="sxs-lookup"><span data-stu-id="5cf28-104">Viewing extension status</span></span>
<span data-ttu-id="5cf28-105">Шаблоны Azure Resource Manager можно выполнять из Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5cf28-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="5cf28-106">После выполнения шаблона hello состояние расширения hello можно просмотреть с помощью обозревателя ресурсов Azure или hello средств командной строки.</span><span class="sxs-lookup"><span data-stu-id="5cf28-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="5cf28-107">Пример:</span><span class="sxs-lookup"><span data-stu-id="5cf28-107">Here is an example:</span></span>

<span data-ttu-id="5cf28-108">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5cf28-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="5cf28-109">Вот пример выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="5cf28-109">Here is hello sample output:</span></span>

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
  <span data-ttu-id="5cf28-110">]</span><span class="sxs-lookup"><span data-stu-id="5cf28-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="5cf28-111">Устранение неполадок расширений</span><span class="sxs-lookup"><span data-stu-id="5cf28-111">Troubleshooting extension failures</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="5cf28-112">Повторный запуск расширения hello на hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="5cf28-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="5cf28-113">При выполнении скриптов на виртуальной Машине с помощью настраиваемого расширения скриптов hello иногда может запустить произошла ошибка, когда виртуальная машина успешно создана, но hello в сценарии возникла ошибка.</span><span class="sxs-lookup"><span data-stu-id="5cf28-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="5cf28-114">В этих conditons hello, рекомендуется toorecover способом после этой ошибки — расширение tooremove hello и перезапустите процесс hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="5cf28-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="5cf28-115">Примечание: В будущем, эта функция будет улучшенные tooremove hello необходимость удаления расширения hello.</span><span class="sxs-lookup"><span data-stu-id="5cf28-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-powershell"></a><span data-ttu-id="5cf28-116">Удалите расширение hello из Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5cf28-116">Remove hello extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="5cf28-117">После удаления расширения hello hello шаблон может быть повторно выполняется toorun hello сценариев на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5cf28-117">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

