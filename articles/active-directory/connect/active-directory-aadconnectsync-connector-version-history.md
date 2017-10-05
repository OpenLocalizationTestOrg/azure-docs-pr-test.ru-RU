---
title: "История выпусков версий соединителей | Документация Майкрософт"
description: "В этой статье перечислены все соединители для Forefront Identity Manager (FIM) и Microsoft Identity Manager (MIM)."
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
ms.openlocfilehash: 313145f4d8e5faa91fb3504cb0fd0ba87ca2e379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="62b81-103">История выпусков версий соединителей</span><span class="sxs-lookup"><span data-stu-id="62b81-103">Connector Version Release History</span></span>
<span data-ttu-id="62b81-104">Соединители для Forefront Identity Manager (FIM) и Microsoft Identity Manager (MIM) часто обновляются.</span><span class="sxs-lookup"><span data-stu-id="62b81-104">The Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="62b81-105">Эта статья касается только FIM и MIM.</span><span class="sxs-lookup"><span data-stu-id="62b81-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="62b81-106">Установка этих соединителей не поддерживается в Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="62b81-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="62b81-107">Выпущенные соединители предварительно устанавливаются в AADConnect при обновлении до указанной сборки.</span><span class="sxs-lookup"><span data-stu-id="62b81-107">Released Connectors are preinstalled on AADConnect when upgrading to specified Build.</span></span>

<span data-ttu-id="62b81-108">В этой статье перечисляются все выпущенные соединители.</span><span class="sxs-lookup"><span data-stu-id="62b81-108">This topic list all versions of the Connectors that have been released.</span></span>

<span data-ttu-id="62b81-109">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="62b81-109">Related links:</span></span>

