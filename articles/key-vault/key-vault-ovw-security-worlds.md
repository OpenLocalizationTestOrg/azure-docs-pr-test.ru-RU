---
ms.assetid: 
title: "механизмы обеспечения безопасности хранилища ключей aaaAzure | Документы Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="f0462-102">Системы безопасности и географические ограничения Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f0462-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="f0462-103">Azure Key Vault —это мультитенантная служба, которая использует пул аппаратных модулей безопасности в каждом расположении Azure.</span><span class="sxs-lookup"><span data-stu-id="f0462-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="f0462-104">Все аппаратные модули безопасности в Azure участках hello одном географическом регионе совместно используют hello и та же граница шифрования (системы безопасности Thales).</span><span class="sxs-lookup"><span data-stu-id="f0462-104">All HSMs at Azure locations in hello same geographic region share hello same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="f0462-105">Например Восток США и Западная часть США совместно использовать hello же системы безопасности, так как они принадлежат toohello США географическое расположение.</span><span class="sxs-lookup"><span data-stu-id="f0462-105">For example, East US and West US share hello same security world because they belong toohello US geo location.</span></span> <span data-ttu-id="f0462-106">Аналогичным образом все расположения Azure, в общей папке на японском языке hello же системы безопасности и всех расположений Azure в Австралии, Индии и так далее.</span><span class="sxs-lookup"><span data-stu-id="f0462-106">Similarly, all Azure locations in Japan share hello same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="f0462-107">Поведение резервного копирования и восстановления</span><span class="sxs-lookup"><span data-stu-id="f0462-107">Backup and restore behavior</span></span>

<span data-ttu-id="f0462-108">Резервная копия ключа из хранилища ключей в одно расположение Azure можно восстановить tooa хранилища ключей в другом расположении Azure, при условии, что оба этих условия истинны:</span><span class="sxs-lookup"><span data-stu-id="f0462-108">A backup taken of a key from a key vault in one Azure location can be restored tooa key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="f0462-109">Оба hello Azure расположения принадлежат toohello одном географическом расположении</span><span class="sxs-lookup"><span data-stu-id="f0462-109">Both of hello Azure locations belong toohello same geographical location</span></span>
- <span data-ttu-id="f0462-110">Хранилищ ключей hello принадлежать toohello одной подписке</span><span class="sxs-lookup"><span data-stu-id="f0462-110">Both of hello key vaults belong toohello same Azure subscription</span></span>

<span data-ttu-id="f0462-111">Например, создание резервных копий по данной подписке ключа в хранилище ключей в западной Индии, может быть только восстановленной tooanother хранилища ключей в hello той же подписке и географическое расположение; Западной Индии, Южной Индии и центральной Индии.</span><span class="sxs-lookup"><span data-stu-id="f0462-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored tooanother key vault in hello same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="f0462-112">Регионы и продукты</span><span class="sxs-lookup"><span data-stu-id="f0462-112">Regions and products</span></span>

- [<span data-ttu-id="f0462-113">Регионы Azure</span><span class="sxs-lookup"><span data-stu-id="f0462-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="f0462-114">Доступность продуктов по регионам</span><span class="sxs-lookup"><span data-stu-id="f0462-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="f0462-115">Регионами являются миров сопоставленных toosecurity, показанное как основные заголовки в таблицах hello:</span><span class="sxs-lookup"><span data-stu-id="f0462-115">Regions are mapped toosecurity worlds, shown as major headings in hello tables:</span></span>

<span data-ttu-id="f0462-116">Hello продуктов по статье области, например, hello **Americas** вкладка содержит Восток США, центральной ЧАСТИ США, ЗАПАД США всех областей Americas toohello сопоставления.</span><span class="sxs-lookup"><span data-stu-id="f0462-116">In hello products by region article, for example, hello **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping toohello Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="f0462-117">Исключением являются восточная часть США (US DOD) и центральная часть США (US DOD), которые имеют собственные системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="f0462-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="f0462-118">Аналогично, на hello **Europe** вкладке СЕВЕРНОЙ ЕВРОПЕ и ЗАПАДНОЙ ЕВРОПЕ сопоставляются toohello Европейского региона.</span><span class="sxs-lookup"><span data-stu-id="f0462-118">Similarly, on hello **Europe** tab, NORTH EUROPE and WEST EUROPE both map toohello Europe region.</span></span> <span data-ttu-id="f0462-119">Hello это также верно для hello **Азиатско-Тихоокеанский регион** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f0462-119">hello same is also true on hello **Asia Pacific** tab.</span></span>



