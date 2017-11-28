---
title: "aaaDesired состояние конфигурации диспетчера ресурсов шаблона | Документы Microsoft"
description: "Определение шаблона Resource Manager для Desired State Configuration, а также примеры и сведения об устранении проблем."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: b5402e5a-1768-4075-8c19-b7f7402687af
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: fc47ac149b1179d9305797eaa8ed8a83c0958c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="1c513-103">Настройка масштабируемых наборов виртуальных машин Windows и Desired State Configuration с помощью шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1c513-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="1c513-104">В этой статье описывается hello шаблона диспетчера ресурсов для hello [обработчик расширений для настройки требуемого состояния](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c513-104">This article describes hello Resource Manager template for hello [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="1c513-105">Пример шаблона для виртуальной машины Windows</span><span class="sxs-lookup"><span data-stu-id="1c513-105">Template example for a Windows VM</span></span>
<span data-ttu-id="1c513-106">Hello следующий фрагмент переходит в раздел ресурсов шаблона hello hello.</span><span class="sxs-lookup"><span data-stu-id="1c513-106">hello following snippet goes into hello Resource section of hello template.</span></span>

```json
            "name": "Microsoft.Powershell.DSC",
            "type": "extensions",
             "location": "[resourceGroup().location]",
             "apiVersion": "2015-06-15",
             "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "dscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }

```

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="1c513-107">Пример шаблона для масштабируемых наборов виртуальных машин Windows</span><span class="sxs-lookup"><span data-stu-id="1c513-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="1c513-108">На узле VMSS имеется раздел «свойства» с hello «VirtualMachineProfile» атрибута «extensionProfile».</span><span class="sxs-lookup"><span data-stu-id="1c513-108">A VMSS node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="1c513-109">Атрибут DSC находится в разделе extensions.</span><span class="sxs-lookup"><span data-stu-id="1c513-109">DSC is added under "extensions".</span></span> 

```json
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": true,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
        }
```

## <a name="detailed-settings-information"></a><span data-ttu-id="1c513-110">Подробные сведения о разделе settings</span><span class="sxs-lookup"><span data-stu-id="1c513-110">Detailed Settings Information</span></span>
<span data-ttu-id="1c513-111">Hello следующая схема представляет часть параметров hello hello расширение Azure DSC в шаблоне диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="1c513-111">hello following schema is for hello settings portion of hello Azure DSC extension in an Azure Resource Manager template.</span></span>

```json

"settings": {
  "wmfVersion": "latest",
  "configuration": {
    "url": "http://validURLToConfigLocation",
    "script": "ConfigurationScript.ps1",
    "function": "ConfigurationFunction"
  },
  "configurationArguments": {
    "argument1": "Value1",
    "argument2": "Value2"
  },
  "configurationData": {
    "url": "https://foo.psd1"
  },
  "privacy": {
    "dataCollection": "enable"
  },
  "advancedOptions": {
    "downloadMappings": {
      "customWmfLocation": "http://myWMFlocation"
    }
  } 
},
"protectedSettings": {
  "configurationArguments": {
    "parameterOfTypePSCredential1": {
      "userName": "UsernameValue1",
      "password": "PasswordValue1"
    },
    "parameterOfTypePSCredential2": {
      "userName": "UsernameValue2",
      "password": "PasswordValue2"
    }
  },
  "configurationUrlSasToken": "?g!bber1sht0k3n",
  "configurationDataUrlSasToken": "?dataAcC355T0k3N"
}

```

## <a name="details"></a><span data-ttu-id="1c513-112">Сведения</span><span class="sxs-lookup"><span data-stu-id="1c513-112">Details</span></span>
| <span data-ttu-id="1c513-113">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="1c513-113">Property Name</span></span> | <span data-ttu-id="1c513-114">Тип</span><span class="sxs-lookup"><span data-stu-id="1c513-114">Type</span></span> | <span data-ttu-id="1c513-115">Описание</span><span class="sxs-lookup"><span data-stu-id="1c513-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1c513-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="1c513-116">settings.wmfVersion</span></span> |<span data-ttu-id="1c513-117">string</span><span class="sxs-lookup"><span data-stu-id="1c513-117">string</span></span> |<span data-ttu-id="1c513-118">Указывает версию hello hello Windows Management Framework, который должен быть установлен на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="1c513-118">Specifies hello version of hello Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="1c513-119">Задание этого свойства too'latest "устанавливает hello WMF в более новую версию.</span><span class="sxs-lookup"><span data-stu-id="1c513-119">Setting this property too'latest' installs hello most updated version of WMF.</span></span> <span data-ttu-id="1c513-120">только текущий Hello допустимые значения для этого свойства — **«4.0", «5.0", "5.0PP' и «последняя»**.</span><span class="sxs-lookup"><span data-stu-id="1c513-120">hello only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="1c513-121">Эти возможные значения: tooupdates субъекта.</span><span class="sxs-lookup"><span data-stu-id="1c513-121">These possible values are subject tooupdates.</span></span> <span data-ttu-id="1c513-122">значение по умолчанию Hello «последняя».</span><span class="sxs-lookup"><span data-stu-id="1c513-122">hello default value is 'latest'.</span></span> |
| <span data-ttu-id="1c513-123">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="1c513-123">settings.configuration.url</span></span> |<span data-ttu-id="1c513-124">string</span><span class="sxs-lookup"><span data-stu-id="1c513-124">string</span></span> |<span data-ttu-id="1c513-125">Указывает URL-адрес расположения hello из какой toodownload ZIP-файл конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="1c513-125">Specifies hello URL location from which toodownload your DSC configuration zip file.</span></span> <span data-ttu-id="1c513-126">Если указан URL-адрес hello требуется маркер SAS для доступа, необходимо tooset hello protectedSettings.configurationUrlSasToken toohello значение свойства токен SAS.</span><span class="sxs-lookup"><span data-stu-id="1c513-126">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationUrlSasToken property toohello value of your SAS token.</span></span> <span data-ttu-id="1c513-127">Это свойство обязательное, если заданы свойства settings.configuration.script и (или) settings.configuration.function.</span><span class="sxs-lookup"><span data-stu-id="1c513-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="1c513-128">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="1c513-128">settings.configuration.script</span></span> |<span data-ttu-id="1c513-129">string</span><span class="sxs-lookup"><span data-stu-id="1c513-129">string</span></span> |<span data-ttu-id="1c513-130">Указывает имя файла hello hello скрипт, содержащий определение hello конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="1c513-130">Specifies hello file name of hello script that contains hello definition of your DSC configuration.</span></span> <span data-ttu-id="1c513-131">Этот скрипт должен быть в корневой папке hello hello ZIP-файле, загружаются из hello URL-адреса, указанного в свойстве configuration.url hello.</span><span class="sxs-lookup"><span data-stu-id="1c513-131">This script must be in hello root folder of hello zip file downloaded from hello URL specified by hello configuration.url property.</span></span> <span data-ttu-id="1c513-132">Это свойство обязательное, если заданы свойства settings.configuration.url и (или) settings.configuration.script.</span><span class="sxs-lookup"><span data-stu-id="1c513-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="1c513-133">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="1c513-133">settings.configuration.function</span></span> |<span data-ttu-id="1c513-134">string</span><span class="sxs-lookup"><span data-stu-id="1c513-134">string</span></span> |<span data-ttu-id="1c513-135">Указывает имя конфигурации DSC hello.</span><span class="sxs-lookup"><span data-stu-id="1c513-135">Specifies hello name of your DSC configuration.</span></span> <span data-ttu-id="1c513-136">Hello конфигурации с именем должны содержаться в скрипте hello определяется configuration.script.</span><span class="sxs-lookup"><span data-stu-id="1c513-136">hello configuration named must be contained in hello script defined by configuration.script.</span></span> <span data-ttu-id="1c513-137">Это свойство обязательное, если заданы свойства settings.configuration.url и (или) settings.configuration.function.</span><span class="sxs-lookup"><span data-stu-id="1c513-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="1c513-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="1c513-138">settings.configurationArguments</span></span> |<span data-ttu-id="1c513-139">Коллекция</span><span class="sxs-lookup"><span data-stu-id="1c513-139">Collection</span></span> |<span data-ttu-id="1c513-140">Определяет любые параметры, которые вы хотите конфигурации DSC tooyour toopass.</span><span class="sxs-lookup"><span data-stu-id="1c513-140">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="1c513-141">Это свойство не зашифровано.</span><span class="sxs-lookup"><span data-stu-id="1c513-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="1c513-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="1c513-142">settings.configurationData.url</span></span> |<span data-ttu-id="1c513-143">string</span><span class="sxs-lookup"><span data-stu-id="1c513-143">string</span></span> |<span data-ttu-id="1c513-144">Указывает URL-адрес hello, из которого toodownload данные конфигурации (.psd1) файла toouse как входные параметры для конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="1c513-144">Specifies hello URL from which toodownload your configuration data (.psd1) file toouse as input for your DSC configuration.</span></span> <span data-ttu-id="1c513-145">Если указан URL-адрес hello требуется маркер SAS для доступа, необходимо tooset hello protectedSettings.configurationDataUrlSasToken toohello значение свойства токен SAS.</span><span class="sxs-lookup"><span data-stu-id="1c513-145">If hello URL provided requires a SAS token for access, you need tooset hello protectedSettings.configurationDataUrlSasToken property toohello value of your SAS token.</span></span> |
| <span data-ttu-id="1c513-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="1c513-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="1c513-147">string</span><span class="sxs-lookup"><span data-stu-id="1c513-147">string</span></span> |<span data-ttu-id="1c513-148">Включает или отключает сбор данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="1c513-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="1c513-149">Hello только допустимые значения для этого свойства — **«Включить», «Отключить», ", или $null**.</span><span class="sxs-lookup"><span data-stu-id="1c513-149">hello only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="1c513-150">Если для этого свойства не задано значение или задано значение null, сбор данных телеметрии будет выполняться.</span><span class="sxs-lookup"><span data-stu-id="1c513-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="1c513-151">значение по умолчанию Hello — ''.</span><span class="sxs-lookup"><span data-stu-id="1c513-151">hello default value is ''.</span></span> [<span data-ttu-id="1c513-152">Дополнительные сведения см. здесь.</span><span class="sxs-lookup"><span data-stu-id="1c513-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="1c513-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="1c513-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="1c513-154">Коллекция</span><span class="sxs-lookup"><span data-stu-id="1c513-154">Collection</span></span> |<span data-ttu-id="1c513-155">Определяет альтернативного расположения, из которого toodownload hello WMF.</span><span class="sxs-lookup"><span data-stu-id="1c513-155">Defines alternate locations from which toodownload hello WMF.</span></span> [<span data-ttu-id="1c513-156">Дополнительные сведения см. здесь.</span><span class="sxs-lookup"><span data-stu-id="1c513-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="1c513-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="1c513-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="1c513-158">Коллекция</span><span class="sxs-lookup"><span data-stu-id="1c513-158">Collection</span></span> |<span data-ttu-id="1c513-159">Определяет любые параметры, которые вы хотите конфигурации DSC tooyour toopass.</span><span class="sxs-lookup"><span data-stu-id="1c513-159">Defines any parameters you would like toopass tooyour DSC configuration.</span></span> <span data-ttu-id="1c513-160">Это свойство зашифровано.</span><span class="sxs-lookup"><span data-stu-id="1c513-160">This property is encrypted.</span></span> |
| <span data-ttu-id="1c513-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="1c513-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="1c513-162">string</span><span class="sxs-lookup"><span data-stu-id="1c513-162">string</span></span> |<span data-ttu-id="1c513-163">Указывает hello маркера tooaccess hello URL-адрес SAS определяется configuration.url.</span><span class="sxs-lookup"><span data-stu-id="1c513-163">Specifies hello SAS token tooaccess hello URL defined by configuration.url.</span></span> <span data-ttu-id="1c513-164">Это свойство зашифровано.</span><span class="sxs-lookup"><span data-stu-id="1c513-164">This property is encrypted.</span></span> |
| <span data-ttu-id="1c513-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="1c513-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="1c513-166">string</span><span class="sxs-lookup"><span data-stu-id="1c513-166">string</span></span> |<span data-ttu-id="1c513-167">Указывает hello маркера tooaccess hello URL-адрес SAS определяется configurationData.url.</span><span class="sxs-lookup"><span data-stu-id="1c513-167">Specifies hello SAS token tooaccess hello URL defined by configurationData.url.</span></span> <span data-ttu-id="1c513-168">Это свойство зашифровано.</span><span class="sxs-lookup"><span data-stu-id="1c513-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="1c513-169">Сравнение разделов settings и protectedSettings</span><span class="sxs-lookup"><span data-stu-id="1c513-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="1c513-170">Все параметры сохраняются в текстовый файл параметров на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1c513-170">All settings are saved in a settings text file on hello VM.</span></span>
<span data-ttu-id="1c513-171">Свойства в разделе «параметры» являются открытые свойства, поскольку не шифруются в текстовом файле параметров hello.</span><span class="sxs-lookup"><span data-stu-id="1c513-171">Properties under 'settings' are public properties because they are not encrypted in hello settings text file.</span></span>
<span data-ttu-id="1c513-172">Свойства в разделе «protectedSettings» шифруются с помощью сертификата и не отображаются в виде обычного текста в этот файл на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1c513-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on hello VM.</span></span>

<span data-ttu-id="1c513-173">Hello конфигурации необходимы учетные данные, они могут быть включены в protectedSettings:</span><span class="sxs-lookup"><span data-stu-id="1c513-173">If hello configuration needs credentials, they can be included in protectedSettings:</span></span>

```json
"protectedSettings": {
    "configurationArguments": {
        "parameterOfTypePSCredential1": {
               "userName": "UsernameValue1",
               "password": "PasswordValue1"
        }
    }
}
```

## <a name="example"></a><span data-ttu-id="1c513-174">Пример</span><span class="sxs-lookup"><span data-stu-id="1c513-174">Example</span></span>
<span data-ttu-id="1c513-175">Hello в примере является производным из раздела «Начало работы» hello hello [страница обзора обработчик расширения DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c513-175">hello following example derives from hello "Getting Started" section of hello [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="1c513-176">Этот пример использует шаблоны диспетчера ресурсов вместо расширения hello toodeploy командлетов.</span><span class="sxs-lookup"><span data-stu-id="1c513-176">This example uses Resource Manager templates instead of cmdlets toodeploy hello extension.</span></span> <span data-ttu-id="1c513-177">Сохранить конфигурацию «IisInstall.ps1» hello, размещения в ней. ZIP-файл и файл hello передачи в URL-адрес доступен.</span><span class="sxs-lookup"><span data-stu-id="1c513-177">Save hello "IisInstall.ps1" configuration, place it in a .ZIP file, and upload hello file in an accessible URL.</span></span> <span data-ttu-id="1c513-178">В этом примере используется хранилище больших двоичных объектов, но это возможно toodownload. ZIP-файлы из любого произвольного места.</span><span class="sxs-lookup"><span data-stu-id="1c513-178">This example uses Azure blob storage, but it is possible toodownload .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="1c513-179">Hello шаблона диспетчера ресурсов Azure hello следующий код дает правильный файл toodownload ВМ hello hello и выполните соответствующую функцию PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="1c513-179">In hello Azure Resource Manager template, hello following code instructs hello VM toodownload hello correct file and run hello appropriate PowerShell function:</span></span>

```json
"settings": {
    "configuration": {
        "url": "https://demo.blob.core.windows.net/",
        "script": "IisInstall.ps1",
        "function": "IISInstall"
    }
    } 
},
"protectedSettings": {
    "configurationUrlSasToken": "odLPL/U1p9lvcnp..."
}
```

## <a name="updating-from-hello-previous-format"></a><span data-ttu-id="1c513-180">Обновление из предыдущего формата hello</span><span class="sxs-lookup"><span data-stu-id="1c513-180">Updating from hello Previous Format</span></span>
<span data-ttu-id="1c513-181">Все параметры в hello предыдущего формата (содержащий hello открытые свойства ModulesUrl, ConfigurationFunction, SasToken или свойства) автоматически адаптировать toohello текущий формат и выполнять так же, как раньше.</span><span class="sxs-lookup"><span data-stu-id="1c513-181">Any settings in hello previous format (containing hello public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt toohello current format and run just as they did before.</span></span>

<span data-ttu-id="1c513-182">Следующая схема Hello является hello предыдущие параметры схемы выглядела:</span><span class="sxs-lookup"><span data-stu-id="1c513-182">hello following schema is what hello previous settings schema looked like:</span></span>

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points tooprivate Azure Blob Storage",
    "ConfigurationFunction": "ConfigurationScript.ps1\\ConfigurationFunction",
    "Properties":  {
        "ParameterToConfigurationFunction1":  "Value1",
        "ParameterToConfigurationFunction2":  "Value2",
        "ParameterOfTypePSCredential1": {
            "UserName": "UsernameValue1",
            "Password": "PrivateSettingsRef:Key1" 
        },
        "ParameterOfTypePSCredential2": {
            "UserName": "UsernameValue2",
            "Password": "PrivateSettingsRef:Key2"
        }
    }
},
"protectedSettings": { 
    "Items": {
        "Key1": "PasswordValue1",
        "Key2": "PasswordValue2"
    },
    "DataBlobUri": "https://UrlToConfigurationDataWithOptionalSasToken.psd1"
}
```

<span data-ttu-id="1c513-183">Вот, как старый формат hello адаптирует toohello текущего формата.</span><span class="sxs-lookup"><span data-stu-id="1c513-183">Here's how hello previous format adapts toohello current format:</span></span>

| <span data-ttu-id="1c513-184">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="1c513-184">Property Name</span></span> | <span data-ttu-id="1c513-185">Предыдущий эквивалент</span><span class="sxs-lookup"><span data-stu-id="1c513-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="1c513-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="1c513-186">settings.wmfVersion</span></span> |<span data-ttu-id="1c513-187">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="1c513-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="1c513-188">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="1c513-188">settings.configuration.url</span></span> |<span data-ttu-id="1c513-189">settings.ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="1c513-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="1c513-190">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="1c513-190">settings.configuration.script</span></span> |<span data-ttu-id="1c513-191">Первая часть свойства settings.ConfigurationFunction (перед \\\\).</span><span class="sxs-lookup"><span data-stu-id="1c513-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="1c513-192">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="1c513-192">settings.configuration.function</span></span> |<span data-ttu-id="1c513-193">Вторая часть свойства settings.ConfigurationFunction (после \\\\).</span><span class="sxs-lookup"><span data-stu-id="1c513-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="1c513-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="1c513-194">settings.configurationArguments</span></span> |<span data-ttu-id="1c513-195">settings.Properties</span><span class="sxs-lookup"><span data-stu-id="1c513-195">settings.Properties</span></span> |
| <span data-ttu-id="1c513-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="1c513-196">settings.configurationData.url</span></span> |<span data-ttu-id="1c513-197">protectedSettings.DataBlobUri (без маркера SAS)</span><span class="sxs-lookup"><span data-stu-id="1c513-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="1c513-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="1c513-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="1c513-199">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="1c513-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="1c513-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="1c513-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="1c513-201">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="1c513-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="1c513-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="1c513-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="1c513-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="1c513-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="1c513-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="1c513-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="1c513-205">settings.SasToken</span><span class="sxs-lookup"><span data-stu-id="1c513-205">settings.SasToken</span></span> |
| <span data-ttu-id="1c513-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="1c513-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="1c513-207">Маркер SAS из свойства protectedSettings.DataBlobUri</span><span class="sxs-lookup"><span data-stu-id="1c513-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="1c513-208">Устранение неполадок — код ошибки 1100</span><span class="sxs-lookup"><span data-stu-id="1c513-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="1c513-209">Код ошибки 1100 указывает на проблему с hello расширения toohello DSC ввод данных пользователем.</span><span class="sxs-lookup"><span data-stu-id="1c513-209">Error Code 1100 indicates that there is a problem with hello user input toohello DSC extension.</span></span>
<span data-ttu-id="1c513-210">текст Hello этих ошибок является переменной и может измениться.</span><span class="sxs-lookup"><span data-stu-id="1c513-210">hello text of these errors is variable and may change.</span></span>
<span data-ttu-id="1c513-211">Ниже приведены некоторые ошибки hello, с которыми вы можете столкнуться, и способах их устранения.</span><span class="sxs-lookup"><span data-stu-id="1c513-211">Here are some of hello errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="1c513-212">Недопустимые значения</span><span class="sxs-lookup"><span data-stu-id="1c513-212">Invalid Values</span></span>
<span data-ttu-id="1c513-213">"Privacy.dataCollection is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="1c513-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="1c513-214">Hello только допустимые значения: «, «Включить» и «Отключить»» «является WmfVersion «{0}».</span><span class="sxs-lookup"><span data-stu-id="1c513-214">hello only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="1c513-215">Возможные значения: …</span><span class="sxs-lookup"><span data-stu-id="1c513-215">Only possible values are …</span></span> <span data-ttu-id="1c513-216">и latest.</span><span class="sxs-lookup"><span data-stu-id="1c513-216">and 'latest'"</span></span>

<span data-ttu-id="1c513-217">Проблема. Указано неразрешенное значение.</span><span class="sxs-lookup"><span data-stu-id="1c513-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="1c513-218">Решение: Изменение hello недопустимое значение tooa допустимое значение.</span><span class="sxs-lookup"><span data-stu-id="1c513-218">Solution: Change hello invalid value tooa valid value.</span></span> <span data-ttu-id="1c513-219">См. таблицу hello в разделе "Сведения" hello.</span><span class="sxs-lookup"><span data-stu-id="1c513-219">See hello table in hello Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="1c513-220">Недопустимый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="1c513-220">Invalid URL</span></span>
<span data-ttu-id="1c513-221">"ConfigurationData.url is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="1c513-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="1c513-222">This is not a valid URL" (Значение свойства configurationData.url — "{0}". Это недопустимый URL-адрес). "DataBlobUri is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="1c513-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="1c513-223">This is not a valid URL" (Значение свойства DataBlobUri — "{0}". Это недопустимый URL-адрес). "Configuration.url is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="1c513-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="1c513-224">This is not a valid URL" (Значение свойства Configuration.url — "{0}". Это недопустимый URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="1c513-224">This is not a valid URL"</span></span>

<span data-ttu-id="1c513-225">Проблема. Указан недопустимый URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="1c513-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="1c513-226">Решение. Проверьте все указанные URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="1c513-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="1c513-227">Убедитесь, что все URL-адреса разрешения toovalid расположения, которым hello расширения доступны на удаленном компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="1c513-227">Make sure all URLs resolve toovalid locations that hello extension can access on hello remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="1c513-228">Недопустимый тип свойства ConfigurationArgument</span><span class="sxs-lookup"><span data-stu-id="1c513-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="1c513-229">"Invalid configurationArguments type {0}" (Недопустимый тип ConfigurationArgument: {0}).</span><span class="sxs-lookup"><span data-stu-id="1c513-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="1c513-230">Проблема: hello свойство ConfigurationArguments не удалось разрешить объект tooa хэш-таблицы.</span><span class="sxs-lookup"><span data-stu-id="1c513-230">Problem: hello ConfigurationArguments property cannot resolve tooa Hashtable object.</span></span> 

<span data-ttu-id="1c513-231">Решение. Задайте для свойства ConfigurationArguments тип Hashtable.</span><span class="sxs-lookup"><span data-stu-id="1c513-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="1c513-232">Соответствует формату hello в предыдущем примере hello.</span><span class="sxs-lookup"><span data-stu-id="1c513-232">Follow hello format provided in hello preceeding example.</span></span> <span data-ttu-id="1c513-233">Обращайте внимание на кавычки, запятые и скобки.</span><span class="sxs-lookup"><span data-stu-id="1c513-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="1c513-234">Повторяющееся свойство ConfigurationArguments</span><span class="sxs-lookup"><span data-stu-id="1c513-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="1c513-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments" (В общедоступном и защищенном свойстве configurationArguments найден повторяющийся аргумент "{0}").</span><span class="sxs-lookup"><span data-stu-id="1c513-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="1c513-236">Проблема: hello ConfigurationArguments в открытых параметров и hello ConfigurationArguments в защищенные параметры содержат свойства с hello таким же именем.</span><span class="sxs-lookup"><span data-stu-id="1c513-236">Problem: hello ConfigurationArguments in public settings and hello ConfigurationArguments in protected settings contain properties with hello same name.</span></span>

<span data-ttu-id="1c513-237">Решение: Удалите одну из дублирующихся свойств hello.</span><span class="sxs-lookup"><span data-stu-id="1c513-237">Solution: Remove one of hello duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="1c513-238">Отсутствующие свойства</span><span class="sxs-lookup"><span data-stu-id="1c513-238">Missing Properties</span></span>
<span data-ttu-id="1c513-239">"Configuration.function requires that configuration.url or configuration.module is specified" (Для параметра configuration.function требуется указать свойство configuration.url или configuration.module).</span><span class="sxs-lookup"><span data-stu-id="1c513-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="1c513-240">"Configuration.url requires that configuration.script is specified" (Для параметра configuration.url требуется указать свойство configuration.script).</span><span class="sxs-lookup"><span data-stu-id="1c513-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="1c513-241">"Configuration.script requires that configuration.url is specified" (Для параметра configuration.script требуется указать свойство configuration.url).</span><span class="sxs-lookup"><span data-stu-id="1c513-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="1c513-242">"Configuration.url requires that configuration.function is specified" (Для параметра configuration.url требуется указать свойство configuration.function).</span><span class="sxs-lookup"><span data-stu-id="1c513-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="1c513-243">"ConfigurationUrlSasToken requires that configuration.url is specified" (Для параметра ConfigurationUrlSasToken требуется указать свойство configuration.url).</span><span class="sxs-lookup"><span data-stu-id="1c513-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="1c513-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified" (Для параметра ConfigurationDataUrlSasToken требуется указать свойство configurationData.url).</span><span class="sxs-lookup"><span data-stu-id="1c513-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="1c513-245">Проблема. Для заданного свойства требуется другое свойство, которое отсутствует.</span><span class="sxs-lookup"><span data-stu-id="1c513-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="1c513-246">Решения:</span><span class="sxs-lookup"><span data-stu-id="1c513-246">Solutions:</span></span> 

* <span data-ttu-id="1c513-247">Укажите отсутствующее свойство hello.</span><span class="sxs-lookup"><span data-stu-id="1c513-247">Provide hello missing property.</span></span>
* <span data-ttu-id="1c513-248">Удалите hello собственности, отсутствующее свойство hello.</span><span class="sxs-lookup"><span data-stu-id="1c513-248">Remove hello property that needs hello missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c513-249">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c513-249">Next Steps</span></span>
<span data-ttu-id="1c513-250">Дополнительные сведения о DSC и задает масштабирования виртуальных машин в [с помощью виртуальной машины задает масштаб, с hello расширений Azure DSC](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span><span class="sxs-lookup"><span data-stu-id="1c513-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with hello Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="1c513-251">Получите дополнительные сведения о [безопасном управлении учетными данными посредством DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c513-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="1c513-252">Дополнительные сведения о hello обработчик расширений Azure DSC см. в разделе [обработчик расширений Azure настройки требуемого состояния введение toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1c513-252">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="1c513-253">Дополнительные сведения о PowerShell DSC [посетите центр документации PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="1c513-253">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

