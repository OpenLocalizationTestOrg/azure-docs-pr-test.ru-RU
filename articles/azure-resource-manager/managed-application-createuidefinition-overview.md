---
title: "Создание определения пользовательского интерфейса для управляемого приложения Azure aaaUnderstand | Документы Microsoft"
description: "Описывает способ определения toocreate пользовательского интерфейса для управляемого приложения Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a>Начало работы с CreateUiDefinition
В этом документе понятия hello core CreateUiDefinition, который используется для создания управляемого приложения hello Azure портала toogenerate hello пользовательским интерфейсом.

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

CreateUiDefinition всегда содержит три свойства: 

* handler;
* версия
* parameters

Для управляемых приложений обработчик должен всегда быть `Microsoft.Compute.MultiVm`, hello последние поддерживаемые версии и `0.1.2-preview`.

Схема Hello hello свойства параметров зависит от сочетание hello указанного обработчика hello и версии. Для управляемых приложений hello поддерживается свойства являются `basics`, `steps`, и `outputs`. Hello основы и действия свойства содержат hello _элементы_ - например, текстовые поля и раскрывающиеся меню - toobe отображаются в hello портал Azure. Hello результатов, которые оно используется toomap hello выходные значения hello указанные элементы toohello параметров шаблона развертывания диспетчера ресурсов Azure hello.

Советуем также использовать параметр `$schema`, но это необязательно. Если указано, hello значение `version` должна совпадать с версией hello в hello `$schema` URI.

## <a name="basics"></a>Основы
Основы шаг Hello всегда является этапом hello приветствия мастера создается при CreateUiDefinition анализирует hello портал Azure. В дополнение к этому toodisplaying hello указываются в `basics`, портал hello вставляет элементы для подписки hello toochoose пользователи, группы ресурсов и расположение для развертывания hello. Как правило элементы, которые запрос для всего развертывания параметров, как hello имя кластера или администратор учетных данных, следует перейти на этом шаге.

Если поведение элемента зависит от подписки, группы ресурсов или расположения hello пользователя, этот элемент не может использоваться в основы. Например **Microsoft.Compute.SizeSelector** зависит от пользователя hello подписке и расположении toodetermine hello список доступных размеров. Таким образом, **Microsoft.Compute.SizeSelector** может использоваться только в steps. Как правило, только элементы hello **Microsoft.Common** пространства имен можно использовать в основы. Несмотря на то что некоторые элементы в других пространствах имен (таких как **Microsoft.Compute.Credentials**), которые не зависят от контекста пользователя hello, по-прежнему разрешены.

## <a name="steps"></a>Действия
Свойство действия Hello может содержать ноль или более toodisplay дополнительные действия после основные, каждый из которых содержит один или несколько элементов. Рассмотрите возможность добавления действия в каждой роли или уровня развертываемое приложение hello. Например добавьте шаг для входных данных для главных узлов hello и шаг для hello рабочих узлов в кластере.

## <a name="outputs"></a>outputs
Hello портал Azure использует hello `outputs` toomap элементы свойств из `basics` и `steps` toohello параметров шаблона развертывания диспетчера ресурсов Azure hello. Hello ключи данного словаря — hello имена параметров шаблона hello и hello значения являются свойствами объектов hello выходные данные из hello ссылки на элементы.

## <a name="functions"></a>Функции
Аналогичные слишком[функции шаблона](resource-group-template-functions.md) в диспетчере ресурсов Azure (как в синтаксис и функции), CreateUiDefinition предоставляет функции для работы с входными и выходными данными элементов, а также функции, например, условные выражения.

## <a name="next-steps"></a>Дальнейшие действия
CreateUiDefinition имеет простую схему. Hello реальные глубину он поступает из все элементы hello поддерживается и функции, удивительное подробного описания какие hello следующие документы:

- [CreateUiDefinition elements](managed-application-createuidefinition-elements.md) (Элементы CreateUiDefinition)
- [Функции](managed-application-createuidefinition-functions.md)

Текущая схема JSON для CreateUiDefinition доступна здесь: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json. 

Более поздние версии можно найти по адресу hello местоположения. Замените hello `0.1.2-preview` часть URL-адрес hello и hello `version` значение с идентификатором hello версии планируется toouse. идентификаторы Hello в настоящее время поддерживается версия `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, и `0.1.2-preview`.
