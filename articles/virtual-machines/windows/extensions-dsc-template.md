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
# <a name="windows-vmss-and-desired-state-configuration-with-azure-resource-manager-templates"></a>Настройка масштабируемых наборов виртуальных машин Windows и Desired State Configuration с помощью шаблонов Azure Resource Manager
В этой статье описывается hello шаблона диспетчера ресурсов для hello [обработчик расширений для настройки требуемого состояния](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="template-example-for-a-windows-vm"></a>Пример шаблона для виртуальной машины Windows
Hello следующий фрагмент переходит в раздел ресурсов шаблона hello hello.

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

## <a name="template-example-for-windows-vmss"></a>Пример шаблона для масштабируемых наборов виртуальных машин Windows
На узле VMSS имеется раздел «свойства» с hello «VirtualMachineProfile» атрибута «extensionProfile». Атрибут DSC находится в разделе extensions. 

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

## <a name="detailed-settings-information"></a>Подробные сведения о разделе settings
Hello следующая схема представляет часть параметров hello hello расширение Azure DSC в шаблоне диспетчера ресурсов Azure.

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

## <a name="details"></a>Сведения
| Имя свойства | Тип | Описание |
| --- | --- | --- |
| settings.wmfVersion |string |Указывает версию hello hello Windows Management Framework, который должен быть установлен на виртуальной Машине. Задание этого свойства too'latest "устанавливает hello WMF в более новую версию. только текущий Hello допустимые значения для этого свойства — **«4.0", «5.0", "5.0PP' и «последняя»**. Эти возможные значения: tooupdates субъекта. значение по умолчанию Hello «последняя». |
| settings.configuration.url |string |Указывает URL-адрес расположения hello из какой toodownload ZIP-файл конфигурации DSC. Если указан URL-адрес hello требуется маркер SAS для доступа, необходимо tooset hello protectedSettings.configurationUrlSasToken toohello значение свойства токен SAS. Это свойство обязательное, если заданы свойства settings.configuration.script и (или) settings.configuration.function. |
| settings.configuration.script |string |Указывает имя файла hello hello скрипт, содержащий определение hello конфигурации DSC. Этот скрипт должен быть в корневой папке hello hello ZIP-файле, загружаются из hello URL-адреса, указанного в свойстве configuration.url hello. Это свойство обязательное, если заданы свойства settings.configuration.url и (или) settings.configuration.script. |
| settings.configuration.function |string |Указывает имя конфигурации DSC hello. Hello конфигурации с именем должны содержаться в скрипте hello определяется configuration.script. Это свойство обязательное, если заданы свойства settings.configuration.url и (или) settings.configuration.function. |
| settings.configurationArguments |Коллекция |Определяет любые параметры, которые вы хотите конфигурации DSC tooyour toopass. Это свойство не зашифровано. |
| settings.configurationData.url |string |Указывает URL-адрес hello, из которого toodownload данные конфигурации (.psd1) файла toouse как входные параметры для конфигурации DSC. Если указан URL-адрес hello требуется маркер SAS для доступа, необходимо tooset hello protectedSettings.configurationDataUrlSasToken toohello значение свойства токен SAS. |
| settings.privacy.dataEnabled |string |Включает или отключает сбор данных телеметрии. Hello только допустимые значения для этого свойства — **«Включить», «Отключить», ", или $null**. Если для этого свойства не задано значение или задано значение null, сбор данных телеметрии будет выполняться. значение по умолчанию Hello — ''. [Дополнительные сведения см. здесь.](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/) |
| settings.advancedOptions.downloadMappings |Коллекция |Определяет альтернативного расположения, из которого toodownload hello WMF. [Дополнительные сведения см. здесь.](http://blogs.msdn.com/b/powershell/archive/2015/10/21/azure-dsc-extension-2-2-amp-how-to-map-downloads-of-the-extension-dependencies-to-your-own-location.aspx) |
| protectedSettings.configurationArguments |Коллекция |Определяет любые параметры, которые вы хотите конфигурации DSC tooyour toopass. Это свойство зашифровано. |
| protectedSettings.configurationUrlSasToken |string |Указывает hello маркера tooaccess hello URL-адрес SAS определяется configuration.url. Это свойство зашифровано. |
| protectedSettings.configurationDataUrlSasToken |string |Указывает hello маркера tooaccess hello URL-адрес SAS определяется configurationData.url. Это свойство зашифровано. |

## <a name="settings-vs-protectedsettings"></a>Сравнение разделов settings и protectedSettings
Все параметры сохраняются в текстовый файл параметров на hello виртуальной Машины.
Свойства в разделе «параметры» являются открытые свойства, поскольку не шифруются в текстовом файле параметров hello.
Свойства в разделе «protectedSettings» шифруются с помощью сертификата и не отображаются в виде обычного текста в этот файл на hello виртуальной Машины.

Hello конфигурации необходимы учетные данные, они могут быть включены в protectedSettings:

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

## <a name="example"></a>Пример
Hello в примере является производным из раздела «Начало работы» hello hello [страница обзора обработчик расширения DSC](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
Этот пример использует шаблоны диспетчера ресурсов вместо расширения hello toodeploy командлетов. Сохранить конфигурацию «IisInstall.ps1» hello, размещения в ней. ZIP-файл и файл hello передачи в URL-адрес доступен. В этом примере используется хранилище больших двоичных объектов, но это возможно toodownload. ZIP-файлы из любого произвольного места.

Hello шаблона диспетчера ресурсов Azure hello следующий код дает правильный файл toodownload ВМ hello hello и выполните соответствующую функцию PowerShell hello.

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

## <a name="updating-from-hello-previous-format"></a>Обновление из предыдущего формата hello
Все параметры в hello предыдущего формата (содержащий hello открытые свойства ModulesUrl, ConfigurationFunction, SasToken или свойства) автоматически адаптировать toohello текущий формат и выполнять так же, как раньше.

Следующая схема Hello является hello предыдущие параметры схемы выглядела:

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

Вот, как старый формат hello адаптирует toohello текущего формата.

| Имя свойства | Предыдущий эквивалент |
| --- | --- |
| settings.wmfVersion |settings.wmfVersion |
| settings.configuration.url |settings.ModulesUrl |
| settings.configuration.script |Первая часть свойства settings.ConfigurationFunction (перед \\\\). |
| settings.configuration.function |Вторая часть свойства settings.ConfigurationFunction (после \\\\). |
| settings.configurationArguments |settings.Properties |
| settings.configurationData.url |protectedSettings.DataBlobUri (без маркера SAS) |
| settings.privacy.dataEnabled |settings.privacy.dataEnabled |
| settings.advancedOptions.downloadMappings |settings.advancedOptions.downloadMappings |
| protectedSettings.configurationArguments |protectedSettings.Properties |
| protectedSettings.configurationUrlSasToken |settings.SasToken |
| protectedSettings.configurationDataUrlSasToken |Маркер SAS из свойства protectedSettings.DataBlobUri |

## <a name="troubleshooting---error-code-1100"></a>Устранение неполадок — код ошибки 1100
Код ошибки 1100 указывает на проблему с hello расширения toohello DSC ввод данных пользователем.
текст Hello этих ошибок является переменной и может измениться.
Ниже приведены некоторые ошибки hello, с которыми вы можете столкнуться, и способах их устранения.

### <a name="invalid-values"></a>Недопустимые значения
"Privacy.dataCollection is '{0}'. Hello только допустимые значения: «, «Включить» и «Отключить»» «является WmfVersion «{0}». Возможные значения: … и latest.

Проблема. Указано неразрешенное значение.

Решение: Изменение hello недопустимое значение tooa допустимое значение. См. таблицу hello в разделе "Сведения" hello.

### <a name="invalid-url"></a>Недопустимый URL-адрес
"ConfigurationData.url is '{0}'. This is not a valid URL" (Значение свойства configurationData.url — "{0}". Это недопустимый URL-адрес). "DataBlobUri is '{0}'. This is not a valid URL" (Значение свойства DataBlobUri — "{0}". Это недопустимый URL-адрес). "Configuration.url is '{0}'. This is not a valid URL" (Значение свойства Configuration.url — "{0}". Это недопустимый URL-адрес).

Проблема. Указан недопустимый URL-адрес.

Решение. Проверьте все указанные URL-адреса. Убедитесь, что все URL-адреса разрешения toovalid расположения, которым hello расширения доступны на удаленном компьютере hello.

### <a name="invalid-configurationargument-type"></a>Недопустимый тип свойства ConfigurationArgument
"Invalid configurationArguments type {0}" (Недопустимый тип ConfigurationArgument: {0}).

Проблема: hello свойство ConfigurationArguments не удалось разрешить объект tooa хэш-таблицы. 

Решение. Задайте для свойства ConfigurationArguments тип Hashtable. Соответствует формату hello в предыдущем примере hello. Обращайте внимание на кавычки, запятые и скобки.

### <a name="duplicate-configurationarguments"></a>Повторяющееся свойство ConfigurationArguments
"Found duplicate arguments '{0}' in both public and protected configurationArguments" (В общедоступном и защищенном свойстве configurationArguments найден повторяющийся аргумент "{0}").

Проблема: hello ConfigurationArguments в открытых параметров и hello ConfigurationArguments в защищенные параметры содержат свойства с hello таким же именем.

Решение: Удалите одну из дублирующихся свойств hello.

### <a name="missing-properties"></a>Отсутствующие свойства
"Configuration.function requires that configuration.url or configuration.module is specified" (Для параметра configuration.function требуется указать свойство configuration.url или configuration.module).

"Configuration.url requires that configuration.script is specified" (Для параметра configuration.url требуется указать свойство configuration.script).

"Configuration.script requires that configuration.url is specified" (Для параметра configuration.script требуется указать свойство configuration.url).

"Configuration.url requires that configuration.function is specified" (Для параметра configuration.url требуется указать свойство configuration.function).

"ConfigurationUrlSasToken requires that configuration.url is specified" (Для параметра ConfigurationUrlSasToken требуется указать свойство configuration.url).

"ConfigurationDataUrlSasToken requires that configurationData.url is specified" (Для параметра ConfigurationDataUrlSasToken требуется указать свойство configurationData.url).

Проблема. Для заданного свойства требуется другое свойство, которое отсутствует.

Решения: 

* Укажите отсутствующее свойство hello.
* Удалите hello собственности, отсутствующее свойство hello.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о DSC и задает масштабирования виртуальных машин в [с помощью виртуальной машины задает масштаб, с hello расширений Azure DSC](../../virtual-machine-scale-sets/virtual-machine-scale-sets-dsc.md)

Получите дополнительные сведения о [безопасном управлении учетными данными посредством DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Дополнительные сведения о hello обработчик расширений Azure DSC см. в разделе [обработчик расширений Azure настройки требуемого состояния введение toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Дополнительные сведения о PowerShell DSC [посетите центр документации PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

