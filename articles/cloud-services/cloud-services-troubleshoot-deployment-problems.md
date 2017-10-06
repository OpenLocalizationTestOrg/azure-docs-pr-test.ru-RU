---
title: "проблемы развертывания aaaTroubleshoot облачные службы | Документы Microsoft"
description: "Существует несколько распространенных проблем, которые вы можете столкнуться при развертывании tooAzure облачной службы. Эта статья содержит toosome решения из них."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: a18ae415-0d1c-4bc4-ab6c-c1ddea02c870
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 15aea4f2b2913d95f3378b2e9762b232531f3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a>Устранение неполадок, которые могут возникнуть при развертывании облачной службы
При развертывании облачной службы приложения пакета tooAzure, можно получить сведения о развертывании hello из hello **свойства** панели hello портал Azure. Можно использовать hello сведения в этой области toohelp диагностировать неполадки с hello облачной службы, и это tooAzure сведения поддержки можно задать при открытии нового запроса на обслуживание.

Можно найти hello **свойства** области следующим образом:

* В hello портал Azure, щелкните hello развертывания облачной службы, **все параметры**, а затем нажмите кнопку **свойства**.
* В hello классический портал Azure, щелкните hello развертывания облачной службы, **МОНИТОРИНГА**, расположенную в правом нижнем углу hello страницы приветствия (под **быстрый обзор**). Имейте в виду, что на этой панели отсутствует метка "Свойства".

> [!NOTE]
> Можно скопировать содержимое hello hello **свойства** буфера обмена toohello панели, щелкнув значок hello в hello правом верхнем углу панели «hello».
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a>Проблема: у меня нет доступа к моему веб-сайту, но мое развертывание запущено и все экземпляры роли готовы
ссылку URL-адрес веб-сайта Hello, отображаются на портале hello не входит порт hello. Hello по умолчанию для веб-сайтов используется порт 80. Если приложение является настроенным toorun в другой порт, необходимо добавить hello правильный порт номер toohello URL-адрес при доступе к веб-сайт hello.

1. В hello портал Azure щелкните hello развертывания облачной службы.
2. В hello **свойства** области hello портал Azure, проверьте hello порты для экземпляров роли hello (под **конечные точки ввода**).
3. Если порт hello не 80, добавьте hello правильный порт значение toohello URL при доступе к приложения hello. toospecify нестандартный порт, введите URL-адрес hello, за которым следует двоеточие (:), за которым следует номер порта hello, без пробелов.

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a>Проблема: мои экземпляры ролей перезапускаются автоматически
Восстановление службы происходит автоматически, когда Azure обнаруживает проблему узлов и поэтому перемещает узлы toonew экземпляров роли. В этом случае экземпляры ролей могут перезапускаться автоматически. Восстановление произошла службы toofind ли:

1. В hello портал Azure щелкните hello развертывания облачной службы.
2. В hello **свойства** области hello портал Azure, просмотрите сведения hello и определить, после восстановления службы возникло во время hello, вы заметили перезапуск роли hello.

Кроме того, роли перезапускаются примерно раз в месяц, когда обновляются ОС узла и гостевая ОС.  
Дополнительные сведения см. в статье блога hello [роли экземпляра перезапускается из-за обновления tooOS](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a>Проблема: когда я пробую переключить виртуальный IP-адрес, отображается сообщение об ошибке
Переключение виртуального IP-адреса не допускается, если развертывание обновляется. Развертывание обновляется автоматически в таких случаях:

* доступна новая операционная система на виртуальной машине и на вашем устройстве настроено автоматическое обновление;
* выполняется восстановление службы.

toofind, если автоматическое обновление мешает переключения виртуального IP-адреса:

1. В hello портал Azure щелкните hello развертывания облачной службы.
2. В hello **свойства** области hello портал Azure, посмотрите значение hello **состояние**. Если это **готов**, затем проверьте **последней операции** toosee Если, выполнялась и, возможно swap hello виртуальных IP-адресов.
3. Повторите шаги 1 и 2 для рабочего развертывания hello.
4. Если автоматическое обновление находится в процессе, дождитесь его toofinish перед попытке замены toodo hello виртуальных IP-адресов.

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a>Проблема: экземпляр роли циклически переключается между состояниями «Запущено», «Инициализация», «Занято» и «Остановлено»
Это может указывать на проблему с кодом, пакетом или файлом конфигурации приложения. В этом случае должно быть состояние hello toosee может меняться каждые несколько минут и hello портал Azure может говориться примерно **перезапуск**, **Busy**, или **Initializing**. Это указывает на наличие ошибки hello приложением, что запуск экземпляра роли hello.

Дополнительные сведения о том, как tootroubleshoot эту проблему, см. hello блога [Azure диагностические данные PaaS](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) и [распространенные проблемы, причина ролей toorecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

## <a name="problem-my-application-stopped-working"></a>Проблема: мое приложение перестало работать
1. В hello портал Azure щелкните экземпляр роли hello.
2. В hello **свойства** области hello портал Azure, рассмотрим следующие условия tooresolve hello проблемы:
   * Если экземпляр роли hello недавно был остановлен (можно проверить значение hello **счетчик прерываний**), может обновлять hello развертывания. Подождите toosee, если экземпляр роли hello возобновляет работу самостоятельно.
   * Если экземпляр роли hello **Busy**, проверьте toosee код вашего приложения, если hello [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) обработано событие. Может потребоваться tooadd или исправить определенный код, который обрабатывает это событие.
   * Пройти hello диагностических данных и устранения неполадок в записи блога hello [Azure диагностические данные PaaS](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

> [!WARNING]
> При восстановлении облачной службы, сброс свойств hello hello развертывания, что удалит сведения hello hello исходной проблеме.
>
>

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите дополнительные [статьи об устранении неполадок](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) в облачных службах.

toolearn как проблемы tootroubleshoot роль облачной службы с помощью диагностические данные Azure PaaS компьютера, в разделе [серии публикаций в блоге Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
