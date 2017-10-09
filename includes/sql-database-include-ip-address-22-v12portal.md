
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. <span data-ttu-id="cf3de-101">Войдите в toohello [портал Azure](https://portal.azure.com/) на http://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="cf3de-101">Log in toohello [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="cf3de-102">В hello слева щелкните **ПРОСМОТРЕТЬ все**.</span><span class="sxs-lookup"><span data-stu-id="cf3de-102">In hello left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="cf3de-103">Hello **Обзор** колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="cf3de-103">hello **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="cf3de-104">Найдите и выберите **Серверы SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="cf3de-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="cf3de-105">Hello **серверов SQL Server** колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="cf3de-105">hello **SQL servers** blade is displayed.</span></span>
   
    ![Найдите сервер базы данных SQL Azure на портале hello][b21-FindServerInPortal]
4. <span data-ttu-id="cf3de-107">Для удобства щелкните hello свести к минимуму управления на ранее hello **Обзор** колонку.</span><span class="sxs-lookup"><span data-stu-id="cf3de-107">For convenience, click hello minimize control on hello earlier **Browse** blade.</span></span>
5. <span data-ttu-id="cf3de-108">В текстовом поле фильтра hello начните вводить имя сервера hello.</span><span class="sxs-lookup"><span data-stu-id="cf3de-108">In hello filter text box, start typing hello name of your server.</span></span> <span data-ttu-id="cf3de-109">Отобразится строка.</span><span class="sxs-lookup"><span data-stu-id="cf3de-109">Your row is displayed.</span></span>
6. <span data-ttu-id="cf3de-110">Щелкните строку hello для вашего сервера.</span><span class="sxs-lookup"><span data-stu-id="cf3de-110">Click hello row for your server.</span></span> <span data-ttu-id="cf3de-111">Отобразится колонка для вашего сервера.</span><span class="sxs-lookup"><span data-stu-id="cf3de-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="cf3de-112">На колонке вашего сервера нажмите кнопку **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="cf3de-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="cf3de-113">Hello **параметры** колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="cf3de-113">hello **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="cf3de-114">Щелкните пункт **Брандмауэр**.</span><span class="sxs-lookup"><span data-stu-id="cf3de-114">Click **Firewall**.</span></span> <span data-ttu-id="cf3de-115">Hello **параметры брандмауэра** колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="cf3de-115">hello **Firewall Settings** blade is displayed.</span></span>
   
    ![Последовательно выберите пункты "Параметры" > "Брандмауэр"][b31-SettingsFirewallNavig]
9. <span data-ttu-id="cf3de-117">Щелкните **Добавить IP-адрес клиента**.</span><span class="sxs-lookup"><span data-stu-id="cf3de-117">Click **Add Client IP**.</span></span> <span data-ttu-id="cf3de-118">Введите имя для нового правила в первом текстовом поле hello.</span><span class="sxs-lookup"><span data-stu-id="cf3de-118">Type in a name for your new rule into hello first text box.</span></span>
10. <span data-ttu-id="cf3de-119">Тип в hello низким и высоким IP-адрес значения для hello диапазон tooenable.</span><span class="sxs-lookup"><span data-stu-id="cf3de-119">Type in hello low and high IP address values for hello range you want tooenable.</span></span>
    
    * <span data-ttu-id="cf3de-120">Это может быть удобно toohave hello низкое значение заканчиваться **.0** и hello высокого уровня с **.255**.</span><span class="sxs-lookup"><span data-stu-id="cf3de-120">It can be handy toohave hello low value end with **.0** and hello high with **.255**.</span></span>
    
    ![Добавить tooallow диапазона адресов IP][b41-AddRange]
11. <span data-ttu-id="cf3de-122">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cf3de-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
