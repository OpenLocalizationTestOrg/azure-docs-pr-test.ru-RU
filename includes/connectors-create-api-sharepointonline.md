

<span data-ttu-id="5c219-101">Для подключения к **SharePoint Online** необходимо предоставить свое удостоверение (имя пользователя и пароль, учетные данные смарт-карты и т. п.).</span><span class="sxs-lookup"><span data-stu-id="5c219-101">In order to connect to **SharePoint Online**, you need to provide your identity (username and password, smart card credentials, etc.) to SharePoint Online.</span></span> <span data-ttu-id="5c219-102">После прохождения аутентификации вы сможете использовать соединитель SharePoint Online в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="5c219-102">Once you've been authenticated, you can proceed to use the SharePoint Online connector  in your logic app.</span></span> 

<span data-ttu-id="5c219-103">Чтобы войти в SharePoint для создания **подключения**, которое будет использоваться в вашем приложении логики, в конструкторе приложений логики сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5c219-103">While on the designer of your logic app, follow these steps to sign into SharePoint to create the **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="5c219-104">В поле поиска введите "SharePoint" и дождитесь возвращения всех триггеров и действий, относящихся к SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="5c219-104">Enter SharePoint in the search box and wait for the search to return all triggers and actions related to SharePoint Online:</span></span>   
   ![Настройка SharePoint][1]  
2. <span data-ttu-id="5c219-106">Выберите триггер **SharePoint Online - When a file is created** (SharePoint Online — при создании файла).</span><span class="sxs-lookup"><span data-stu-id="5c219-106">Select the **SharePoint Online - When a file is created** trigger</span></span>  
3. <span data-ttu-id="5c219-107">Выберите **Sign in to SharePoint Online** (Вход в SharePoint Online).</span><span class="sxs-lookup"><span data-stu-id="5c219-107">Select **Sign in to SharePoint Online**:</span></span>   
   <span data-ttu-id="5c219-108">![Настройка SharePoint][2]</span><span class="sxs-lookup"><span data-stu-id="5c219-108">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="5c219-109">Укажите учетные данные SharePoint, чтобы войти и пройти аутентификацию в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5c219-109">Provide your SharePoint credentials to sign in to authenticate with SharePoint</span></span>   
   ![Настройка SharePoint][3]     
5. <span data-ttu-id="5c219-111">После выполнения аутентификации вы будете перенаправлены к своему приложению логики.</span><span class="sxs-lookup"><span data-stu-id="5c219-111">After the authentication completes you'll be redirected to your logic app.</span></span> <span data-ttu-id="5c219-112">Таким образом, подключение было создано.</span><span class="sxs-lookup"><span data-stu-id="5c219-112">That's it, the connection has been created.</span></span> <span data-ttu-id="5c219-113">Внизу отобразится сообщение о том, что вы подключены к SharePoint.</span><span class="sxs-lookup"><span data-stu-id="5c219-113">Notice the message at the bottom that indicates that you are now connected to SharePoint.</span></span>  
   ![Настройка SharePoint][4]  
6. <span data-ttu-id="5c219-115">Затем можно будет добавить другие триггеры и действия, необходимые для завершения приложения логики.</span><span class="sxs-lookup"><span data-stu-id="5c219-115">You can then add other triggers and actions that you need to complete your logic app.</span></span>   

[1]: ./media/connectors-create-api-sharepointonline/connectionconfig1.png
[2]: ./media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ./media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ./media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ./media/connectors-create-api-sharepointonline/connectionconfig5.png
