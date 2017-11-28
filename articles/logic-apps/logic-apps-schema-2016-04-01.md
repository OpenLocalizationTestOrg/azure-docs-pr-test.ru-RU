---
title: "Обновления схемы от 1 июня 2016 г. Azure Logic Apps | Документация Майкрософт"
description: "Создание определений JSON для Azure Logic Apps с версией схемы 2016-06-01"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/25/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 43df04d6478e44c82c88b17d916cfc9fe4afc03e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a><span data-ttu-id="61f6c-103">Обновления схемы для Azure Logic Apps от 1 июня 2016 г.</span><span class="sxs-lookup"><span data-stu-id="61f6c-103">Schema updates for Azure Logic Apps - June 1, 2016</span></span>

<span data-ttu-id="61f6c-104">Эта новая версия схемы и API для Azure Logic Apps включает основные улучшения, которые повышают надежность и простоту использования приложений логики.</span><span class="sxs-lookup"><span data-stu-id="61f6c-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

* <span data-ttu-id="61f6c-105">[Области](#scopes) позволяют группировать или вкладывать действия в виде набора действий.</span><span class="sxs-lookup"><span data-stu-id="61f6c-105">[Scopes](#scopes) let you group or nest actions as a collection of actions.</span></span>
* <span data-ttu-id="61f6c-106">[Условия и циклы](#conditions-loops) — это действия первого класса.</span><span class="sxs-lookup"><span data-stu-id="61f6c-106">[Conditions and loops](#conditions-loops) are now first-class actions.</span></span>
* <span data-ttu-id="61f6c-107">Более точный порядок выполняющихся действий со свойством `runAfter` вместо `dependsOn`.</span><span class="sxs-lookup"><span data-stu-id="61f6c-107">More precise ordering for running actions with the `runAfter` property, replacing `dependsOn`</span></span>

<span data-ttu-id="61f6c-108">Сведения об обновлении приложений логики с предварительной версии схемы от 1 августа 2015 г. до схемы от 1 июня 2016 г. см. в [соответствующем разделе](##upgrade-your-schema).</span><span class="sxs-lookup"><span data-stu-id="61f6c-108">To upgrade your logic apps from the August 1, 2015 preview schema to the June 1, 2016 schema, [check out the upgrade section](##upgrade-your-schema).</span></span>

<a name="scopes"></a>
## <a name="scopes"></a><span data-ttu-id="61f6c-109">Области действия</span><span class="sxs-lookup"><span data-stu-id="61f6c-109">Scopes</span></span>

<span data-ttu-id="61f6c-110">Эта схема включает области, позволяющие группировать несколько действий или вложить одно действие в другое.</span><span class="sxs-lookup"><span data-stu-id="61f6c-110">This schema includes scopes, which let you group actions together, or nest actions inside each other.</span></span> <span data-ttu-id="61f6c-111">Например, одно условие может содержать в себе другое условие.</span><span class="sxs-lookup"><span data-stu-id="61f6c-111">For example, a condition can contain another condition.</span></span> <span data-ttu-id="61f6c-112">Узнайте больше о [синтаксисе областей](../logic-apps/logic-apps-loops-and-scopes.md) или просмотрите базовый пример области, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="61f6c-112">Learn more about [scope syntax](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic scope example:</span></span>

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>
## <a name="conditions-and-loops-changes"></a><span data-ttu-id="61f6c-113">Изменения в условиях и циклах</span><span class="sxs-lookup"><span data-stu-id="61f6c-113">Conditions and loops changes</span></span>

<span data-ttu-id="61f6c-114">В предыдущих версиях схемы условия и циклы были параметрами, связанными с каким-то одним действием.</span><span class="sxs-lookup"><span data-stu-id="61f6c-114">In previous schema versions, conditions and loops were parameters associated with a single action.</span></span> <span data-ttu-id="61f6c-115">В этой схеме отсутствует такое ограничение, поэтому условия и циклы теперь отображаются как типы действий.</span><span class="sxs-lookup"><span data-stu-id="61f6c-115">This schema lifts this limitation, so conditions and loops now appear as action types.</span></span> <span data-ttu-id="61f6c-116">Узнайте больше о [циклах и областях](../logic-apps/logic-apps-loops-and-scopes.md) или просмотрите этот базовый пример условия:</span><span class="sxs-lookup"><span data-stu-id="61f6c-116">Learn more about [loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md), or review this basic example for a condition action:</span></span>

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>
## <a name="runafter-property"></a><span data-ttu-id="61f6c-117">Свойство runAfter</span><span class="sxs-lookup"><span data-stu-id="61f6c-117">'runAfter' property</span></span>

<span data-ttu-id="61f6c-118">Свойство `runAfter` заменяет свойство `dependsOn`, обеспечивая более точный порядок выполнения действий на основе состояния предыдущих действий.</span><span class="sxs-lookup"><span data-stu-id="61f6c-118">The `runAfter` property replaces `dependsOn`, providing more precision when you specify the run order for actions based on the status of previous actions.</span></span>

<span data-ttu-id="61f6c-119">Свойство `dependsOn` означало "действие запущено и успешно выполнено" независимо от того, сколько раз нужно выполнить действие и каким было завершение предыдущего действия: успешным, неудавшимся или пропущенным.</span><span class="sxs-lookup"><span data-stu-id="61f6c-119">The `dependsOn` property was synonymous with "the action ran and was successful", no matter how many times you wanted to execute an action, based on whether the previous action was successful, failed, or skipped.</span></span> <span data-ttu-id="61f6c-120">Свойство `runAfter` обеспечивает нужную гибкость в виде объекта, который указывает все имена действий, а затем выполняется.</span><span class="sxs-lookup"><span data-stu-id="61f6c-120">The `runAfter` property provides that flexibility as an object that specifies all the action names after which the object runs.</span></span> <span data-ttu-id="61f6c-121">Оно также определяет массив состояний, которые можно использовать в качестве триггеров.</span><span class="sxs-lookup"><span data-stu-id="61f6c-121">This property also defines an array of statuses that are acceptable as triggers.</span></span> <span data-ttu-id="61f6c-122">Например, если вы хотите выполнить активацию после успешного завершения действия A и успешного завершения или сбоя действия B, требуется такое свойство `runAfter`:</span><span class="sxs-lookup"><span data-stu-id="61f6c-122">For example, if you wanted to run after step A succeeds and also after step B succeeds or fails, you construct this `runAfter` property:</span></span>

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a><span data-ttu-id="61f6c-123">Обновление схемы</span><span class="sxs-lookup"><span data-stu-id="61f6c-123">Upgrade your schema</span></span>

<span data-ttu-id="61f6c-124">Выполнить обновление схемы до новой версии очень просто.</span><span class="sxs-lookup"><span data-stu-id="61f6c-124">Upgrading to the new schema only takes a few steps.</span></span> <span data-ttu-id="61f6c-125">Вот что входит в процесс обновления: запуск скрипта обновления, сохранение в качестве нового приложения логики и, если нужно, перезапись предыдущего приложения логики.</span><span class="sxs-lookup"><span data-stu-id="61f6c-125">The upgrade process includes running the upgrade script, saving as a new logic app, and if you want, possibly overwriting the previous logic app.</span></span>

1. <span data-ttu-id="61f6c-126">Откройте приложение логики на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="61f6c-126">In the Azure portal, open your logic app.</span></span>

2. <span data-ttu-id="61f6c-127">Перейдите на вкладку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="61f6c-127">Go to **Overview**.</span></span> <span data-ttu-id="61f6c-128">На панели инструментов приложения логики выберите **Обновить схему**.</span><span class="sxs-lookup"><span data-stu-id="61f6c-128">On the logic app toolbar, choose **Update Schema**.</span></span>
   
    ![Выбор параметра "Обновить схему"][1]
   
    <span data-ttu-id="61f6c-130">Обновленное определение возвращается. При необходимости его можно скопировать и вставить в определение ресурса.</span><span class="sxs-lookup"><span data-stu-id="61f6c-130">The upgraded definition is returned, which you can copy and paste into a resource definition if necessary.</span></span> 
    <span data-ttu-id="61f6c-131">Однако мы **настоятельно рекомендуем** нажать кнопку **Сохранить как**, чтобы в обновленном приложении логики все ссылки на подключение были рабочими.</span><span class="sxs-lookup"><span data-stu-id="61f6c-131">However, we **strongly recommend** you choose **Save As** to make sure that all connection references are valid in the upgraded logic app.</span></span>

3. <span data-ttu-id="61f6c-132">Нажмите кнопку **Сохранить как** на панели инструментов колонки обновления.</span><span class="sxs-lookup"><span data-stu-id="61f6c-132">In the upgrade blade toolbar, choose **Save As**.</span></span>

4. <span data-ttu-id="61f6c-133">Введите имя и состояние логики.</span><span class="sxs-lookup"><span data-stu-id="61f6c-133">Enter the logic name and status.</span></span> <span data-ttu-id="61f6c-134">Чтобы развернуть обновленное приложение логики, выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="61f6c-134">To deploy your upgraded logic app, choose **Create**.</span></span>

5. <span data-ttu-id="61f6c-135">Убедитесь, что обновленное приложение логики работает правильно.</span><span class="sxs-lookup"><span data-stu-id="61f6c-135">Confirm that your upgraded logic app works as expected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="61f6c-136">Если вы используете триггер запуска вручную или триггер запроса, в новом приложении логики URL-адрес обратного вызова будет новым.</span><span class="sxs-lookup"><span data-stu-id="61f6c-136">If you are using a manual or request trigger, the callback URL changes in your new logic app.</span></span> <span data-ttu-id="61f6c-137">Проверьте новый URL-адрес, чтобы убедиться, что приложение работает полноценно.</span><span class="sxs-lookup"><span data-stu-id="61f6c-137">Test the new URL to make sure the end-to-end experience works.</span></span> <span data-ttu-id="61f6c-138">Вы можете клонировать имеющееся приложение логики, чтобы сохранить предыдущие URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="61f6c-138">To preserve previous URLs, you can clone over your existing logic app.</span></span>

6. <span data-ttu-id="61f6c-139">*Необязательно.* Чтобы перезаписать предыдущее приложение логики, заменив его новой версией схемы, щелкните **Клонировать** на панели инструментов возле значка **Обновить схему**.</span><span class="sxs-lookup"><span data-stu-id="61f6c-139">*Optional* To overwrite your previous logic app with the new schema version, on the toolbar, choose **Clone**, next to **Update Schema**.</span></span> <span data-ttu-id="61f6c-140">Этот шаг необходим, только если нужно сохранить код ресурса или URL-адрес триггера запроса вашего приложения логики.</span><span class="sxs-lookup"><span data-stu-id="61f6c-140">This step is necessary only if you want to keep the same resource ID or request trigger URL of your logic app.</span></span>

### <a name="upgrade-tool-notes"></a><span data-ttu-id="61f6c-141">Примечания о средстве обновления</span><span class="sxs-lookup"><span data-stu-id="61f6c-141">Upgrade tool notes</span></span>

#### <a name="mapping-conditions"></a><span data-ttu-id="61f6c-142">Условия сопоставления</span><span class="sxs-lookup"><span data-stu-id="61f6c-142">Mapping conditions</span></span>

<span data-ttu-id="61f6c-143">В обновленном определении это средство в качестве области максимально эффективно собирает вместе действия ветвления true и false.</span><span class="sxs-lookup"><span data-stu-id="61f6c-143">In the upgraded definition, the tool makes a best effort at grouping true and false branch actions together as a scope.</span></span> <span data-ttu-id="61f6c-144">В частности, шаблон конструктора `@equals(actions('a').status, 'Skipped')` должен отображаться как действие `else`.</span><span class="sxs-lookup"><span data-stu-id="61f6c-144">Specifically, the designer pattern of `@equals(actions('a').status, 'Skipped')` should appear as an `else` action.</span></span> <span data-ttu-id="61f6c-145">Но если средство обнаруживает нераспознаваемые шаблоны, оно создает отдельные условия для ветвей true и false.</span><span class="sxs-lookup"><span data-stu-id="61f6c-145">However, if the tool detects unrecognizable patterns, the tool might create separate conditions for both the true and the false branch.</span></span> <span data-ttu-id="61f6c-146">При необходимости можно сопоставить действия после обновления.</span><span class="sxs-lookup"><span data-stu-id="61f6c-146">You can remap actions after upgrading, if necessary.</span></span>

#### <a name="foreach-loop-with-condition"></a><span data-ttu-id="61f6c-147">Цикл foreach с условием</span><span class="sxs-lookup"><span data-stu-id="61f6c-147">'foreach' loop with condition</span></span>

<span data-ttu-id="61f6c-148">В новой схеме можно использовать действие фильтра для репликации шаблона цикла `foreach` с одним условием на элемент, но в то же время это изменение должно автоматически выполняться при обновлении.</span><span class="sxs-lookup"><span data-stu-id="61f6c-148">In the new schema, you can use the filter action to replicate the pattern of a `foreach` loop with a condition per item, but this change should automatically happen when you upgrade.</span></span> <span data-ttu-id="61f6c-149">Условие становится действием фильтра до запуска цикла foreach, чтобы вернулся только массив элементов, которые соответствуют условию. Этот массив передается в действие foreach.</span><span class="sxs-lookup"><span data-stu-id="61f6c-149">The condition becomes a filter action before the foreach loop for returning only an array of items that match the condition, and that array is passed into the foreach action.</span></span> <span data-ttu-id="61f6c-150">Пример см. в статье [Циклы, области действия и индивидуальная обработка приложений логики](../logic-apps/logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="61f6c-150">For an example, see [Loops and scopes](../logic-apps/logic-apps-loops-and-scopes.md).</span></span>

#### <a name="resource-tags"></a><span data-ttu-id="61f6c-151">Теги ресурсов</span><span class="sxs-lookup"><span data-stu-id="61f6c-151">Resource tags</span></span>

<span data-ttu-id="61f6c-152">После обновления теги ресурсов удаляются, поэтому их нужно сбросить для обновленного рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="61f6c-152">After you upgrade, resource tags are removed, so you must reset them for the upgraded workflow.</span></span>

## <a name="other-changes"></a><span data-ttu-id="61f6c-153">Другие изменения</span><span class="sxs-lookup"><span data-stu-id="61f6c-153">Other changes</span></span>

### <a name="renamed-manual-trigger-to-request-trigger"></a><span data-ttu-id="61f6c-154">Переименование триггера запуска вручную на триггер запроса</span><span class="sxs-lookup"><span data-stu-id="61f6c-154">Renamed 'manual' trigger to 'request' trigger</span></span>

<span data-ttu-id="61f6c-155">Тип триггера `manual` устарел, поэтому он переименован на `request` с типом `http`.</span><span class="sxs-lookup"><span data-stu-id="61f6c-155">The `manual` trigger type was deprecated and renamed to `request` with type `http`.</span></span> <span data-ttu-id="61f6c-156">Это изменение лучше соответствует типу шаблона, для построения которого используется триггер.</span><span class="sxs-lookup"><span data-stu-id="61f6c-156">This change creates more consistency for the kind of pattern that the trigger is used to build.</span></span>

### <a name="new-filter-action"></a><span data-ttu-id="61f6c-157">Новое действие "фильтр"</span><span class="sxs-lookup"><span data-stu-id="61f6c-157">New 'filter' action</span></span>

<span data-ttu-id="61f6c-158">Для фильтрации большого массива в меньший набор элементов новый тип `filter` принимает массив и условие, оценивает соответствие каждого элемента условию и возвращает только те элементы, которые соответствуют условию.</span><span class="sxs-lookup"><span data-stu-id="61f6c-158">To filter a large array down to a smaller set of items, the new `filter` type accepts an array and a condition, evaluates the condition for each item, and returns an array with items meeting the condition.</span></span>

### <a name="restrictions-for-foreach-and-until-actions"></a><span data-ttu-id="61f6c-159">Ограничения действий foreach и until</span><span class="sxs-lookup"><span data-stu-id="61f6c-159">Restrictions for 'foreach' and 'until' actions</span></span>

<span data-ttu-id="61f6c-160">Циклы `foreach` и `until` ограничены одним действием.</span><span class="sxs-lookup"><span data-stu-id="61f6c-160">The `foreach` and `until` loop are restricted to a single action.</span></span>

### <a name="new-trackedproperties-for-actions"></a><span data-ttu-id="61f6c-161">Новое свойство trackedProperties для действий</span><span class="sxs-lookup"><span data-stu-id="61f6c-161">New 'trackedProperties' for actions</span></span>

<span data-ttu-id="61f6c-162">Теперь у действий может быть дополнительное свойство (элемент того же уровня, что и `runAfter` и `type`) с именем `trackedProperties`.</span><span class="sxs-lookup"><span data-stu-id="61f6c-162">Actions can now have an additional property called `trackedProperties`, which is sibling to the `runAfter` and `type` properties.</span></span> <span data-ttu-id="61f6c-163">Этот объект указывает, что некоторые выходные или входные данные действия нужно включить в телеметрию службы диагностики Azure. Эта телеметрия отправляется в рамках рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="61f6c-163">This object specifies certain action inputs or outputs that you want to include in the Azure Diagnostic telemetry, emitted as part of a workflow.</span></span> <span data-ttu-id="61f6c-164">Например:</span><span class="sxs-lookup"><span data-stu-id="61f6c-164">For example:</span></span>

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="61f6c-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="61f6c-165">Next Steps</span></span>
* [<span data-ttu-id="61f6c-166">Создание определений приложений логики</span><span class="sxs-lookup"><span data-stu-id="61f6c-166">Create workflow definitions for logic apps</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="61f6c-167">Создание шаблона развертывания приложения логики</span><span class="sxs-lookup"><span data-stu-id="61f6c-167">Create deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
