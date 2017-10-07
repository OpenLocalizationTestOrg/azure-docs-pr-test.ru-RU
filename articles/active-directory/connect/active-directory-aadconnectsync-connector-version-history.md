---
title: "aaaConnector журнал выпуска версий | Документы Microsoft"
description: "В этом разделе перечислены все выпуски hello соединителей для Forefront Identity Manager (FIM) и Microsoft Identity Manager (MIM)"
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 3522f17c30e46542eaa367ecdefdfd2fc47f71a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="6e2fc-103">История выпусков версий соединителей</span><span class="sxs-lookup"><span data-stu-id="6e2fc-103">Connector Version Release History</span></span>
<span data-ttu-id="6e2fc-104">часто обновляются Hello соединителей для Forefront Identity Manager (FIM) и Microsoft Identity Manager (MIM).</span><span class="sxs-lookup"><span data-stu-id="6e2fc-104">hello Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="6e2fc-105">Эта статья касается только FIM и MIM.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="6e2fc-106">Установка этих соединителей не поддерживается в Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="6e2fc-107">Выпущено соединители приобретаются в AADConnect при обновлении toospecified сборки.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-107">Released Connectors are preinstalled on AADConnect when upgrading toospecified Build.</span></span>

<span data-ttu-id="6e2fc-108">В этом разделе перечислены все версии hello соединителей, которые были выпущены.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-108">This topic list all versions of hello Connectors that have been released.</span></span>

<span data-ttu-id="6e2fc-109">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="6e2fc-109">Related links:</span></span>

