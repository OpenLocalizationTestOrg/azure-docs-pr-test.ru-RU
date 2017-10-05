---
title: "Использование Azure AD Connect Health для синхронизации | Документация Майкрософт"
description: "На этой странице Azure AD Connect Health описывается отслеживание синхронизации Azure AD Connect."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4b06338cb62cc458e7b097db36023f0746d4e969
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a><span data-ttu-id="5bfc2-103">Мониторинг синхронизации Azure AD Connect с помощью Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="5bfc2-103">Monitor Azure AD Connect sync with Azure AD Connect Health</span></span>
<span data-ttu-id="5bfc2-104">Приведенная ниже документация относится к мониторингу синхронизации Azure AD Connect с помощью Azure AD Connect Health.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-104">The following documentation is specific to monitoring Azure AD Connect (Sync) with Azure AD Connect Health.</span></span>  <span data-ttu-id="5bfc2-105">Сведения о мониторинге AD FS с помощью Azure AD Connect Health см. в [этой статье](active-directory-aadconnect-health-adfs.md).</span><span class="sxs-lookup"><span data-stu-id="5bfc2-105">For information on monitoring AD FS with Azure AD Connect Health see [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md).</span></span> <span data-ttu-id="5bfc2-106">Кроме того, сведения о мониторинге доменных служб Active Directory с помощью Azure AD Connect Health можно найти [здесь](active-directory-aadconnect-health-adds.md).</span><span class="sxs-lookup"><span data-stu-id="5bfc2-106">Additionally, for information on monitoring Active Directory Domain Services with Azure AD Connect Health see [Using Azure AD Connect Health with AD DS](active-directory-aadconnect-health-adds.md).</span></span>