* [<span data-ttu-id="62b81-110">Скачивание последних соединителей.</span><span class="sxs-lookup"><span data-stu-id="62b81-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="62b81-111">[универсальному соединителю LDAP](active-directory-aadconnectsync-connector-genericldap.md) .</span><span class="sxs-lookup"><span data-stu-id="62b81-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="62b81-112">[универсальному соединителю SQL](active-directory-aadconnectsync-connector-genericsql.md) .</span><span class="sxs-lookup"><span data-stu-id="62b81-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="62b81-113">[соединителю веб-служб](http://go.microsoft.com/fwlink/?LinkID=226245) .</span><span class="sxs-lookup"><span data-stu-id="62b81-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="62b81-114">[соединителю PowerShell](active-directory-aadconnectsync-connector-powershell.md) .</span><span class="sxs-lookup"><span data-stu-id="62b81-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="62b81-115">[соединителю Lotus Domino](active-directory-aadconnectsync-connector-domino.md) .</span><span class="sxs-lookup"><span data-stu-id="62b81-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="62b81-116">1.1.604.0 (AADConnect — ожидается выпуск)</span><span class="sxs-lookup"><span data-stu-id="62b81-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="62b81-117">Исправленные проблемы:</span><span class="sxs-lookup"><span data-stu-id="62b81-117">Fixed issues:</span></span>

* <span data-ttu-id="62b81-118">Универсальный соединитель веб-служб:</span><span class="sxs-lookup"><span data-stu-id="62b81-118">Generic Web Services:</span></span>
  * <span data-ttu-id="62b81-119">Устранена проблема, не позволявшая создать проект SOAP при наличии двух или более конечных точек.</span><span class="sxs-lookup"><span data-stu-id="62b81-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="62b81-120">Универсальный соединитель SQL:</span><span class="sxs-lookup"><span data-stu-id="62b81-120">Generic SQL:</span></span>
  * <span data-ttu-id="62b81-121">Во время выполнения импорта соединитель GSQL неправильно преобразовывал время при сохранении данных в пространстве соединителя.</span><span class="sxs-lookup"><span data-stu-id="62b81-121">In the operation of import the GSQL was not converting time correctly, when saved to connector space.</span></span> <span data-ttu-id="62b81-122">Формат даты и времени по умолчанию для пространства соединителя GSQL был изменен с "гггг-ММ-дд чч:мм:ссZ" на "гггг-ММ-дд ЧЧ:мм:ссZ".</span><span class="sxs-lookup"><span data-stu-id="62b81-122">The default date and time format for connector space of the GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' to 'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="62b81-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="62b81-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="62b81-124">Исправленные проблемы:</span><span class="sxs-lookup"><span data-stu-id="62b81-124">Fixed issues:</span></span>

* <span data-ttu-id="62b81-125">Универсальный соединитель веб-служб:</span><span class="sxs-lookup"><span data-stu-id="62b81-125">Generic Web Services:</span></span>
  * <span data-ttu-id="62b81-126">Средство Wsconfig не правильно преобразовало массив JSON из примера запроса для метода службы REST.</span><span class="sxs-lookup"><span data-stu-id="62b81-126">The Wsconfig tool did not convert correctly the Json array from "sample request" for the REST service method.</span></span> <span data-ttu-id="62b81-127">По этой причине возникали проблемы с сериализацией данного массива JSON для запроса REST.</span><span class="sxs-lookup"><span data-stu-id="62b81-127">This caused problems with serialization this Json array for the REST request.</span></span>
  * <span data-ttu-id="62b81-128">Инструмент настройки соединителя веб-служб не поддерживает использование символов пробела в именах атрибутов JSON.</span><span class="sxs-lookup"><span data-stu-id="62b81-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="62b81-129">Можно вручную добавить шаблон замены в файл WSConfigTool.exe.config, например ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```.</span><span class="sxs-lookup"><span data-stu-id="62b81-129">A Substitution pattern can be added manually to the WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="62b81-130">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="62b81-130">Lotus Notes:</span></span>
  * <span data-ttu-id="62b81-131">Если параметр **Allow custom certifiers for Organization/Organizational Units** (Разрешить настраиваемые заверители для организаций и подразделений) отключен, то во время экспорта (обновления) происходит сбой соединителя. Затем все атрибуты будут экспортированы в Domino, однако во время экспорта для синхронизации возвращается исключение KeyNotFoundException.</span><span class="sxs-lookup"><span data-stu-id="62b81-131">When the option **Allow custom certifiers for Organization/Organizational Units** is disabled then the connector fails during export (Update) After the export flow all attributes are exported to Domino but at the time of export a KeyNotFoundException is returned to Sync.</span></span> 
    * <span data-ttu-id="62b81-132">Это связано с тем, что операция переименования завершается сбоем при попытке изменения DN (атрибута имени пользователя), изменив один из атрибутов ниже:</span><span class="sxs-lookup"><span data-stu-id="62b81-132">This happens because the rename operation fails when it tries to change DN (UserName attribute) by changing one of the attributes below:</span></span>  
      - <span data-ttu-id="62b81-133">LastName</span><span class="sxs-lookup"><span data-stu-id="62b81-133">LastName</span></span>
      - <span data-ttu-id="62b81-134">FirstName</span><span class="sxs-lookup"><span data-stu-id="62b81-134">FirstName</span></span>
      - <span data-ttu-id="62b81-135">MiddleInitial;</span><span class="sxs-lookup"><span data-stu-id="62b81-135">MiddleInitial</span></span>
      - <span data-ttu-id="62b81-136">AltFullName;</span><span class="sxs-lookup"><span data-stu-id="62b81-136">AltFullName</span></span>
      - <span data-ttu-id="62b81-137">AltFullNameLanguage;</span><span class="sxs-lookup"><span data-stu-id="62b81-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="62b81-138">ou;</span><span class="sxs-lookup"><span data-stu-id="62b81-138">ou</span></span>
      - <span data-ttu-id="62b81-139">altcommonname.</span><span class="sxs-lookup"><span data-stu-id="62b81-139">altcommonname</span></span>

  * <span data-ttu-id="62b81-140">Если параметр **Разрешить настраиваемые заверители для организации и подразделений** включен, но необходимые заверители все еще пусты, возникает исключение KeyNotFoundException.</span><span class="sxs-lookup"><span data-stu-id="62b81-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="62b81-141">Улучшения</span><span class="sxs-lookup"><span data-stu-id="62b81-141">Enhancements:</span></span>

* <span data-ttu-id="62b81-142">Универсальный соединитель SQL:</span><span class="sxs-lookup"><span data-stu-id="62b81-142">Generic SQL:</span></span>
  * <span data-ttu-id="62b81-143">**Сценарий: переработан. Реализовано:** компонент "*".</span><span class="sxs-lookup"><span data-stu-id="62b81-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="62b81-144">**Описание решения**. Изменен подход к [обработке ссылок с несколькими значениями атрибутов](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="62b81-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="62b81-145">Исправленные проблемы:</span><span class="sxs-lookup"><span data-stu-id="62b81-145">Fixed issues:</span></span>

* <span data-ttu-id="62b81-146">Универсальный соединитель веб-служб:</span><span class="sxs-lookup"><span data-stu-id="62b81-146">Generic Web Services:</span></span>
  * <span data-ttu-id="62b81-147">Не удается импортировать конфигурацию сервера при наличии соединителя веб-службы</span><span class="sxs-lookup"><span data-stu-id="62b81-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="62b81-148">Соединитель веб-службы не работает с несколькими веб-службами</span><span class="sxs-lookup"><span data-stu-id="62b81-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="62b81-149">Универсальный соединитель SQL:</span><span class="sxs-lookup"><span data-stu-id="62b81-149">Generic SQL:</span></span>
  * <span data-ttu-id="62b81-150">Типы объектов не указаны для ссылочного атрибута с одним значением</span><span class="sxs-lookup"><span data-stu-id="62b81-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="62b81-151">Разностный импорт в рамках стратегии отслеживания изменений удаляет объект при удалении значения из таблицы с несколькими значениями</span><span class="sxs-lookup"><span data-stu-id="62b81-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="62b81-152">Исключение OverflowException в соединителе GSQL с использованием DB2 в AS/400</span><span class="sxs-lookup"><span data-stu-id="62b81-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="62b81-153">Lotus:</span><span class="sxs-lookup"><span data-stu-id="62b81-153">Lotus:</span></span>
  * <span data-ttu-id="62b81-154">Добавлена возможность включения и отключения поиска подразделений перед открытием страницы с глобальными параметрами</span><span class="sxs-lookup"><span data-stu-id="62b81-154">Added option to enable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="62b81-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="62b81-155">1.1.443.0</span></span>

<span data-ttu-id="62b81-156">Дата выпуска: март 2017 г.</span><span class="sxs-lookup"><span data-stu-id="62b81-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="62b81-157">Улучшения</span><span class="sxs-lookup"><span data-stu-id="62b81-157">Enhancements</span></span>

* <span data-ttu-id="62b81-158">Универсальный соединитель SQL.</span><span class="sxs-lookup"><span data-stu-id="62b81-158">Generic SQL:</span></span></br><span data-ttu-id="62b81-159">
  **Сценарий.** Для соединителя SQL ссылка разрешается только на один тип объекта, а также требуется перекрестная ссылка для участников. Это хорошо известное ограничение.</span><span class="sxs-lookup"><span data-stu-id="62b81-159">
  **Scenario Symptoms:**  It is a well-known limitation with the SQL Connector where we only allow a reference to one object type and require cross reference with members.</span></span> </br><span data-ttu-id="62b81-160">
**Решение.** На этапе обработки ссылок с выбранным параметром "*" все сочетания типов объектов будут возвращены в модуль синхронизации.</span><span class="sxs-lookup"><span data-stu-id="62b81-160">
**Solution description:** In the processing step for references were "*" option is chosen, ALL combinations of object types will be returned back to the sync engine.</span></span>

>[!Important]
- <span data-ttu-id="62b81-161">Будет создано множество заполнителей.</span><span class="sxs-lookup"><span data-stu-id="62b81-161">This will create many placeholders</span></span>
- <span data-ttu-id="62b81-162">Убедитесь, что типы объектов имеют уникальные имена.</span><span class="sxs-lookup"><span data-stu-id="62b81-162">It is required to make sure the naming is unique cross object types.</span></span>


* <span data-ttu-id="62b81-163">Универсальный соединитель LDAP.</span><span class="sxs-lookup"><span data-stu-id="62b81-163">Generic LDAP:</span></span></br><span data-ttu-id="62b81-164">
 **Сценарий.** Если в определенном разделе выбрано только несколько контейнеров, поиск по-прежнему будет выполняться по всему разделу.</span><span class="sxs-lookup"><span data-stu-id="62b81-164">
**Scenario:** When only few containers are selected in specific partition, then the search still will be done in whole partition.</span></span> <span data-ttu-id="62b81-165">Этот определенный раздел будет фильтроваться по службе синхронизации, а не по агенту управления, что может привести к снижению производительности.</span><span class="sxs-lookup"><span data-stu-id="62b81-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="62b81-166">**Решение.** Измените код соединителя GLDAP, чтобы просматривать все контейнеры, а также искать объекты в каждом из них вместо поиска по всему разделу.</span><span class="sxs-lookup"><span data-stu-id="62b81-166">**Solution description:** Changed GLDAP connector's code to make it possible go through all containers and search objects in each of them, instead of searching in the whole partition.</span></span>


* <span data-ttu-id="62b81-167">Lotus Domino.</span><span class="sxs-lookup"><span data-stu-id="62b81-167">Lotus Domino:</span></span>

  <span data-ttu-id="62b81-168">**Сценарий.** Поддержка удаления электронной почты Domino для удаления пользователя во время экспорта.</span><span class="sxs-lookup"><span data-stu-id="62b81-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="62b81-169">
  **Решение.** Настраиваемая поддержка удаления электронной почты для удаления пользователя во время экспорта.</span><span class="sxs-lookup"><span data-stu-id="62b81-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="62b81-170">Исправленные проблемы:</span><span class="sxs-lookup"><span data-stu-id="62b81-170">Fixed issues:</span></span>
* <span data-ttu-id="62b81-171">Универсальный соединитель веб-служб:</span><span class="sxs-lookup"><span data-stu-id="62b81-171">Generic Web Services:</span></span>
 * <span data-ttu-id="62b81-172">При изменении URL-адреса службы в проектах wsconfig SAP по умолчанию с помощью средства настройки веб-службы возникает следующая ошибка: "Не удалось найти часть пути".</span><span class="sxs-lookup"><span data-stu-id="62b81-172">When changing the service URL in Default SAP wsconfig projects through WebService Configuration Tool then the following error happens: Could not find a part of the path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="62b81-173">Универсальный соединитель LDAP:</span><span class="sxs-lookup"><span data-stu-id="62b81-173">Generic LDAP:</span></span>
 * <span data-ttu-id="62b81-174">Соединитель GLDAP не распознает все атрибуты в AD LDS.</span><span class="sxs-lookup"><span data-stu-id="62b81-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="62b81-175">Если атрибуты UPN не обнаруживаются в схеме каталога LDAP, работа мастера приостанавливается.</span><span class="sxs-lookup"><span data-stu-id="62b81-175">Wizard breaks when no UPN attributes are detected from the LDAP directory schema</span></span>
 * <span data-ttu-id="62b81-176">Если атрибут objectclass не выбран, операции импорта изменений завершаются с ошибками обнаружения, что не происходит во время полного импорта.</span><span class="sxs-lookup"><span data-stu-id="62b81-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="62b81-177">На странице конфигурации Configure Partitions and Hierarchies (Настройка разделов и иерархий) не отображаются объекты с типами, соответствующими разделу серверов Novel в универсальном соединителе.</span><span class="sxs-lookup"><span data-stu-id="62b81-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal to the partition for Novel servers in the Generic</span></span>  
<span data-ttu-id="62b81-178">Агент управления LDAP.</span><span class="sxs-lookup"><span data-stu-id="62b81-178">LDAP MA.</span></span> <span data-ttu-id="62b81-179">Отображаются только объекты из раздела RootDSE.</span><span class="sxs-lookup"><span data-stu-id="62b81-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="62b81-180">Универсальный соединитель SQL:</span><span class="sxs-lookup"><span data-stu-id="62b81-180">Generic SQL:</span></span>
 * <span data-ttu-id="62b81-181">Исправление ошибки, когда многозначный атрибут импорта изменений универсального соединителя SQL не сообщал об ошибке.</span><span class="sxs-lookup"><span data-stu-id="62b81-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="62b81-182">Если экспортировать удаленные или добавленные значения многозначного атрибута в источник данных, они не будут в нем распознаваться.</span><span class="sxs-lookup"><span data-stu-id="62b81-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="62b81-183">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="62b81-183">Lotus Notes:</span></span>
 * <span data-ttu-id="62b81-184">Определенное поле "Полное имя" отображается в метавселенной правильно. Однако при экспорте в заметки значение атрибута пусто или имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="62b81-184">A specific field "Full Name" is shown in the metaverse correctly however when exporting to Notes the value for the attribute is Null or Empty.</span></span>
 * <span data-ttu-id="62b81-185">Исправление ошибки дублирования для издателя сертификатов</span><span class="sxs-lookup"><span data-stu-id="62b81-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="62b81-186">Если для соединителя Lotus Domino вместе с другими объектами выбран объект без данных, во время полного импорта отобразится сообщение об ошибке обнаружения.</span><span class="sxs-lookup"><span data-stu-id="62b81-186">When the Object without any data is selected on the Lotus Domino Connector with other objects then we receive the Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="62b81-187">По завершении выполнения импорта изменений для соединителя Lotus Domino служба Microsoft.IdentityManagement.MA.LotusDomino.Service.exe иногда возвращает сообщение об ошибке приложения.</span><span class="sxs-lookup"><span data-stu-id="62b81-187">When Delta Import is being running on the Lotus Domino Connector, at the end of that run, the Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="62b81-188">Участие в группе работает надлежащим образом и поддерживается, за исключением случаев, когда при выполнении экспорта для удаления пользователя из членства отображается успешное обновление, хотя пользователь на самом деле не удаляется из членства в Lotus Notes.</span><span class="sxs-lookup"><span data-stu-id="62b81-188">Group membership overall works fine and is maintained, except when running the export to try to remove a user from membership it shows as successful with an update, but the user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="62b81-189">В графическом интерфейсе настройки агента управления Lotus добавлена возможность выбрать режим экспорта Append Item at bottom (Добавление элемента внизу), чтобы добавлять новые элементы внизу во время экспорта многозначных атрибутов.</span><span class="sxs-lookup"><span data-stu-id="62b81-189">An opportunity to choose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA to append new items at bottom during the export for multi-valued attributes.</span></span>
 * <span data-ttu-id="62b81-190">Соединитель добавляет логику, необходимую для удаления файла из почтовой папки и хранилища идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="62b81-190">Connector will add the needed logic to delete the file from the Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="62b81-191">Нельзя удалить участников из адресной книги Notes.</span><span class="sxs-lookup"><span data-stu-id="62b81-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="62b81-192">Значения должны быть успешно удалены из многозначного атрибута.</span><span class="sxs-lookup"><span data-stu-id="62b81-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="62b81-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="62b81-193">1.1.117.0</span></span>
<span data-ttu-id="62b81-194">Дата выпуска: март 2016 г.</span><span class="sxs-lookup"><span data-stu-id="62b81-194">Released: 2016 March</span></span>

<span data-ttu-id="62b81-195">**Новый соединитель**</span><span class="sxs-lookup"><span data-stu-id="62b81-195">**New Connector**</span></span>  
<span data-ttu-id="62b81-196">Первоначальный выпуск [универсальному соединителю SQL](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="62b81-196">Initial release of the [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="62b81-197">**Новые функции:**</span><span class="sxs-lookup"><span data-stu-id="62b81-197">**New features:**</span></span>

* <span data-ttu-id="62b81-198">Универсальный соединитель LDAP:</span><span class="sxs-lookup"><span data-stu-id="62b81-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="62b81-199">Добавлена поддержка импорта изменений с помощью Isode.</span><span class="sxs-lookup"><span data-stu-id="62b81-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="62b81-200">Соединитель веб-служб:</span><span class="sxs-lookup"><span data-stu-id="62b81-200">Web Services Connector:</span></span>
  * <span data-ttu-id="62b81-201">Обновлены действия csEntryChangeResult и setImportErrorCode, чтобы устранить ошибки уровня объекта, возвращаемые в модуль синхронизации.</span><span class="sxs-lookup"><span data-stu-id="62b81-201">Updated the csEntryChangeResult activity and setImportErrorCode activity to allow object level errors to be returned back to the sync engine.</span></span>
  * <span data-ttu-id="62b81-202">Обновлены шаблоны SAP6 и SAP6User для использования новых функций обработки ошибок уровня объекта.</span><span class="sxs-lookup"><span data-stu-id="62b81-202">Updated the SAP6 and SAP6User templates to use the new object level error functionality.</span></span>
* <span data-ttu-id="62b81-203">Соединитель Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="62b81-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="62b81-204">Для экспорта требуется один издатель сертификатов на адресную книгу.</span><span class="sxs-lookup"><span data-stu-id="62b81-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="62b81-205">Теперь можно использовать один и тот же пароль для всех издателей сертификатов, чтобы облегчить управление.</span><span class="sxs-lookup"><span data-stu-id="62b81-205">You can now use the same password for all certifiers to make the management easier.</span></span>

<span data-ttu-id="62b81-206">**Исправленные проблемы:**</span><span class="sxs-lookup"><span data-stu-id="62b81-206">**Fixed issues:**</span></span>

* <span data-ttu-id="62b81-207">Универсальный соединитель LDAP:</span><span class="sxs-lookup"><span data-stu-id="62b81-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="62b81-208">IBM Tivoli DS: некоторые ссылочные атрибуты не обнаруживались должным образом.</span><span class="sxs-lookup"><span data-stu-id="62b81-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="62b81-209">Open LDAP: при импорте изменений усекались пробелы в начале и конце строки.</span><span class="sxs-lookup"><span data-stu-id="62b81-209">For Open LDAP during a delta import, whitespaces at the beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="62b81-210">Novell и NetIQ: экспорт, при котором объект перемещался между подразделениями или контейнерами и в то же время переименовывался, приводил к сбою.</span><span class="sxs-lookup"><span data-stu-id="62b81-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at the same time renamed the object failed.</span></span>
* <span data-ttu-id="62b81-211">Соединитель веб-служб:</span><span class="sxs-lookup"><span data-stu-id="62b81-211">Web Services Connector:</span></span>
  * <span data-ttu-id="62b81-212">Если у веб-службы было несколько конечных точек для одной привязки, то соединитель не мог правильно обнаружить эти конечные точки.</span><span class="sxs-lookup"><span data-stu-id="62b81-212">If the web service had multiple end-points for same binding, then the Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="62b81-213">Соединитель Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="62b81-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="62b81-214">Не работал экспорт атрибута fullName в базу данных обслуживания почты.</span><span class="sxs-lookup"><span data-stu-id="62b81-214">An export of the fullName attribute to a mail-in database did not work.</span></span>
  * <span data-ttu-id="62b81-215">При экспорте с добавлением и удалением участника группы выполнялось только экспортирование добавленных участников.</span><span class="sxs-lookup"><span data-stu-id="62b81-215">An export which both added and removed member from a group only exported the added members.</span></span>
  * <span data-ttu-id="62b81-216">Если документ Notes являлся недопустимым (атрибуту isValid задано значение false), происходил сбой соединителя.</span><span class="sxs-lookup"><span data-stu-id="62b81-216">If a Notes Document is invalid (the attribute isValid set to false), then the Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="62b81-217">Более старые выпуски</span><span class="sxs-lookup"><span data-stu-id="62b81-217">Older releases</span></span>
<span data-ttu-id="62b81-218">До марта 2016 г. соединители выпускались в виде разделов службы поддержки.</span><span class="sxs-lookup"><span data-stu-id="62b81-218">Before March 2016, the Connectors were released as support topics.</span></span>

<span data-ttu-id="62b81-219">**Универсальный LDAP**</span><span class="sxs-lookup"><span data-stu-id="62b81-219">**Generic LDAP**</span></span>

* <span data-ttu-id="62b81-220">[KB3078617](https://support.microsoft.com/kb/3078617) — 1.0.0597, сентябрь 2015 г.</span><span class="sxs-lookup"><span data-stu-id="62b81-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="62b81-221">[KB3044896](https://support.microsoft.com/kb/3044896) — 1.0.0549, март 2015 г.</span><span class="sxs-lookup"><span data-stu-id="62b81-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="62b81-222">[KB3031009](https://support.microsoft.com/kb/3031009) — 1.0.0534, январь 2015 г.</span><span class="sxs-lookup"><span data-stu-id="62b81-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="62b81-223">[KB3008177](https://support.microsoft.com/kb/3008177) — 1.0.0419, сентябрь 2014 г.</span><span class="sxs-lookup"><span data-stu-id="62b81-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="62b81-224">[KB2936070](https://support.microsoft.com/kb/2936070) — 4.3.1082, март 2014 г.</span><span class="sxs-lookup"><span data-stu-id="62b81-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="62b81-225">**Веб-службы**</span><span class="sxs-lookup"><span data-stu-id="62b81-225">**WebServices**</span></span>

* <span data-ttu-id="62b81-226">[KB3008178](https://support.microsoft.com/kb/3008178) — 1.0.0419, сентябрь 2014 г.</span><span class="sxs-lookup"><span data-stu-id="62b81-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="62b81-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="62b81-227">**PowerShell**</span></span>

* <span data-ttu-id="62b81-228">[KB3008179](https://support.microsoft.com/kb/3008179) — 1.0.0419, сентябрь 2014 г.</span><span class="sxs-lookup"><span data-stu-id="62b81-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="62b81-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="62b81-229">**Lotus Domino**</span></span>

* <span data-ttu-id="62b81-230">[KB3096533](https://support.microsoft.com/kb/3096533) — 1.0.0597, сентябрь 2015 г.</span><span class="sxs-lookup"><span data-stu-id="62b81-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="62b81-231">[KB3044895](https://support.microsoft.com/kb/3044895) — 1.0.0549, март 2015 г.</span><span class="sxs-lookup"><span data-stu-id="62b81-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="62b81-232">[KB2977286](https://support.microsoft.com/kb/2977286) — 5.3.0712, август 2014 г.</span><span class="sxs-lookup"><span data-stu-id="62b81-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="62b81-233">[KB2932635](https://support.microsoft.com/kb/2932635) — 5.3.1003, февраль 2014 г.</span><span class="sxs-lookup"><span data-stu-id="62b81-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="62b81-234">[KB2899874](https://support.microsoft.com/kb/2899874) — 5.3.0721, октябрь 2013 г.</span><span class="sxs-lookup"><span data-stu-id="62b81-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="62b81-235">[KB2875551](https://support.microsoft.com/kb/2875551) — 5.3.0534, август 2013 г.</span><span class="sxs-lookup"><span data-stu-id="62b81-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="62b81-236">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="62b81-236">Next steps</span></span>
<span data-ttu-id="62b81-237">Узнайте больше о настройке [службы синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) .</span><span class="sxs-lookup"><span data-stu-id="62b81-237">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="62b81-238">Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="62b81-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
