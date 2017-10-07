---
title: "aaaTroubleshoot ролей, которые не toostart | Документы Microsoft"
description: "Ниже приведены наиболее распространенные причины, почему роли облачной службы может завершиться ошибкой toostart. Также предоставляются toothese решения проблемы."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a>Устранение неполадок ролей облачной службы, которые не toostart
Ниже приведены некоторые распространенные проблемы и решения связанных tooAzure облачные службы ролей, которые не toostart.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a>Отсутствующие DLL-библиотеки и зависимости
Если роли не отвечают или циклически переключаются между состояниями **Инициализация**, **Занято** и **Остановка**, это может быть вызвано отсутствием сборок или библиотек DLL.

Симптомы отсутствия сборок и библиотек DLL могут быть такими:

* Экземпляр роли циклически переключается между состояниями **Инициализация**, **Занято** и **Остановка**.
* Экземпляр роли перемещено слишком**готовности** , но при переходе tooyour веб-приложение hello страница не отображается.

Эти проблемы можно решить несколькими способами.

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a>Диагностика неполадок в связи с отсутствующими библиотеками DLL в веб-роли
Когда перейдите tooa веб-сайт, который развертывается на веб-роли и hello браузер отображает сервера ошибка аналогичные toohello ниже, это может указывать, что библиотека DLL отсутствует.

![Ошибка сервера в приложении «/».](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a>Диагностика проблем с помощью отключения режима настраиваемых ошибок
Более полные сведения об ошибке можно просмотреть, настроив файл web.config hello для hello tooset роли web hello tooOff режим пользовательских ошибок и повторного развертывания службы hello.

tooview более выполните ошибки без использования удаленного рабочего стола.

1. Откройте решение hello в Microsoft Visual Studio.
2. В hello **обозревателе решений**hello файл web.config и откройте его.
3. В файле web.config hello найдите раздел system.web hello и добавьте hello, следующей строкой:

    ```xml
    <customErrors mode="Off" />
    ```
4. Сохраните файл hello.
5. Упакуйте и повторно разверните службу hello.

После развертывания службы hello, вы увидите сообщение об ошибке с именем hello hello отсутствующих сборок или библиотек DLL.

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a>Диагностировать проблемы, просмотрев ошибки hello удаленно
Можно использовать удаленный рабочий стол tooaccess hello роли и удаленно просматривать более полные сведения об ошибке. Используйте следующие шаги tooview hello ошибки с помощью удаленного рабочего стола hello.

1. Убедитесь, что установлен пакет SDK для Azure версии 1.3 или более поздней.
2. Слишком во время развертывания hello hello решения с помощью Visual Studio, выберите «Настроить удаленный рабочий стол подключений...». Дополнительные сведения о настройке подключения удаленного рабочего стола hello см. в разделе [использование удаленного рабочего стола с ролями Azure](../vs-azure-tools-remote-desktop-roles.md).
3. Hello Microsoft Azure классическом портале, как только состояние экземпляра hello **готовности**, выберите один из экземпляров роли hello.
4. Нажмите кнопку hello **Connect** значок в hello **удаленного доступа** ленте hello.
5. Войдите в toohello виртуальной машины с помощью hello учетные данные, которые были указаны во время настройки удаленного рабочего стола hello.
6. Откройте командное окно.
7. Введите `IPconfig`.
8. Запомните значение IPV4-адрес hello.
9. Откройте браузер Internet Explorer.
10. Введите адрес hello и имя hello hello веб-приложения. Например, `http://<IPV4 Address>/default.aspx`.

Навигация по toohello веб-сайта теперь возвращают более подробные сообщения об ошибке.

* Ошибка сервера в приложении «/».
* Описание: Необработанное исключение произошло во время выполнения hello hello текущего веб-запроса. Просмотрите трассировку стека hello Дополнительные сведения об ошибке hello и где он находится в коде hello.
* Сведения об исключении: System.IO.FIleNotFoundException: не удалось загрузить файл, сборку Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35 или какую-то их зависимость. Hello системе не удается найти указанный файл hello.

Например:

![Явная ошибка сервера в приложении «/».](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a>Диагностика проблем с помощью эмулятора вычислений hello
Можно использовать toodiagnose эмулятор вычислений Microsoft Azure hello и устранения проблем с отсутствующими зависимостями и ошибок в файле web.config.

Чтобы улучшить результаты использования этого метода диагностики, следует использовать компьютер или виртуальную машину, на которой выполнена чистая установка Windows. toobest имитировать hello среды Azure, используйте Windows Server 2008 R2 x64.

1. Установите автономную версию hello hello [пакета Azure SDK](https://azure.microsoft.com/downloads/).
2. На компьютере для разработки hello построение проекта облачной службы hello.
3. В проводнике Windows перейдите toohello папку bin\debug проекта облачной службы hello.
4. Скопируйте папку .csx hello и .cscfg файл toohello компьютер, что вы используете toodebug hello проблемы.
5. На hello очистки компьютера, откройте окно командной строки Azure SDK и введите `csrun.exe /devstore:start`.
6. Введите в командной строке hello `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.
7. При запуске роли hello, вы увидите подробные сведения об ошибке в Internet Explorer. Можно также использовать стандартные средства устранения неполадок Windows toofurther диагностировать проблему hello.

## <a name="diagnose-issues-by-using-intellitrace"></a>Диагностика неполадок с помощью IntelliTrace
Для рабочих ролей и веб-ролей, которые используют платформу .NET Framework 4, можно использовать функцию [EnterpriseIntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), доступную в Microsoft Visual Studio Enterprise.

Выполните эти шаги toodeploy hello службы с включенным компонентом IntelliTrace.

1. Убедитесь, что установлен пакет SDK для Azure версии 1.3 или более поздней.
2. Развертывание решения hello с помощью Visual Studio. Во время развертывания, проверьте hello **включить IntelliTrace для ролей .NET 4** флажок.
3. После запуска экземпляра hello, откройте hello **обозревателя серверов**.
4. Разверните hello **Azure\\облачные службы** узла и найдите развертывание hello.
5. Расширяйте развертывание hello, пока не увидите hello экземпляров роли. Щелкните правой кнопкой мыши один из экземпляров hello.
6. Выберите элемент **Просмотр журналов IntelliTrace**. Hello **Сводка IntelliTrace** будет открыт.
7. Найдите раздел исключений hello hello сводки. Если существуют исключения, будет называться hello раздел **данные исключения**.
8. Разверните hello **данные исключения** и выполните поиск **System.IO.FileNotFoundException** аналогичные toohello следующие ошибки:

![Данные исключения, отсутствующий файл или сборка](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a>Устранение ошибок из-за отсутствующих библиотек DLL и сборок
tooaddress отсутствует DLL и сборок ошибки, выполните следующие действия.

1. Откройте решение hello в Visual Studio.
2. В **обозревателе решений**откройте hello **ссылки** папки.
3. Щелкните сборку hello, указанную в ошибке hello.
4. В hello **свойства** панели найдите **свойства Copy Local** и задайте значение hello слишком**True**.
5. Повторное развертывание hello облачной службы.

После проверки того, что все ошибки исправлены, вы можете развернуть службу hello без проверки hello **включить IntelliTrace для ролей .NET 4** флажок.

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите дополнительные [статьи об устранении неполадок](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) в облачных службах.

toolearn как проблемы tootroubleshoot роль облачной службы с помощью диагностические данные Azure PaaS компьютера, в разделе [серии публикаций в блоге Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
