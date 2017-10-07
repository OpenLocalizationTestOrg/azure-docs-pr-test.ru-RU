---
title: "aaaCommon вызывает повторное использование ролей облачной службы | Документы Microsoft"
description: "Внезапный перезапуск роли облачной службы может привести к длительному простою. Ниже приведены некоторые распространенные проблемы, вызывающие toobe ролей перезапуска, которая может помочь сократить время простоя."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 533930d1-8035-4402-b16a-cf887b2c4f85
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 8fa152b33d2b22a8a02f834d4bc38519b4272f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="common-issues-that-cause-roles-toorecycle"></a>Общие ошибки, вызывающие toorecycle ролей
В этой статье рассматриваются некоторые основные причины проблем с развертыванием hello и предоставляет разрешение советы toohelp устранения этих проблем. Указывает на то, что возникла проблема с приложением при toostart сбоя экземпляра роли hello или циклически переключается между состояниями инициализации, занятости и остановки hello.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-runtime-dependencies"></a>Отсутствующие зависимости среды выполнения
Если роль приложения использует любую сборку, не является частью hello .NET Framework или hello Azure управляемой библиотеке, необходимо явно включить эту сборку в пакет приложения hello. Имейте в виду, что другие платформы Майкрософт недоступны в Azure по умолчанию. Если ваша роль использует такую платформу, необходимо добавить эти сборки toohello приложения.

Перед выполнением сборки и пакет приложения, проверьте следующие hello.

* Если с помощью Visual studio, убедитесь, что hello **Копировать локально** задано слишком**True** для каждой связанной сборки в проекте, который не является частью hello Azure SDK или hello .NET Framework.
* Убедитесь, что файл web.config hello не ссылается на все неиспользуемые сборки из элемент compilation hello.
* Hello **действие при построении** каждого cshtml файла задано слишком**содержимого**. Это гарантирует, что файлы hello правильно отображались hello пакета и позволяет tooappear других файлов в пакете hello.

## <a name="assembly-targets-wrong-platform"></a>Сборка нацелена на неверную платформу.
Azure является 64-разрядной средой. Таким образом, сборки .NET, скомпилированные для 32-разрядной среды, не будут работать в Azure.

## <a name="role-throws-unhandled-exceptions-while-initializing-or-stopping"></a>Роль вызывает необработанные исключения во время инициализации или остановки.
Любые исключения, вызванные методами "hello" hello [RoleEntryPoint] класса, содержащего hello [OnStart], [OnStop], и [запуска]метода, являются необработанными исключениями. Если обнаруживается необработанное исключение в одном из этих методов, hello роль будет перезапущена. Если hello роль постоянно перезапускается, может вызывает необработанное исключение каждый раз, он пробует toostart.

## <a name="role-returns-from-run-method"></a>Роль возвращается из метода Run.
Hello [запуска] метод является предполагаемым toorun бесконечно. Если код переопределяет hello [запуска] метод, он должен перейти в режим бесконечно. Если hello [запуска] метод возвращает hello роль перезапускается.

## <a name="incorrect-diagnosticsconnectionstring-setting"></a>Неверный параметр DiagnosticsConnectionString
Если приложение использует диагностику Azure, в файле конфигурации службы необходимо указать hello `DiagnosticsConnectionString` параметр конфигурации. Этот параметр следует указать учетную запись хранилища tooyour соединения HTTPS в Azure.

tooensure, ваш `DiagnosticsConnectionString` значение является правильным, перед развертыванием пакета вашего приложения tooAzure, проверьте следующие hello:  

* Hello `DiagnosticsConnectionString` задания точек tooa действительную учетную запись хранилища в Azure.  
  По умолчанию этот параметр указывает toohello эмулированной учетной записи хранилища, поэтому его необходимо явно изменить этот параметр, перед развертыванием пакета приложения. Если этот параметр не изменяются, когда экземпляр роли hello пытается монитор диагностики hello toostart создается исключение. Это может привести к toorecycle экземпляр роли hello бесконечно.
* Hello указана строка подключения в hello ниже [формат](../storage/common/storage-configure-connection-string.md). (hello необходимо указать протокол как HTTPS.) Замените *MyAccountName* с именем hello вашей учетной записи хранилища и *MyAccountKey* с помощью ключа доступа:    

        DefaultEndpointsProtocol=https;AccountName=MyAccountName;AccountKey=MyAccountKey

  При разработке приложения с помощью средств Azure для Microsoft Visual Studio, можно использовать tooset страниц свойств hello, это значение.

## <a name="exported-certificate-does-not-include-private-key"></a>Экспортированный сертификат не содержит закрытый ключ.
toorun SSL веб-роли, необходимо убедиться, ваш экспортированный сертификат управления включает hello закрытый ключ. При использовании hello *диспетчера сертификатов Windows* tooexport hello сертификата, быть убедиться, что tooselect **Да** для hello **экспорта hello закрытый ключ** параметр. Hello сертификат необходимо экспортировать в формате PFX hello, который в настоящее время поддерживается только формат hello.

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите дополнительные [статьи об устранении неполадок](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) в облачных службах.

Дополнительные сценарии перезапуска ролей см. в [серии статей в блоге Кевина Уильямсона](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

[RoleEntryPoint]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx
[OnStart]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx
[OnStop]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx
[запуска]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx
