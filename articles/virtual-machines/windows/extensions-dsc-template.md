---
title: "Шаблон Resource Manager для настройки требуемого состояния | Документация Майкрософт"
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
ms.openlocfilehash: 4292f9d8cd181073fdf0adff99fcb9624e0e9f55
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a><span data-ttu-id="c3a84-103">Настройка масштабируемых наборов виртуальных машин Windows и Desired State Configuration с помощью шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c3a84-103">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>
<span data-ttu-id="c3a84-104">В этой статье описывается шаблон Resource Manager для [обработчика расширения для настройки требуемого состояния](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c3a84-104">This article describes the Resource Manager template for the [Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="template-example-for-a-windows-vm"></a><span data-ttu-id="c3a84-105">Пример шаблона для виртуальной машины Windows</span><span class="sxs-lookup"><span data-stu-id="c3a84-105">Template example for a Windows VM</span></span>
<span data-ttu-id="c3a84-106">В приведенном ниже фрагменте кода показан раздел Resource шаблона.</span><span class="sxs-lookup"><span data-stu-id="c3a84-106">The following snippet goes into the Resource section of the template.</span></span>

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

## <a name="template-example-for-windows-vmss"></a><span data-ttu-id="c3a84-107">Пример шаблона для масштабируемых наборов виртуальных машин Windows</span><span class="sxs-lookup"><span data-stu-id="c3a84-107">Template example for Windows VMSS</span></span>
<span data-ttu-id="c3a84-108">Узел масштабируемых наборов виртуальных машин содержит раздел properties с атрибутами VirtualMachineProfile и extensionProfile.</span><span class="sxs-lookup"><span data-stu-id="c3a84-108">A VMSS node has a "properties" section with the "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="c3a84-109">Атрибут DSC находится в разделе extensions.</span><span class="sxs-lookup"><span data-stu-id="c3a84-109">DSC is added under "extensions".</span></span> 

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

## <a name="detailed-settings-information"></a><span data-ttu-id="c3a84-110">Подробные сведения о разделе settings</span><span class="sxs-lookup"><span data-stu-id="c3a84-110">Detailed Settings Information</span></span>
<span data-ttu-id="c3a84-111">В приведенной ниже схеме показана часть settings расширения Azure DSC в шаблоне Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c3a84-111">The following schema is for the settings portion of the Azure DSC extension in an Azure Resource Manager template.</span></span>

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

## <a name="details"></a><span data-ttu-id="c3a84-112">Сведения</span><span class="sxs-lookup"><span data-stu-id="c3a84-112">Details</span></span>
| <span data-ttu-id="c3a84-113">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="c3a84-113">Property Name</span></span> | <span data-ttu-id="c3a84-114">Тип</span><span class="sxs-lookup"><span data-stu-id="c3a84-114">Type</span></span> | <span data-ttu-id="c3a84-115">Описание</span><span class="sxs-lookup"><span data-stu-id="c3a84-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3a84-116">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="c3a84-116">settings.wmfVersion</span></span> |<span data-ttu-id="c3a84-117">string</span><span class="sxs-lookup"><span data-stu-id="c3a84-117">string</span></span> |<span data-ttu-id="c3a84-118">Указывает версию Windows Management Framework, которую необходимо установить на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c3a84-118">Specifies the version of the Windows Management Framework that should be installed on your VM.</span></span> <span data-ttu-id="c3a84-119">Если задать для этого свойства значение latest, будет установлена последняя версия Windows Management Framework.</span><span class="sxs-lookup"><span data-stu-id="c3a84-119">Setting this property to 'latest' installs the most updated version of WMF.</span></span> <span data-ttu-id="c3a84-120">Для этого свойства доступны только такие значения: **4.0, 5.0, 5.0PP и latest**.</span><span class="sxs-lookup"><span data-stu-id="c3a84-120">The only current possible values for this property are **'4.0', '5.0', '5.0PP', and 'latest'**.</span></span> <span data-ttu-id="c3a84-121">Возможные значения зависят от обновлений.</span><span class="sxs-lookup"><span data-stu-id="c3a84-121">These possible values are subject to updates.</span></span> <span data-ttu-id="c3a84-122">По умолчанию используется значение latest.</span><span class="sxs-lookup"><span data-stu-id="c3a84-122">The default value is 'latest'.</span></span> |
| <span data-ttu-id="c3a84-123">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="c3a84-123">settings.configuration.url</span></span> |<span data-ttu-id="c3a84-124">string</span><span class="sxs-lookup"><span data-stu-id="c3a84-124">string</span></span> |<span data-ttu-id="c3a84-125">Указывает URL-адрес расположения, из которого можно скачать ZIP-файл конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="c3a84-125">Specifies the URL location from which to download your DSC configuration zip file.</span></span> <span data-ttu-id="c3a84-126">Если для доступа к предоставленному URL-адресу требуется маркер SAS, необходимо задать для свойства protectedSettings.configurationUrlSasToken значение маркера SAS.</span><span class="sxs-lookup"><span data-stu-id="c3a84-126">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationUrlSasToken property to the value of your SAS token.</span></span> <span data-ttu-id="c3a84-127">Это свойство обязательное, если заданы свойства settings.configuration.script и (или) settings.configuration.function.</span><span class="sxs-lookup"><span data-stu-id="c3a84-127">This property is required if settings.configuration.script and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="c3a84-128">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="c3a84-128">settings.configuration.script</span></span> |<span data-ttu-id="c3a84-129">string</span><span class="sxs-lookup"><span data-stu-id="c3a84-129">string</span></span> |<span data-ttu-id="c3a84-130">Указывает имя файла скрипта, содержащего определение вашей конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="c3a84-130">Specifies the file name of the script that contains the definition of your DSC configuration.</span></span> <span data-ttu-id="c3a84-131">Этот скрипт должен находиться в корневом каталоге ZIP-файла, скачанного по URL-адресу, указанному в свойстве configuration.url.</span><span class="sxs-lookup"><span data-stu-id="c3a84-131">This script must be in the root folder of the zip file downloaded from the URL specified by the configuration.url property.</span></span> <span data-ttu-id="c3a84-132">Это свойство обязательное, если заданы свойства settings.configuration.url и (или) settings.configuration.script.</span><span class="sxs-lookup"><span data-stu-id="c3a84-132">This property is required if settings.configuration.url and/or settings.configuration.script are defined.</span></span> |
| <span data-ttu-id="c3a84-133">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="c3a84-133">settings.configuration.function</span></span> |<span data-ttu-id="c3a84-134">string</span><span class="sxs-lookup"><span data-stu-id="c3a84-134">string</span></span> |<span data-ttu-id="c3a84-135">Указывает имя вашей конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="c3a84-135">Specifies the name of your DSC configuration.</span></span> <span data-ttu-id="c3a84-136">Указанную конфигурацию необходимо добавить в скрипт, заданный в свойстве configuration.script.</span><span class="sxs-lookup"><span data-stu-id="c3a84-136">The configuration named must be contained in the script defined by configuration.script.</span></span> <span data-ttu-id="c3a84-137">Это свойство обязательное, если заданы свойства settings.configuration.url и (или) settings.configuration.function.</span><span class="sxs-lookup"><span data-stu-id="c3a84-137">This property is required if settings.configuration.url and/or settings.configuration.function are defined.</span></span> |
| <span data-ttu-id="c3a84-138">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="c3a84-138">settings.configurationArguments</span></span> |<span data-ttu-id="c3a84-139">Коллекция</span><span class="sxs-lookup"><span data-stu-id="c3a84-139">Collection</span></span> |<span data-ttu-id="c3a84-140">Определяет параметры, которые необходимо передать в конфигурацию DSC.</span><span class="sxs-lookup"><span data-stu-id="c3a84-140">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="c3a84-141">Это свойство не зашифровано.</span><span class="sxs-lookup"><span data-stu-id="c3a84-141">This property is not encrypted.</span></span> |
| <span data-ttu-id="c3a84-142">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="c3a84-142">settings.configurationData.url</span></span> |<span data-ttu-id="c3a84-143">строка</span><span class="sxs-lookup"><span data-stu-id="c3a84-143">string</span></span> |<span data-ttu-id="c3a84-144">Указывает URL-адрес расположения, из которого можно скачать файл данных конфигурации (в формате PDS1), используемый в качестве входных данных для вашей конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="c3a84-144">Specifies the URL from which to download your configuration data (.psd1) file to use as input for your DSC configuration.</span></span> <span data-ttu-id="c3a84-145">Если для доступа к предоставленному URL-адресу требуется маркер SAS, необходимо задать для свойства protectedSettings.configurationDataUrlSasToken значение маркера SAS.</span><span class="sxs-lookup"><span data-stu-id="c3a84-145">If the URL provided requires a SAS token for access, you need to set the protectedSettings.configurationDataUrlSasToken property to the value of your SAS token.</span></span> |
| <span data-ttu-id="c3a84-146">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="c3a84-146">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="c3a84-147">string</span><span class="sxs-lookup"><span data-stu-id="c3a84-147">string</span></span> |<span data-ttu-id="c3a84-148">Включает или отключает сбор данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="c3a84-148">Enables or disables telemetry collection.</span></span> <span data-ttu-id="c3a84-149">Для этого свойства доступны только такие значения: **Enable, Disable или $null**.</span><span class="sxs-lookup"><span data-stu-id="c3a84-149">The only possible values for this property are **'Enable', 'Disable', '', or $null**.</span></span> <span data-ttu-id="c3a84-150">Если для этого свойства не задано значение или задано значение null, сбор данных телеметрии будет выполняться.</span><span class="sxs-lookup"><span data-stu-id="c3a84-150">Leaving this property blank or null enables telemetry.</span></span> <span data-ttu-id="c3a84-151">Значение по умолчанию — ''.</span><span class="sxs-lookup"><span data-stu-id="c3a84-151">The default value is ''.</span></span> [<span data-ttu-id="c3a84-152">Дополнительные сведения см. здесь.</span><span class="sxs-lookup"><span data-stu-id="c3a84-152">More Information</span></span>](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| <span data-ttu-id="c3a84-153">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="c3a84-153">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="c3a84-154">Коллекция</span><span class="sxs-lookup"><span data-stu-id="c3a84-154">Collection</span></span> |<span data-ttu-id="c3a84-155">Определяет альтернативные расположения для скачивания Windows Management Framework.</span><span class="sxs-lookup"><span data-stu-id="c3a84-155">Defines alternate locations from which to download the WMF.</span></span> [<span data-ttu-id="c3a84-156">Дополнительные сведения см. здесь.</span><span class="sxs-lookup"><span data-stu-id="c3a84-156">More Information</span></span>](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| <span data-ttu-id="c3a84-157">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="c3a84-157">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="c3a84-158">Коллекция</span><span class="sxs-lookup"><span data-stu-id="c3a84-158">Collection</span></span> |<span data-ttu-id="c3a84-159">Определяет параметры, которые необходимо передать в конфигурацию DSC.</span><span class="sxs-lookup"><span data-stu-id="c3a84-159">Defines any parameters you would like to pass to your DSC configuration.</span></span> <span data-ttu-id="c3a84-160">Это свойство зашифровано.</span><span class="sxs-lookup"><span data-stu-id="c3a84-160">This property is encrypted.</span></span> |
| <span data-ttu-id="c3a84-161">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="c3a84-161">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="c3a84-162">string</span><span class="sxs-lookup"><span data-stu-id="c3a84-162">string</span></span> |<span data-ttu-id="c3a84-163">Указывает маркер SAS для доступа к URL-адресу, определенному в свойстве configuration.url.</span><span class="sxs-lookup"><span data-stu-id="c3a84-163">Specifies the SAS token to access the URL defined by configuration.url.</span></span> <span data-ttu-id="c3a84-164">Это свойство зашифровано.</span><span class="sxs-lookup"><span data-stu-id="c3a84-164">This property is encrypted.</span></span> |
| <span data-ttu-id="c3a84-165">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="c3a84-165">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="c3a84-166">string</span><span class="sxs-lookup"><span data-stu-id="c3a84-166">string</span></span> |<span data-ttu-id="c3a84-167">Указывает маркер SAS для доступа к URL-адресу, определенному в свойстве configurationData.url.</span><span class="sxs-lookup"><span data-stu-id="c3a84-167">Specifies the SAS token to access the URL defined by configurationData.url.</span></span> <span data-ttu-id="c3a84-168">Это свойство зашифровано.</span><span class="sxs-lookup"><span data-stu-id="c3a84-168">This property is encrypted.</span></span> |

## <a name="settings-vs-protectedsettings"></a><span data-ttu-id="c3a84-169">Сравнение разделов settings и protectedSettings</span><span class="sxs-lookup"><span data-stu-id="c3a84-169">Settings vs. ProtectedSettings</span></span>
<span data-ttu-id="c3a84-170">Все параметры сохраняются в текстовом файле параметров на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c3a84-170">All settings are saved in a settings text file on the VM.</span></span>
<span data-ttu-id="c3a84-171">Свойства в разделе settings общедоступные, так как они не зашифрованы в текстовом файле параметров.</span><span class="sxs-lookup"><span data-stu-id="c3a84-171">Properties under 'settings' are public properties because they are not encrypted in the settings text file.</span></span>
<span data-ttu-id="c3a84-172">Свойства в разделе protectedSettings зашифрованы с помощью сертификата, а это значит, что они не отображаются как обычный текст в файле на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="c3a84-172">Properties under 'protectedSettings' are encrypted with a certificate and are not shown in plain text in this file on the VM.</span></span>

<span data-ttu-id="c3a84-173">Если для конфигурации нужны учетные данные, их можно добавить в раздел protectedSettings.</span><span class="sxs-lookup"><span data-stu-id="c3a84-173">If the configuration needs credentials, they can be included in protectedSettings:</span></span>

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

## <a name="example"></a><span data-ttu-id="c3a84-174">Пример</span><span class="sxs-lookup"><span data-stu-id="c3a84-174">Example</span></span>
<span data-ttu-id="c3a84-175">Следующий пример основан на примере конфигурации из раздела "Приступая к работе" статьи [Общие сведения об обработчике расширения Desired State Configuration в Azure](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c3a84-175">The following example derives from the "Getting Started" section of the [DSC Extension Handler Overview page](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
<span data-ttu-id="c3a84-176">В этом примере для развертывания расширения используются шаблоны Resource Manager, а не командлеты.</span><span class="sxs-lookup"><span data-stu-id="c3a84-176">This example uses Resource Manager templates instead of cmdlets to deploy the extension.</span></span> <span data-ttu-id="c3a84-177">Сохраните конфигурацию IisInstall.ps1, добавьте ее в ZIP-файл и передайте файл на доступный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="c3a84-177">Save the "IisInstall.ps1" configuration, place it in a .ZIP file, and upload the file in an accessible URL.</span></span> <span data-ttu-id="c3a84-178">В этом примере используется хранилище BLOB-объектов Azure, но ZIP-файл можно скачать из любого произвольного расположения.</span><span class="sxs-lookup"><span data-stu-id="c3a84-178">This example uses Azure blob storage, but it is possible to download .ZIP files from any arbitrary location.</span></span>

<span data-ttu-id="c3a84-179">В шаблоне Azure Resource Manager следующий код указывает виртуальной машине скачать правильный файл и выполнить соответствующую функцию PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c3a84-179">In the Azure Resource Manager template, the following code instructs the VM to download the correct file and run the appropriate PowerShell function:</span></span>

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

## <a name="updating-from-the-previous-format"></a><span data-ttu-id="c3a84-180">Обновление из предыдущего формата</span><span class="sxs-lookup"><span data-stu-id="c3a84-180">Updating from the Previous Format</span></span>
<span data-ttu-id="c3a84-181">Все параметры в предыдущем формате (содержащие общедоступные свойства ModulesUrl, ConfigurationFunction, SasToken или Properties) автоматически адаптируются к текущему формату и выполняются в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="c3a84-181">Any settings in the previous format (containing the public properties ModulesUrl, ConfigurationFunction, SasToken, or Properties) automatically adapt to the current format and run just as they did before.</span></span>

<span data-ttu-id="c3a84-182">Раньше схема settings выглядела следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c3a84-182">The following schema is what the previous settings schema looked like:</span></span>

```json
"settings": {
    "WMFVersion": "latest",
    "ModulesUrl": "https://UrlToZipContainingConfigurationScript.ps1.zip",
    "SasToken": "SAS Token if ModulesUrl points to private Azure Blob Storage",
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

<span data-ttu-id="c3a84-183">Вот как меняется предыдущий формат:</span><span class="sxs-lookup"><span data-stu-id="c3a84-183">Here's how the previous format adapts to the current format:</span></span>

| <span data-ttu-id="c3a84-184">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="c3a84-184">Property Name</span></span> | <span data-ttu-id="c3a84-185">Предыдущий эквивалент</span><span class="sxs-lookup"><span data-stu-id="c3a84-185">Previous Schema Equivalent</span></span> |
| --- | --- |
| <span data-ttu-id="c3a84-186">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="c3a84-186">settings.wmfVersion</span></span> |<span data-ttu-id="c3a84-187">settings.wmfVersion</span><span class="sxs-lookup"><span data-stu-id="c3a84-187">settings.WMFVersion</span></span> |
| <span data-ttu-id="c3a84-188">settings.configuration.url</span><span class="sxs-lookup"><span data-stu-id="c3a84-188">settings.configuration.url</span></span> |<span data-ttu-id="c3a84-189">settings.ModulesUrl</span><span class="sxs-lookup"><span data-stu-id="c3a84-189">settings.ModulesUrl</span></span> |
| <span data-ttu-id="c3a84-190">settings.configuration.script</span><span class="sxs-lookup"><span data-stu-id="c3a84-190">settings.configuration.script</span></span> |<span data-ttu-id="c3a84-191">Первая часть свойства settings.ConfigurationFunction (перед \\\\).</span><span class="sxs-lookup"><span data-stu-id="c3a84-191">First part of settings.ConfigurationFunction (before '\\\\')</span></span> |
| <span data-ttu-id="c3a84-192">settings.configuration.function</span><span class="sxs-lookup"><span data-stu-id="c3a84-192">settings.configuration.function</span></span> |<span data-ttu-id="c3a84-193">Вторая часть свойства settings.ConfigurationFunction (после \\\\).</span><span class="sxs-lookup"><span data-stu-id="c3a84-193">Second part of settings.ConfigurationFunction (after '\\\\')</span></span> |
| <span data-ttu-id="c3a84-194">settings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="c3a84-194">settings.configurationArguments</span></span> |<span data-ttu-id="c3a84-195">settings.Properties</span><span class="sxs-lookup"><span data-stu-id="c3a84-195">settings.Properties</span></span> |
| <span data-ttu-id="c3a84-196">settings.configurationData.url</span><span class="sxs-lookup"><span data-stu-id="c3a84-196">settings.configurationData.url</span></span> |<span data-ttu-id="c3a84-197">protectedSettings.DataBlobUri (без маркера SAS)</span><span class="sxs-lookup"><span data-stu-id="c3a84-197">protectedSettings.DataBlobUri (without SAS token)</span></span> |
| <span data-ttu-id="c3a84-198">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="c3a84-198">settings.privacy.dataEnabled</span></span> |<span data-ttu-id="c3a84-199">settings.privacy.dataEnabled</span><span class="sxs-lookup"><span data-stu-id="c3a84-199">settings.Privacy.DataEnabled</span></span> |
| <span data-ttu-id="c3a84-200">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="c3a84-200">settings.advancedOptions.downloadMappings</span></span> |<span data-ttu-id="c3a84-201">settings.advancedOptions.downloadMappings</span><span class="sxs-lookup"><span data-stu-id="c3a84-201">settings.AdvancedOptions.DownloadMappings</span></span> |
| <span data-ttu-id="c3a84-202">protectedSettings.configurationArguments</span><span class="sxs-lookup"><span data-stu-id="c3a84-202">protectedSettings.configurationArguments</span></span> |<span data-ttu-id="c3a84-203">protectedSettings.Properties</span><span class="sxs-lookup"><span data-stu-id="c3a84-203">protectedSettings.Properties</span></span> |
| <span data-ttu-id="c3a84-204">protectedSettings.configurationUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="c3a84-204">protectedSettings.configurationUrlSasToken</span></span> |<span data-ttu-id="c3a84-205">settings.SasToken</span><span class="sxs-lookup"><span data-stu-id="c3a84-205">settings.SasToken</span></span> |
| <span data-ttu-id="c3a84-206">protectedSettings.configurationDataUrlSasToken</span><span class="sxs-lookup"><span data-stu-id="c3a84-206">protectedSettings.configurationDataUrlSasToken</span></span> |<span data-ttu-id="c3a84-207">Маркер SAS из свойства protectedSettings.DataBlobUri</span><span class="sxs-lookup"><span data-stu-id="c3a84-207">SAS token from protectedSettings.DataBlobUri</span></span> |

## <a name="troubleshooting---error-code-1100"></a><span data-ttu-id="c3a84-208">Устранение неполадок — код ошибки 1100</span><span class="sxs-lookup"><span data-stu-id="c3a84-208">Troubleshooting - Error Code 1100</span></span>
<span data-ttu-id="c3a84-209">Код ошибки 1100 указывает на проблему с входными данными пользователя в расширении DSC.</span><span class="sxs-lookup"><span data-stu-id="c3a84-209">Error Code 1100 indicates that there is a problem with the user input to the DSC extension.</span></span>
<span data-ttu-id="c3a84-210">Текст этих ошибок может меняться.</span><span class="sxs-lookup"><span data-stu-id="c3a84-210">The text of these errors is variable and may change.</span></span>
<span data-ttu-id="c3a84-211">Ниже приведены некоторые общие ошибки и способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="c3a84-211">Here are some of the errors you may run into and how you can fix them.</span></span>

### <a name="invalid-values"></a><span data-ttu-id="c3a84-212">Недопустимые значения</span><span class="sxs-lookup"><span data-stu-id="c3a84-212">Invalid Values</span></span>
<span data-ttu-id="c3a84-213">"Privacy.dataCollection is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="c3a84-213">"Privacy.dataCollection is '{0}'.</span></span> <span data-ttu-id="c3a84-214">The only possible values are '', 'Enable', and 'Disable'" (Значение свойства Privacy.dataCollection — "{0}". Единственные возможные значения: Enable и Disable). "WmfVersion is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="c3a84-214">The only possible values are '', 'Enable', and 'Disable'" "WmfVersion is '{0}'.</span></span> <span data-ttu-id="c3a84-215">Возможные значения: …</span><span class="sxs-lookup"><span data-stu-id="c3a84-215">Only possible values are …</span></span> <span data-ttu-id="c3a84-216">и latest.</span><span class="sxs-lookup"><span data-stu-id="c3a84-216">and 'latest'"</span></span>

<span data-ttu-id="c3a84-217">Проблема. Указано неразрешенное значение.</span><span class="sxs-lookup"><span data-stu-id="c3a84-217">Problem: A provided value is not allowed.</span></span>

<span data-ttu-id="c3a84-218">Решение. Замените недопустимое значение допустимым.</span><span class="sxs-lookup"><span data-stu-id="c3a84-218">Solution: Change the invalid value to a valid value.</span></span> <span data-ttu-id="c3a84-219">См. раздел "Сведения".</span><span class="sxs-lookup"><span data-stu-id="c3a84-219">See the table in the Details section.</span></span>

### <a name="invalid-url"></a><span data-ttu-id="c3a84-220">Недопустимый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="c3a84-220">Invalid URL</span></span>
<span data-ttu-id="c3a84-221">"ConfigurationData.url is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="c3a84-221">"ConfigurationData.url is '{0}'.</span></span> <span data-ttu-id="c3a84-222">This is not a valid URL" (Значение свойства configurationData.url — "{0}". Это недопустимый URL-адрес). "DataBlobUri is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="c3a84-222">This is not a valid URL" "DataBlobUri is '{0}'.</span></span> <span data-ttu-id="c3a84-223">This is not a valid URL" (Значение свойства DataBlobUri — "{0}". Это недопустимый URL-адрес). "Configuration.url is '{0}'.</span><span class="sxs-lookup"><span data-stu-id="c3a84-223">This is not a valid URL" "Configuration.url is '{0}'.</span></span> <span data-ttu-id="c3a84-224">This is not a valid URL" (Значение свойства Configuration.url — "{0}". Это недопустимый URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="c3a84-224">This is not a valid URL"</span></span>

<span data-ttu-id="c3a84-225">Проблема. Указан недопустимый URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="c3a84-225">Problem: A provided URL is not valid.</span></span>

<span data-ttu-id="c3a84-226">Решение. Проверьте все указанные URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="c3a84-226">Solution: Check all your provided URLs.</span></span> <span data-ttu-id="c3a84-227">Убедитесь, что все URL-адреса разрешаются в допустимые расположения, к которым расширение может получить доступ на удаленном компьютере.</span><span class="sxs-lookup"><span data-stu-id="c3a84-227">Make sure all URLs resolve to valid locations that the extension can access on the remote machine.</span></span>

### <a name="invalid-configurationargument-type"></a><span data-ttu-id="c3a84-228">Недопустимый тип свойства ConfigurationArgument</span><span class="sxs-lookup"><span data-stu-id="c3a84-228">Invalid ConfigurationArgument Type</span></span>
<span data-ttu-id="c3a84-229">"Invalid configurationArguments type {0}" (Недопустимый тип ConfigurationArgument: {0}).</span><span class="sxs-lookup"><span data-stu-id="c3a84-229">"Invalid configurationArguments type {0}"</span></span>

<span data-ttu-id="c3a84-230">Проблема. Невозможно разрешить свойство ConfigurationArguments в объект Hashtable.</span><span class="sxs-lookup"><span data-stu-id="c3a84-230">Problem: The ConfigurationArguments property cannot resolve to a Hashtable object.</span></span> 

<span data-ttu-id="c3a84-231">Решение. Задайте для свойства ConfigurationArguments тип Hashtable.</span><span class="sxs-lookup"><span data-stu-id="c3a84-231">Solution: Make your ConfigurationArguments property a Hashtable.</span></span> <span data-ttu-id="c3a84-232">Следуйте формату из приведенного выше примера.</span><span class="sxs-lookup"><span data-stu-id="c3a84-232">Follow the format provided in the preceeding example.</span></span> <span data-ttu-id="c3a84-233">Обращайте внимание на кавычки, запятые и скобки.</span><span class="sxs-lookup"><span data-stu-id="c3a84-233">Watch out for quotes, commas, and braces.</span></span>

### <a name="duplicate-configurationarguments"></a><span data-ttu-id="c3a84-234">Повторяющееся свойство ConfigurationArguments</span><span class="sxs-lookup"><span data-stu-id="c3a84-234">Duplicate ConfigurationArguments</span></span>
<span data-ttu-id="c3a84-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments" (В общедоступном и защищенном свойстве configurationArguments найден повторяющийся аргумент "{0}").</span><span class="sxs-lookup"><span data-stu-id="c3a84-235">"Found duplicate arguments '{0}' in both public and protected configurationArguments"</span></span>

<span data-ttu-id="c3a84-236">Проблема. Свойства ConfigurationArguments из общедоступной и защищенной схемы settings содержат свойства с одинаковыми именами.</span><span class="sxs-lookup"><span data-stu-id="c3a84-236">Problem: The ConfigurationArguments in public settings and the ConfigurationArguments in protected settings contain properties with the same name.</span></span>

<span data-ttu-id="c3a84-237">Решение. Удалите одно из повторяющихся свойств.</span><span class="sxs-lookup"><span data-stu-id="c3a84-237">Solution: Remove one of the duplicate properties.</span></span>

### <a name="missing-properties"></a><span data-ttu-id="c3a84-238">Отсутствующие свойства</span><span class="sxs-lookup"><span data-stu-id="c3a84-238">Missing Properties</span></span>
<span data-ttu-id="c3a84-239">"Configuration.function requires that configuration.url or configuration.module is specified" (Для параметра configuration.function требуется указать свойство configuration.url или configuration.module).</span><span class="sxs-lookup"><span data-stu-id="c3a84-239">"Configuration.function requires that configuration.url or configuration.module is specified"</span></span>

<span data-ttu-id="c3a84-240">"Configuration.url requires that configuration.script is specified" (Для параметра configuration.url требуется указать свойство configuration.script).</span><span class="sxs-lookup"><span data-stu-id="c3a84-240">"Configuration.url requires that configuration.script is specified"</span></span>

<span data-ttu-id="c3a84-241">"Configuration.script requires that configuration.url is specified" (Для параметра configuration.script требуется указать свойство configuration.url).</span><span class="sxs-lookup"><span data-stu-id="c3a84-241">"Configuration.script requires that configuration.url is specified"</span></span>

<span data-ttu-id="c3a84-242">"Configuration.url requires that configuration.function is specified" (Для параметра configuration.url требуется указать свойство configuration.function).</span><span class="sxs-lookup"><span data-stu-id="c3a84-242">"Configuration.url requires that configuration.function is specified"</span></span>

<span data-ttu-id="c3a84-243">"ConfigurationUrlSasToken requires that configuration.url is specified" (Для параметра ConfigurationUrlSasToken требуется указать свойство configuration.url).</span><span class="sxs-lookup"><span data-stu-id="c3a84-243">"ConfigurationUrlSasToken requires that configuration.url is specified"</span></span>

<span data-ttu-id="c3a84-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified" (Для параметра ConfigurationDataUrlSasToken требуется указать свойство configurationData.url).</span><span class="sxs-lookup"><span data-stu-id="c3a84-244">"ConfigurationDataUrlSasToken requires that configurationData.url is specified"</span></span>

<span data-ttu-id="c3a84-245">Проблема. Для заданного свойства требуется другое свойство, которое отсутствует.</span><span class="sxs-lookup"><span data-stu-id="c3a84-245">Problem: A defined property needs another property that is missing.</span></span>

<span data-ttu-id="c3a84-246">Решения:</span><span class="sxs-lookup"><span data-stu-id="c3a84-246">Solutions:</span></span> 

* <span data-ttu-id="c3a84-247">Укажите отсутствующее свойство.</span><span class="sxs-lookup"><span data-stu-id="c3a84-247">Provide the missing property.</span></span>
* <span data-ttu-id="c3a84-248">Удалите свойство, требующее отсутствующего свойства.</span><span class="sxs-lookup"><span data-stu-id="c3a84-248">Remove the property that needs the missing property.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3a84-249">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c3a84-249">Next Steps</span></span>
<span data-ttu-id="c3a84-250">Дополнительные сведения о DSC и масштабируемых наборах виртуальных машин см. в статье [Использование наборов масштабирования виртуальных машин с помощью расширения Azure DSC](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md).</span><span class="sxs-lookup"><span data-stu-id="c3a84-250">Learn about DSC and virtual machine scale sets in [Using Virtual Machine Scale Sets with the Azure DSC Extension](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)</span></span>

<span data-ttu-id="c3a84-251">Получите дополнительные сведения о [безопасном управлении учетными данными посредством DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c3a84-251">Find more details on [DSC's secure credential management](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="c3a84-252">Дополнительные сведения об обработчике расширений DSC см. в статье [Общие сведения об обработчике расширения для настройки требуемого состояния в Azure](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c3a84-252">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="c3a84-253">Для получения дополнительных сведений о DSC PowerShell [посетите центр документации PowerShell](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="c3a84-253">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