* [<span data-ttu-id="6e2fc-110">Скачивание последних соединителей.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="6e2fc-111">[универсальному соединителю LDAP](active-directory-aadconnectsync-connector-genericldap.md) .</span><span class="sxs-lookup"><span data-stu-id="6e2fc-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="6e2fc-112">[универсальному соединителю SQL](active-directory-aadconnectsync-connector-genericsql.md) .</span><span class="sxs-lookup"><span data-stu-id="6e2fc-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="6e2fc-113">[соединителю веб-служб](http://go.microsoft.com/fwlink/?LinkID=226245) .</span><span class="sxs-lookup"><span data-stu-id="6e2fc-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="6e2fc-114">[соединителю PowerShell](active-directory-aadconnectsync-connector-powershell.md) .</span><span class="sxs-lookup"><span data-stu-id="6e2fc-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="6e2fc-115">[соединителю Lotus Domino](active-directory-aadconnectsync-connector-domino.md) .</span><span class="sxs-lookup"><span data-stu-id="6e2fc-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="6e2fc-116">1.1.604.0 (AADConnect — ожидается выпуск)</span><span class="sxs-lookup"><span data-stu-id="6e2fc-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="6e2fc-117">Исправленные проблемы:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-117">Fixed issues:</span></span>

* <span data-ttu-id="6e2fc-118">Универсальный соединитель веб-служб:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-118">Generic Web Services:</span></span>
  * <span data-ttu-id="6e2fc-119">Устранена проблема, не позволявшая создать проект SOAP при наличии двух или более конечных точек.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="6e2fc-120">Универсальный соединитель SQL:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-120">Generic SQL:</span></span>
  * <span data-ttu-id="6e2fc-121">В операции hello импорта hello GSQL был не преобразования времени неправильно, при сохранении tooconnector пространства.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-121">In hello operation of import hello GSQL was not converting time correctly, when saved tooconnector space.</span></span> <span data-ttu-id="6e2fc-122">Hello формат даты и времени по умолчанию для пространства соединителя hello GSQL был изменен с «гггг мм дд hh:mm:ssZ» too'yyyy мм дд HH:mm:ssZ ".</span><span class="sxs-lookup"><span data-stu-id="6e2fc-122">hello default date and time format for connector space of hello GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' too'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="6e2fc-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="6e2fc-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="6e2fc-124">Исправленные проблемы:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-124">Fixed issues:</span></span>

* <span data-ttu-id="6e2fc-125">Универсальный соединитель веб-служб:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-125">Generic Web Services:</span></span>
  * <span data-ttu-id="6e2fc-126">Средство Wsconfig Hello не была правильно преобразование hello массив Json из «образец запроса» для метода службы REST hello.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-126">hello Wsconfig tool did not convert correctly hello Json array from "sample request" for hello REST service method.</span></span> <span data-ttu-id="6e2fc-127">Причиной проблем с сериализацией этот массив Json для запроса REST hello.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-127">This caused problems with serialization this Json array for hello REST request.</span></span>
  * <span data-ttu-id="6e2fc-128">Инструмент настройки соединителя веб-служб не поддерживает использование символов пробела в именах атрибутов JSON.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="6e2fc-129">Шаблон замены можно добавить вручную toohello WSConfigTool.exe.config файла, например```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="6e2fc-129">A Substitution pattern can be added manually toohello WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="6e2fc-130">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-130">Lotus Notes:</span></span>
  * <span data-ttu-id="6e2fc-131">Здравствуйте, когда параметр **Разрешить пользовательские certifiers для организации и организационных единиц** отключена, то hello соединителя завершается с ошибкой во время экспорта (обновление), после экспорта hello передаче всех атрибутов, экспортированный tooDomino, но во время hello Экспорт KeyNotFoundException возвращается tooSync.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-131">When hello option **Allow custom certifiers for Organization/Organizational Units** is disabled then hello connector fails during export (Update) After hello export flow all attributes are exported tooDomino but at hello time of export a KeyNotFoundException is returned tooSync.</span></span> 
    * <span data-ttu-id="6e2fc-132">Это происходит потому, что hello переименовать завершается с ошибкой, когда он пытается toochange различающееся имя (атрибут имени пользователя) путем изменения одного из атрибутов hello ниже:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-132">This happens because hello rename operation fails when it tries toochange DN (UserName attribute) by changing one of hello attributes below:</span></span>  
      - <span data-ttu-id="6e2fc-133">LastName</span><span class="sxs-lookup"><span data-stu-id="6e2fc-133">LastName</span></span>
      - <span data-ttu-id="6e2fc-134">FirstName</span><span class="sxs-lookup"><span data-stu-id="6e2fc-134">FirstName</span></span>
      - <span data-ttu-id="6e2fc-135">MiddleInitial;</span><span class="sxs-lookup"><span data-stu-id="6e2fc-135">MiddleInitial</span></span>
      - <span data-ttu-id="6e2fc-136">AltFullName;</span><span class="sxs-lookup"><span data-stu-id="6e2fc-136">AltFullName</span></span>
      - <span data-ttu-id="6e2fc-137">AltFullNameLanguage;</span><span class="sxs-lookup"><span data-stu-id="6e2fc-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="6e2fc-138">ou;</span><span class="sxs-lookup"><span data-stu-id="6e2fc-138">ou</span></span>
      - <span data-ttu-id="6e2fc-139">altcommonname.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-139">altcommonname</span></span>

  * <span data-ttu-id="6e2fc-140">Если параметр **Разрешить настраиваемые заверители для организации и подразделений** включен, но необходимые заверители все еще пусты, возникает исключение KeyNotFoundException.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="6e2fc-141">Улучшения</span><span class="sxs-lookup"><span data-stu-id="6e2fc-141">Enhancements:</span></span>

* <span data-ttu-id="6e2fc-142">Универсальный соединитель SQL:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-142">Generic SQL:</span></span>
  * <span data-ttu-id="6e2fc-143">**Сценарий: переработан. Реализовано:** компонент "*".</span><span class="sxs-lookup"><span data-stu-id="6e2fc-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="6e2fc-144">**Описание решения**. Изменен подход к [обработке ссылок с несколькими значениями атрибутов](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="6e2fc-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="6e2fc-145">Исправленные проблемы:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-145">Fixed issues:</span></span>

* <span data-ttu-id="6e2fc-146">Универсальный соединитель веб-служб:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-146">Generic Web Services:</span></span>
  * <span data-ttu-id="6e2fc-147">Не удается импортировать конфигурацию сервера при наличии соединителя веб-службы</span><span class="sxs-lookup"><span data-stu-id="6e2fc-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="6e2fc-148">Соединитель веб-службы не работает с несколькими веб-службами</span><span class="sxs-lookup"><span data-stu-id="6e2fc-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="6e2fc-149">Универсальный соединитель SQL:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-149">Generic SQL:</span></span>
  * <span data-ttu-id="6e2fc-150">Типы объектов не указаны для ссылочного атрибута с одним значением</span><span class="sxs-lookup"><span data-stu-id="6e2fc-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="6e2fc-151">Разностный импорт в рамках стратегии отслеживания изменений удаляет объект при удалении значения из таблицы с несколькими значениями</span><span class="sxs-lookup"><span data-stu-id="6e2fc-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="6e2fc-152">Исключение OverflowException в соединителе GSQL с использованием DB2 в AS/400</span><span class="sxs-lookup"><span data-stu-id="6e2fc-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="6e2fc-153">Lotus:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-153">Lotus:</span></span>
  * <span data-ttu-id="6e2fc-154">Добавлен параметр tooenable\disable поиск подразделений перед открытием страницы GlobalParameters</span><span class="sxs-lookup"><span data-stu-id="6e2fc-154">Added option tooenable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="6e2fc-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="6e2fc-155">1.1.443.0</span></span>

<span data-ttu-id="6e2fc-156">Дата выпуска: март 2017 г.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="6e2fc-157">Улучшения</span><span class="sxs-lookup"><span data-stu-id="6e2fc-157">Enhancements</span></span>

* <span data-ttu-id="6e2fc-158">Универсальный соединитель SQL:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-158">Generic SQL:</span></span></br><span data-ttu-id="6e2fc-159">
  **Сценарий симптомы:** это хорошо известное ограничение с hello SQL соединителя, здесь мы только разрешить tooone объекта ссылочным типом и требует перекрестная ссылка с элементами.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-159">
  **Scenario Symptoms:**  It is a well-known limitation with hello SQL Connector where we only allow a reference tooone object type and require cross reference with members.</span></span> </br><span data-ttu-id="6e2fc-160">
**Описание решения:** на этапе обработки hello для ссылок были «*» выбран параметр, все комбинации типов объектов, будет возвращено назад toohello модуль синхронизации.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-160">
**Solution description:** In hello processing step for references were "*" option is chosen, ALL combinations of object types will be returned back toohello sync engine.</span></span>

>[!Important]
- <span data-ttu-id="6e2fc-161">Будет создано множество заполнителей.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-161">This will create many placeholders</span></span>
- <span data-ttu-id="6e2fc-162">Это обязательный toomake именования hello должно быть уникальным кросс-типы объектов.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-162">It is required toomake sure hello naming is unique cross object types.</span></span>


* <span data-ttu-id="6e2fc-163">Универсальный соединитель LDAP.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-163">Generic LDAP:</span></span></br><span data-ttu-id="6e2fc-164">
 **Сценарий:** при выборе только несколько контейнеров в определенной секции, затем hello поиска по-прежнему будет выполняться в весь раздел.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-164">
**Scenario:** When only few containers are selected in specific partition, then hello search still will be done in whole partition.</span></span> <span data-ttu-id="6e2fc-165">Этот определенный раздел будет фильтроваться по службе синхронизации, а не по агенту управления, что может привести к снижению производительности.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="6e2fc-166">**Описание решения:** toomake код изменен GLDAP соединителя можно проходить через все контейнеры и выполнять поиск объектов в каждом из них, вместо поиска в секции целиком hello.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-166">**Solution description:** Changed GLDAP connector's code toomake it possible go through all containers and search objects in each of them, instead of searching in hello whole partition.</span></span>


* <span data-ttu-id="6e2fc-167">Lotus Domino.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-167">Lotus Domino:</span></span>

  <span data-ttu-id="6e2fc-168">**Сценарий.** Поддержка удаления электронной почты Domino для удаления пользователя во время экспорта.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="6e2fc-169">
  **Решение.** Настраиваемая поддержка удаления электронной почты для удаления пользователя во время экспорта.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="6e2fc-170">Исправленные проблемы:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-170">Fixed issues:</span></span>
* <span data-ttu-id="6e2fc-171">Универсальный соединитель веб-служб:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-171">Generic Web Services:</span></span>
 * <span data-ttu-id="6e2fc-172">При изменении URL-адрес службы hello в основной SAP wsconfig проекты средстве настройки веб-службы, то происходит следующая ошибка hello: не удалось найти часть пути hello</span><span class="sxs-lookup"><span data-stu-id="6e2fc-172">When changing hello service URL in Default SAP wsconfig projects through WebService Configuration Tool then hello following error happens: Could not find a part of hello path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="6e2fc-173">Универсальный соединитель LDAP.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-173">Generic LDAP:</span></span>
 * <span data-ttu-id="6e2fc-174">Соединитель GLDAP не распознает все атрибуты в AD LDS.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="6e2fc-175">Мастер Разрывы при обнаружении без имени участника-пользователя атрибутов из схемы каталога LDAP hello</span><span class="sxs-lookup"><span data-stu-id="6e2fc-175">Wizard breaks when no UPN attributes are detected from hello LDAP directory schema</span></span>
 * <span data-ttu-id="6e2fc-176">Если атрибут objectclass не выбран, операции импорта изменений завершаются с ошибками обнаружения, что не происходит во время полного импорта.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="6e2fc-177">На странице «Настройка разделов и иерархии» конфигурации, не показывает все объекты, какой тип секции равно toohello Novel серверов в универсальный hello</span><span class="sxs-lookup"><span data-stu-id="6e2fc-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal toohello partition for Novel servers in hello Generic</span></span>  
<span data-ttu-id="6e2fc-178">Агент управления LDAP.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-178">LDAP MA.</span></span> <span data-ttu-id="6e2fc-179">Отображаются только объекты из раздела RootDSE.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="6e2fc-180">Универсальный соединитель SQL:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-180">Generic SQL:</span></span>
 * <span data-ttu-id="6e2fc-181">Исправление ошибки, когда многозначный атрибут импорта изменений универсального соединителя SQL не сообщал об ошибке.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="6e2fc-182">Если экспортировать удаленные или добавленные значения многозначного атрибута в источник данных, они не будут в нем распознаваться.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="6e2fc-183">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-183">Lotus Notes:</span></span>
 * <span data-ttu-id="6e2fc-184">Указанное поле, «Полное имя» отображается в метавселенной hello правильно тем не менее при экспорте tooNotes hello значение для атрибута hello равно Null или пусто.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-184">A specific field "Full Name" is shown in hello metaverse correctly however when exporting tooNotes hello value for hello attribute is Null or Empty.</span></span>
 * <span data-ttu-id="6e2fc-185">Исправление ошибки дублирования для издателя сертификатов</span><span class="sxs-lookup"><span data-stu-id="6e2fc-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="6e2fc-186">При выборе на hello соединителя Lotus Domino с другими объектами hello объекта без данных затем мы получили сообщение об ошибке обнаружения hello при выполнении полного импорта.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-186">When hello Object without any data is selected on hello Lotus Domino Connector with other objects then we receive hello Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="6e2fc-187">Если разностный Импорт службой на hello соединителя Lotus Domino, в конце hello, выполнения, hello Microsoft.IdentityManagement.MA.LotusDomino.Service.exe иногда возвращает сообщение об ошибке приложения.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-187">When Delta Import is being running on hello Lotus Domino Connector, at hello end of that run, hello Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="6e2fc-188">Общую группу членства хорошо работает и сохраняется, за исключением того, при выполнении hello экспорта tootry tooremove пользователя от членства показывает успешным при работе с обновлением, но hello пользователь фактически не удаляются из членства в Lotus Notes.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-188">Group membership overall works fine and is maintained, except when running hello export tootry tooremove a user from membership it shows as successful with an update, but hello user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="6e2fc-189">Это режим toochoose возможность экспорта, как «Добавить элемент внизу» была добавлена в конфигурации графического пользовательского интерфейса Lotus MA tooappend новые элементы внизу во время экспорта hello для многозначных атрибутов.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-189">An opportunity toochoose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA tooappend new items at bottom during hello export for multi-valued attributes.</span></span>
 * <span data-ttu-id="6e2fc-190">Добавляет соединитель hello необходимости логику toodelete hello файл из папки почты hello и идентификатор хранилища.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-190">Connector will add hello needed logic toodelete hello file from hello Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="6e2fc-191">Нельзя удалить участников из адресной книги Notes.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="6e2fc-192">Значения должны быть успешно удалены из многозначного атрибута.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="6e2fc-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="6e2fc-193">1.1.117.0</span></span>
<span data-ttu-id="6e2fc-194">Дата выпуска: март 2016 г.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-194">Released: 2016 March</span></span>

<span data-ttu-id="6e2fc-195">**Новый соединитель**</span><span class="sxs-lookup"><span data-stu-id="6e2fc-195">**New Connector**</span></span>  
<span data-ttu-id="6e2fc-196">Начальный выпуск hello [универсальный соединитель SQL](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="6e2fc-196">Initial release of hello [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="6e2fc-197">**Новые функции:**</span><span class="sxs-lookup"><span data-stu-id="6e2fc-197">**New features:**</span></span>

* <span data-ttu-id="6e2fc-198">Универсальный соединитель LDAP:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="6e2fc-199">Добавлена поддержка импорта изменений с помощью Isode.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="6e2fc-200">Соединитель веб-служб:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-200">Web Services Connector:</span></span>
  * <span data-ttu-id="6e2fc-201">Обновленные hello csEntryChangeResult действия и setImportErrorCode действия tooallow объекта ошибки уровня toobe возвращаемый задней toohello модуль синхронизации.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-201">Updated hello csEntryChangeResult activity and setImportErrorCode activity tooallow object level errors toobe returned back toohello sync engine.</span></span>
  * <span data-ttu-id="6e2fc-202">Обновленные hello SAP6 и SAP6User шаблоны toouse hello новый объект ошибки уровня функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-202">Updated hello SAP6 and SAP6User templates toouse hello new object level error functionality.</span></span>
* <span data-ttu-id="6e2fc-203">Соединитель Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="6e2fc-204">Для экспорта требуется один издатель сертификатов на адресную книгу.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="6e2fc-205">После этого можно использовать hello же пароль для всех certifiers toomake hello управления проще.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-205">You can now use hello same password for all certifiers toomake hello management easier.</span></span>

<span data-ttu-id="6e2fc-206">**Исправленные проблемы:**</span><span class="sxs-lookup"><span data-stu-id="6e2fc-206">**Fixed issues:**</span></span>

* <span data-ttu-id="6e2fc-207">Универсальный соединитель LDAP:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="6e2fc-208">IBM Tivoli DS: некоторые ссылочные атрибуты не обнаруживались должным образом.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="6e2fc-209">Для открытых LDAP во время импорта дельта пробельные символы в hello начала и конца строки были усечены.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-209">For Open LDAP during a delta import, whitespaces at hello beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="6e2fc-210">Novell и NetIQ экспорт, переместить объект между подразделений и контейнеров, а также на hello одновременную сбой переименованный hello объекта.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at hello same time renamed hello object failed.</span></span>
* <span data-ttu-id="6e2fc-211">Соединитель веб-служб:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-211">Web Services Connector:</span></span>
  * <span data-ttu-id="6e2fc-212">Если hello веб-служба имеет несколько конечных точек для одной привязки, затем hello соединитель не обнаружил неправильно этих конечных точек.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-212">If hello web service had multiple end-points for same binding, then hello Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="6e2fc-213">Соединитель Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="6e2fc-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="6e2fc-214">Экспорт hello полное имя атрибута tooa mail в базе данных не работает.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-214">An export of hello fullName attribute tooa mail-in database did not work.</span></span>
  * <span data-ttu-id="6e2fc-215">Экспорт, в которой как добавление или удаление члена из группы только для экспортированного hello добавлялись новые элементы.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-215">An export which both added and removed member from a group only exported hello added members.</span></span>
  * <span data-ttu-id="6e2fc-216">Если указан недопустимый документ заметки (hello isValid атрибута равным toofalse), затем hello соединителя завершается с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-216">If a Notes Document is invalid (hello attribute isValid set toofalse), then hello Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="6e2fc-217">Более старые выпуски</span><span class="sxs-lookup"><span data-stu-id="6e2fc-217">Older releases</span></span>
<span data-ttu-id="6e2fc-218">До марта 2016 г. hello соединителей были выпущены в виде вопросам технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-218">Before March 2016, hello Connectors were released as support topics.</span></span>

<span data-ttu-id="6e2fc-219">**Универсальный LDAP**</span><span class="sxs-lookup"><span data-stu-id="6e2fc-219">**Generic LDAP**</span></span>

* <span data-ttu-id="6e2fc-220">[KB3078617](https://support.microsoft.com/kb/3078617) — 1.0.0597, сентябрь 2015 г.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="6e2fc-221">[KB3044896](https://support.microsoft.com/kb/3044896) — 1.0.0549, март 2015 г.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="6e2fc-222">[KB3031009](https://support.microsoft.com/kb/3031009) — 1.0.0534, январь 2015 г.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="6e2fc-223">[KB3008177](https://support.microsoft.com/kb/3008177) — 1.0.0419, сентябрь 2014 г.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="6e2fc-224">[KB2936070](https://support.microsoft.com/kb/2936070) — 4.3.1082, март 2014 г.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="6e2fc-225">**Веб-службы**</span><span class="sxs-lookup"><span data-stu-id="6e2fc-225">**WebServices**</span></span>

* <span data-ttu-id="6e2fc-226">[KB3008178](https://support.microsoft.com/kb/3008178) — 1.0.0419, сентябрь 2014 г.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="6e2fc-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="6e2fc-227">**PowerShell**</span></span>

* <span data-ttu-id="6e2fc-228">[KB3008179](https://support.microsoft.com/kb/3008179) — 1.0.0419, сентябрь 2014 г.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="6e2fc-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="6e2fc-229">**Lotus Domino**</span></span>

* <span data-ttu-id="6e2fc-230">[KB3096533](https://support.microsoft.com/kb/3096533) — 1.0.0597, сентябрь 2015 г.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="6e2fc-231">[KB3044895](https://support.microsoft.com/kb/3044895) — 1.0.0549, март 2015 г.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="6e2fc-232">[KB2977286](https://support.microsoft.com/kb/2977286) — 5.3.0712, август 2014 г.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="6e2fc-233">[KB2932635](https://support.microsoft.com/kb/2932635) — 5.3.1003, февраль 2014 г.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="6e2fc-234">[KB2899874](https://support.microsoft.com/kb/2899874) — 5.3.0721, октябрь 2013 г.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="6e2fc-235">[KB2875551](https://support.microsoft.com/kb/2875551) — 5.3.0534, август 2013 г.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e2fc-236">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6e2fc-236">Next steps</span></span>
<span data-ttu-id="6e2fc-237">Дополнительные сведения о hello [синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6e2fc-237">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="6e2fc-238">Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="6e2fc-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