![Azure AD Connect Health для синхронизации](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a><span data-ttu-id="5bfc2-108">Оповещения Azure AD Connect Health для синхронизации</span><span class="sxs-lookup"><span data-stu-id="5bfc2-108">Alerts for Azure AD Connect Health for sync</span></span>
<span data-ttu-id="5bfc2-109">Раздел оповещений Azure AD Connect Health для синхронизации содержит список активных оповещений.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-109">The Azure AD Connect Health Alerts for sync section provides you the list of active alerts.</span></span> <span data-ttu-id="5bfc2-110">Каждое оповещение содержит соответствующую информацию, действия по устранению и ссылки на связанную документацию.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-110">Each alert includes relevant information, resolution steps, and links to related documentation.</span></span> <span data-ttu-id="5bfc2-111">Если выбрать активное или разрешенное оповещение, появится новая колонка с дополнительной информацией, действиями, которые можно предпринять для устранения причин оповещения, и ссылками на дополнительную документацию.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-111">By selecting an active or resolved alert you will see a new blade with additional information, as well as steps you can take to resolve the alert, and links to additional documentation.</span></span> <span data-ttu-id="5bfc2-112">Можно также просмотреть данные журнала об оповещениях, которые были разрешены в прошлом.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-112">You can also view historical data on alerts that were resolved in the past.</span></span>

<span data-ttu-id="5bfc2-113">Если выбрать оповещение, отобразится дополнительная информация, действия, которые можно предпринять для устранения причин оповещения, и ссылки на дополнительную документацию.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-113">By selecting an alert you will be provided with additional information as well as steps you can take to resolve the alert and links to additional documentation.</span></span>

![Ошибка синхронизации Azure AD Connect](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a><span data-ttu-id="5bfc2-115">Ограниченное ознакомление с оповещениями</span><span class="sxs-lookup"><span data-stu-id="5bfc2-115">Limited Evaluation of Alerts</span></span>
<span data-ttu-id="5bfc2-116">Если Azure AD Connect не использует конфигурацию по умолчанию (например, для фильтрации атрибутов выбрана пользовательская конфигурация), агент Azure AD Connect Health не будет передавать события ошибок, связанные с Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-116">If Azure AD Connect is NOT using the default configuration (for example, if Attribute Filtering is changed from the default configuration to a custom configuration), then the Azure AD Connect Health agent will not upload the error events related to Azure AD Connect.</span></span>

<span data-ttu-id="5bfc2-117">Это не позволяет службе в полной мере изучать оповещения.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-117">This limits the evaluation of alerts by the service.</span></span> <span data-ttu-id="5bfc2-118">На портале Azure в разделе службы появится соответствующее сообщение.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-118">You'd will see a banner that indicates this condition in the Azure Portal under your service.</span></span>

![Azure AD Connect Health для синхронизации](./media/active-directory-aadconnect-health-sync/banner.png)

<span data-ttu-id="5bfc2-120">Чтобы исправить это, в меню "Параметры" разрешите агенту Azure AD Connect Health передавать все журналы ошибок.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-120">You can change this by clicking "Settings" and allowing Azure AD Connect Health agent to upload all error logs.</span></span>

![Azure AD Connect Health для синхронизации](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a><span data-ttu-id="5bfc2-122">Sync Insight</span><span class="sxs-lookup"><span data-stu-id="5bfc2-122">Sync Insight</span></span>
<span data-ttu-id="5bfc2-123">Часто администраторы хотят знать, сколько времени требуется для синхронизации изменений в Azure AD, а также количество выполненных изменений.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-123">Admins Frequently want to know about the time it takes to sync changes to Azure AD and the amount of changes taking place.</span></span> <span data-ttu-id="5bfc2-124">Этот компонент предоставляет удобный способ визуализации этих сведений с помощью следующих диаграмм:</span><span class="sxs-lookup"><span data-stu-id="5bfc2-124">This feature provides an easy way to visualize this using the below graphs:</span></span>   

* <span data-ttu-id="5bfc2-125">задержка операций синхронизации;</span><span class="sxs-lookup"><span data-stu-id="5bfc2-125">Latency of sync operations</span></span>
* <span data-ttu-id="5bfc2-126">тренд, отображающий изменения объектов.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-126">Object Change trend</span></span>

### <a name="sync-latency"></a><span data-ttu-id="5bfc2-127">Задержка синхронизации</span><span class="sxs-lookup"><span data-stu-id="5bfc2-127">Sync Latency</span></span>
<span data-ttu-id="5bfc2-128">Этот компонент отвечает за графическое отображение тренда задержек операций синхронизации (импорт, экспорт и т. д.) для соединителей.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-128">This feature provides a graphical trend of latency of the sync operations (import, export, etc.) for connectors.</span></span>  <span data-ttu-id="5bfc2-129">Он позволяет не только быстро оценить задержки операций (например, при наличии большого количества происходящих изменений), но также определить аномальные задержки, требующие дополнительного изучения.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-129">This provides a quick and easy way to understand not only the latency of your operations (larger if you have a large set of changes occurring) but also a way to detect anomalies in the latency that may require further investigation.</span></span>

![Задержка синхронизации](./media/active-directory-aadconnect-health-sync/synclatency02.png)

<span data-ttu-id="5bfc2-131">По умолчанию для соединителя Azure AD отображаются только задержки операции экспорта.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-131">By default, only the latency of the 'Export' operation for the Azure AD connector is shown.</span></span>  <span data-ttu-id="5bfc2-132">Чтобы просмотреть дополнительные операции в этом соединителе или операции в других соединителях, щелкните диаграмму правой кнопкой мыши, выберите "Изменить диаграмму" или нажмите кнопку "Изменение диаграммы задержки" и выберите определенную операцию или соединитель.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-132">To see more operations on the connector or to view operations from other connectors, right-click on the chart,  select Edit Chart or click on the "Edit Latency Chart" button and choose the specific operation and connectors.</span></span>

### <a name="sync-object-changes"></a><span data-ttu-id="5bfc2-133">Изменения объектов синхронизации</span><span class="sxs-lookup"><span data-stu-id="5bfc2-133">Sync Object Changes</span></span>
<span data-ttu-id="5bfc2-134">Этот компонент отвечает за графическое отображение тренда количества изменений, которые вычисляются и экспортируются в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-134">This feature provides a graphical trend of the number of changes that are being evaluated and exported to Azure AD.</span></span>  <span data-ttu-id="5bfc2-135">Сейчас сбор такой информации из журналов синхронизации затруднен.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-135">Today, trying to gather this information from the sync logs is difficult.</span></span>  <span data-ttu-id="5bfc2-136">Схема — это не только простое средство мониторинга количества изменений, происходящих в вашей среде, она также предоставляет визуальные сведения о происходящих сбоях.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-136">The chart gives you, not only a simpler way of monitoring the number of changes that are occurring in your environment, but also a visual view of the failures that are occurring.</span></span>

![Задержка синхронизации](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a><span data-ttu-id="5bfc2-138">Отчет об ошибках синхронизации на уровне объектов (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="5bfc2-138">Object Level Synchronization Error Report (Preview)</span></span>
<span data-ttu-id="5bfc2-139">Этот компонент предоставляет отчет об ошибках синхронизации, которые могут возникать при синхронизации данных удостоверений между Windows Server AD и Azure AD с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-139">This feature provides a report about synchronization errors that can occur when identity data is synchronized between Windows Server AD and Azure AD using Azure AD Connect.</span></span>

* <span data-ttu-id="5bfc2-140">В отчете содержатся ошибки, записанные клиентом синхронизации (Azure AD Connect версии 1.1.281.0 или выше).</span><span class="sxs-lookup"><span data-stu-id="5bfc2-140">The report covers errors recorded by the sync client (Azure AD Connect version 1.1.281.0 or higher)</span></span>
* <span data-ttu-id="5bfc2-141">В отчете приводятся ошибки, произошедшие в течение последней операции синхронизации в модуле синхронизации</span><span class="sxs-lookup"><span data-stu-id="5bfc2-141">It includes the errors that occurred in the last synchronization operation on the sync engine.</span></span> <span data-ttu-id="5bfc2-142">(операция "Экспорт" в соединителе Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5bfc2-142">("Export" on the Azure AD Connector.)</span></span>
* <span data-ttu-id="5bfc2-143">Агент Azure AD Connect Health для синхронизации должен иметь исходящее подключение к необходимым конечным точкам. Таким образом, отчет будет содержать актуальные данные.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-143">Azure AD Connect Health agent for sync must have outbound connectivity to the required end points for the report to include the latest data.</span></span>
* <span data-ttu-id="5bfc2-144">Отчет **обновляется каждые 30 минут** на основе данных, полученных от агента Azure AD Connect Health для синхронизации.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-144">The report is **updated after every 30 minutes** using the data uploaded by Azure AD Connect Health agent for sync.</span></span>
  <span data-ttu-id="5bfc2-145">Этот отчет отличается следующими основными преимуществами:</span><span class="sxs-lookup"><span data-stu-id="5bfc2-145">It provides the following key capabilities</span></span>

  * <span data-ttu-id="5bfc2-146">классификация ошибок;</span><span class="sxs-lookup"><span data-stu-id="5bfc2-146">Categorization of errors</span></span>
  * <span data-ttu-id="5bfc2-147">вывод списка объектов с ошибками по категориям;</span><span class="sxs-lookup"><span data-stu-id="5bfc2-147">List of objects with error per category</span></span>
  * <span data-ttu-id="5bfc2-148">хранение данных об ошибках в одном месте;</span><span class="sxs-lookup"><span data-stu-id="5bfc2-148">All the data about the errors at one place</span></span>
  * <span data-ttu-id="5bfc2-149">параллельное сравнение объектов с ошибкой, возникшей в результате конфликта;</span><span class="sxs-lookup"><span data-stu-id="5bfc2-149">Side by side comparison of Objects with error due to a conflict</span></span>
  * <span data-ttu-id="5bfc2-150">скачивание отчета об ошибках в формате CVS (ожидается в ближайшее время).</span><span class="sxs-lookup"><span data-stu-id="5bfc2-150">Download the error report as a CVS (coming soon)</span></span>

### <a name="categorization-of-errors"></a><span data-ttu-id="5bfc2-151">Классификация ошибок</span><span class="sxs-lookup"><span data-stu-id="5bfc2-151">Categorization of Errors</span></span>
<span data-ttu-id="5bfc2-152">Имеющиеся ошибки синхронизации группируются в отчете по следующим категориям.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-152">The report categorizes the existing synchronization errors in the following categories:</span></span>

| <span data-ttu-id="5bfc2-153">Категория</span><span class="sxs-lookup"><span data-stu-id="5bfc2-153">Category</span></span> | <span data-ttu-id="5bfc2-154">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="5bfc2-154">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5bfc2-155">Повторяющийся атрибут</span><span class="sxs-lookup"><span data-stu-id="5bfc2-155">Duplicate Attribute</span></span> |<span data-ttu-id="5bfc2-156">Ошибки при попытках Azure AD Connect создать или обновить объекты с повторяющимися значениями одного или нескольких атрибутов в Azure AD, которые должны быть уникальными в клиенте, такие как proxyAddresses, UserPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-156">Errors when Azure AD Connect attempts create or update objects with duplicated values of one or more attributes in Azure AD that must be unique in a Tenant, such as proxyAddresses, UserPrincipalName.</span></span> |
| <span data-ttu-id="5bfc2-157">Несоответствие данных</span><span class="sxs-lookup"><span data-stu-id="5bfc2-157">Data Mismatch</span></span> |<span data-ttu-id="5bfc2-158">Ошибки синхронизации, возникшие в результате сбоя мягкого сопоставления объектов.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-158">Errors when the soft-match fails to match objects that result in synchronization errors.</span></span> |
| <span data-ttu-id="5bfc2-159">Сбой проверки данных</span><span class="sxs-lookup"><span data-stu-id="5bfc2-159">Data Validation Failure</span></span> |<span data-ttu-id="5bfc2-160">Ошибки, возникшие из-за недопустимых данных, таких как неподдерживаемые символы в важных атрибутах (например, UserPrincipalName), ошибки формата, не проходящие проверку перед записью в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-160">Errors due to invalid data, such as unsupported characters in critical attributes such as UserPrincipalName, format errors that fail validation before being written in Azure AD.</span></span> |
| <span data-ttu-id="5bfc2-161">Большой атрибут</span><span class="sxs-lookup"><span data-stu-id="5bfc2-161">Large Attribute</span></span> |<span data-ttu-id="5bfc2-162">Ошибки, возникающие, если размер, длина и количество атрибутов превышают установленный предел.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-162">Errors when one or more attributes are larger than the allowed size, length or count.</span></span> |
| <span data-ttu-id="5bfc2-163">Другие</span><span class="sxs-lookup"><span data-stu-id="5bfc2-163">Other</span></span> |<span data-ttu-id="5bfc2-164">Все другие ошибки, не входящие в категории выше.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-164">All other errors that don't fit in the above categories.</span></span> <span data-ttu-id="5bfc2-165">На основе отзывов эти категории будут разделены на подкатегории.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-165">Based on feedback, this category will be split in sub categories.</span></span> |

<span data-ttu-id="5bfc2-166">![Сводка по отчету об ошибках синхронизации](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Категории отчета об ошибках синхронизации](./media/active-directory-aadconnect-health-sync/errorreport02.png)</span><span class="sxs-lookup"><span data-stu-id="5bfc2-166">![Sync Error Report Summary](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Sync Error Report Categories](./media/active-directory-aadconnect-health-sync/errorreport02.png)</span></span>

### <a name="list-of-objects-with-error-per-category"></a><span data-ttu-id="5bfc2-167">Вывод списка объектов с ошибками по категориям</span><span class="sxs-lookup"><span data-stu-id="5bfc2-167">List of objects with error per category</span></span>
<span data-ttu-id="5bfc2-168">Перейдя к каждой категории ошибок, вы увидите список объектов с ошибками, которые под нее подпадают.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-168">Drilling into each category will provide the list of objects having the error in that category.</span></span>
<span data-ttu-id="5bfc2-169">![Список объектов в отчете об ошибках синхронизации](./media/active-directory-aadconnect-health-sync/errorreport03.png)</span><span class="sxs-lookup"><span data-stu-id="5bfc2-169">![Sync Error Report List](./media/active-directory-aadconnect-health-sync/errorreport03.png)</span></span>

### <a name="error-details"></a><span data-ttu-id="5bfc2-170">Сведения об ошибке</span><span class="sxs-lookup"><span data-stu-id="5bfc2-170">Error Details</span></span>
<span data-ttu-id="5bfc2-171">В подробном представлении каждой ошибки содержатся следующие данные:</span><span class="sxs-lookup"><span data-stu-id="5bfc2-171">Following data is available in the detailed view for each error</span></span>

* <span data-ttu-id="5bfc2-172">идентификаторы затронутого *объекта AD*;</span><span class="sxs-lookup"><span data-stu-id="5bfc2-172">Identifiers for the *AD Object* involved</span></span>
* <span data-ttu-id="5bfc2-173">идентификаторы затронутого *объекта Azure AD* (в соответствующем случае);</span><span class="sxs-lookup"><span data-stu-id="5bfc2-173">Identifiers for the *Azure AD Object* involved (as applicable)</span></span>
* <span data-ttu-id="5bfc2-174">описание ошибки и способы ее устранения.</span><span class="sxs-lookup"><span data-stu-id="5bfc2-174">Error description and how to fix</span></span>
* <span data-ttu-id="5bfc2-175">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="5bfc2-175">Related articles</span></span>

![Сведения об ошибках в отчете об ошибках синхронизации](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-the-error-report-as-csv"></a><span data-ttu-id="5bfc2-177">Скачивание отчета об ошибках в формате CVS</span><span class="sxs-lookup"><span data-stu-id="5bfc2-177">Download the error report as CSV</span></span>
<span data-ttu-id="5bfc2-178">Вы можете скачать CSV-файл со сведениями обо всех ошибках с помощью кнопки "Экспорт".</span><span class="sxs-lookup"><span data-stu-id="5bfc2-178">By selecting the "Export" button you can download a CSV file with all the details about all the errors.</span></span>

## <a name="related-links"></a><span data-ttu-id="5bfc2-179">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="5bfc2-179">Related links</span></span>
* [<span data-ttu-id="5bfc2-180">Устранение ошибок синхронизации</span><span class="sxs-lookup"><span data-stu-id="5bfc2-180">Troubleshooting Errors during synchronization</span></span>](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [<span data-ttu-id="5bfc2-181">Синхронизация удостоверений и устойчивость повторяющихся атрибутов</span><span class="sxs-lookup"><span data-stu-id="5bfc2-181">Duplicate Attribute Resiliency</span></span>](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [<span data-ttu-id="5bfc2-182">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="5bfc2-182">Azure AD Connect Health</span></span>](active-directory-aadconnect-health.md)
* [<span data-ttu-id="5bfc2-183">Установка агента Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="5bfc2-183">Azure AD Connect Health Agent Installation</span></span>](active-directory-aadconnect-health-agent-install.md)
* [<span data-ttu-id="5bfc2-184">Операции Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="5bfc2-184">Azure AD Connect Health Operations</span></span>](active-directory-aadconnect-health-operations.md)
* [<span data-ttu-id="5bfc2-185">Использование Azure AD Connect Health с AD FS</span><span class="sxs-lookup"><span data-stu-id="5bfc2-185">Using Azure AD Connect Health with AD FS</span></span>](active-directory-aadconnect-health-adfs.md)
* [<span data-ttu-id="5bfc2-186">Using Azure AD Connect Health with AD DS (Использование Azure AD Connect Health с AD DS)</span><span class="sxs-lookup"><span data-stu-id="5bfc2-186">Using Azure AD Connect Health with AD DS</span></span>](active-directory-aadconnect-health-adds.md)
* [<span data-ttu-id="5bfc2-187">Часто задаваемые вопросы об Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="5bfc2-187">Azure AD Connect Health FAQ</span></span>](active-directory-aadconnect-health-faq.md)
* [<span data-ttu-id="5bfc2-188">Azure AD Connect Health: история версий</span><span class="sxs-lookup"><span data-stu-id="5bfc2-188">Azure AD Connect Health Version History</span></span>](active-directory-aadconnect-health-version-history.md)