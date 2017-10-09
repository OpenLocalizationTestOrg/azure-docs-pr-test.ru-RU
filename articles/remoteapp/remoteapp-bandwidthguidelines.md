---
title: "пропускная способность сети RemoteApp aaaAzure — Общие рекомендации | Документы Microsoft"
description: "Описание общих рекомендаций по пропускной способности сети для приложений и коллекций Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a>Пропускная способность сети Azure RemoteApp — общие рекомендации (если невозможно провести свои тесты)
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Если у вас hello hello времени или возможности toorun [тесты пропускной способности сети](remoteapp-bandwidthtests.md) для Azure RemoteApp, ниже приведены некоторые достаточно общий рекомендации, которые могут помочь оценить пропускной способности сети для каждого пользователя.

Если имеется смесь этих сценариев, мы не рекомендуем ничего не превышала (в) 10 МБИТ/с, hello минимальную пропускную способность сети для современных приложений, подключенных к Интернету, в удаленной среде. (Хотя, как уже было сказано, это обеспечивает взаимодействие с пользователем лишь на приемлемом уровне.)

## <a name="complex-powerpoint-simple-powerpoint"></a>Сложный PowerPoint, простой PowerPoint
Лучше всего Azure RemoteApp работает в локальной сети 100 МБ/с. В hello 10 МБ/s сетевого профиля при флуктуации выше 120 ms более 5%, hello пользователя будет отображаться среднее взаимодействие. На 1 МБ в секунду hello другой glaring - например, слайд-шоу, hello пользователь может не видеть анимации вообще поскольку кадры пропускаются.

## <a name="internet-explorer-mixed-pdf-pdf-text"></a>Internet Explorer, смешанный PDF, PDF, текст
Сетевой профиль 10 МБИТ/с — закрыть tooLAN по большей части. 1 МБ в секунду предоставит интерфейс ОК, несмотря на то, что возможны некоторые флуктуации когда пользователь выполняет прокрутку, пока имеются изображения на экране приветствия.

## <a name="flash-video-youtube"></a>Видео в формате Flash (YouTube)
100 МБИТ/с локальной сети обеспечивает максимальное удобство hello, допустимые (то есть вам справиться с частотой кадров hello, однако флуктуаций увеличивается) — 10 МБИТ/с. При скорости 1 МБ/с дрожание достигает очень высокого уровня и становится заметным.

## <a name="word-typing-word-remote-input"></a>Ввод в Word (удаленный ввод в Word)
Это сценарий отличается низким использованием пропускной способности. При 256 КБ/с обеспечивается качество работы, сопоставимое с локальной сетью.

## <a name="learn-more"></a>Подробнее
* [Оценка использования пропускной способности сети Azure RemoteApp](remoteapp-bandwidth.md)
* [Azure RemoteApp — как пропускная способность сети и качество взаимодействия связаны друг с другом?](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp — тест использования пропускной способности сети в рамках распространенных сценариев](remoteapp-bandwidthtests.md)

