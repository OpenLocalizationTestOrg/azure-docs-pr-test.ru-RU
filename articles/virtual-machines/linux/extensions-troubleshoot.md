---
title: "Устранение неполадок расширения виртуальной машины Linux | Документация Майкрософт"
description: "Узнайте об устранении неполадок в расширении виртуальной машины Linux в Azure."
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 589890de379d0b729de1f1ba9e604e0ec0496f50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a><span data-ttu-id="932a5-103">Устранение неполадок расширения виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="932a5-103">Troubleshooting Azure Linux VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="932a5-104">Просмотр состояния расширения</span><span class="sxs-lookup"><span data-stu-id="932a5-104">Viewing extension status</span></span>
<span data-ttu-id="932a5-105">Шаблоны Azure Resource Manager можно выполнять из Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="932a5-105">Azure Resource Manager templates can be executed from the  Azure CLI.</span></span> <span data-ttu-id="932a5-106">После выполнения шаблона состояние расширения можно узнать в обозревателе ресурсов Azure или с помощью средств командной строки.</span><span class="sxs-lookup"><span data-stu-id="932a5-106">Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.</span></span>

<span data-ttu-id="932a5-107">Пример:</span><span class="sxs-lookup"><span data-stu-id="932a5-107">Here is an example:</span></span>

<span data-ttu-id="932a5-108">Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="932a5-108">Azure CLI:</span></span>

      azure vm get-instance-view


<span data-ttu-id="932a5-109">Пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="932a5-109">Here is the sample output:</span></span>

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
  <span data-ttu-id="932a5-110">]</span><span class="sxs-lookup"><span data-stu-id="932a5-110">]</span></span>

## <a name="troubleshooting-extenson-failures"></a><span data-ttu-id="932a5-111">Устранение сбоев в расширениях</span><span class="sxs-lookup"><span data-stu-id="932a5-111">Troubleshooting Extenson failures:</span></span>
### <a name="re-running-the-extension-on-the-vm"></a><span data-ttu-id="932a5-112">Повторное выполнение расширения на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="932a5-112">Re-running the extension on the VM</span></span>
<span data-ttu-id="932a5-113">При выполнении сценариев на виртуальной машине с помощью расширения пользовательских сценариев может возникать ошибка, указывающая на то, что виртуальная машина создана успешно, но сценарий не выполнен.</span><span class="sxs-lookup"><span data-stu-id="932a5-113">If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed.</span></span> <span data-ttu-id="932a5-114">В этом случае рекомендуется удалить соответствующее расширение и выполнить шаблон еще раз.</span><span class="sxs-lookup"><span data-stu-id="932a5-114">Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.</span></span>
<span data-ttu-id="932a5-115">Примечание. В будущем эта функция будет усовершенствована, что позволит устранить необходимость в удалении расширения.</span><span class="sxs-lookup"><span data-stu-id="932a5-115">Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.</span></span>

#### <a name="remove-the-extension-from-azure-cli"></a><span data-ttu-id="932a5-116">Удаление расширения с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="932a5-116">Remove the extension from Azure CLI</span></span>
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

<span data-ttu-id="932a5-117">В данном коде publisher-name соответствует типу расширения из выходных данных azure vm get-instance-view, а имя представляет собой имя ресурса расширения из шаблона.</span><span class="sxs-lookup"><span data-stu-id="932a5-117">Where "publsher-name" corresponds to the extension type from the output of "azure vm get-instance-view" and name is the name of the extension resource from the template</span></span>

<span data-ttu-id="932a5-118">После удаления расширения шаблон можно выполнить повторно, чтобы запустить скрипты на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="932a5-118">Once the extension has been removed, the template can be re-executed to run the scripts on the VM.</span></span>

