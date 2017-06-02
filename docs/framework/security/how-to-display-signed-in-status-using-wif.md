---
title: "Практическое руководство. Отображение состояния входа с помощью WIF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4d1174e4-5397-4962-9a5f-3b1ad7b3fc14
caps.latest.revision: 6
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 6
---
# Практическое руководство. Отображение состояния входа с помощью WIF
## Применение  
  
-   Основой \(WIF\) 4.5 идентификатора Microsoft® Windows®  
  
-   ASP.NET® веб\-форм  
  
## Сводка  
 В этом разделе описывается, как отобразить состояние данных для входа в WIF\- позволенном приложения ASP.NET.  WIF предоставляет механизм для создания приложения заявк\- зависимым и управления проверка подлинности и авторизация для ресурсов приложения.  
  
## Содержание  
  
-   Обзор  
  
-   Сводка действий  
  
-   Шаг 1.задайте идентификатор и получения расширения  
  
-   Шаг 2.создание приложения ASP.NET проверяющей стороны  
  
-   Шаг 3 — предоставление локальной службы маркеров безопасности разработки подлинность пользователей  
  
-   Шаг 4 — измените приложение ASP.NET для отображения информации о состоянии вход  
  
-   Шаг 5.запуск интеграцию между WIF и приложением ASP.NET  
  
## Обзор  
 В этом разделе показано, как создать простое приложение, поддерживающее утверждения с помощью WIF и успехом, подписан ли пользователь, или нет.  Следующие действия используют локальной службы маркеров безопасности разработки, включается с расширением Visual Studio идентификатора и доступа.  Локальная служба маркеров безопасности предназначена для разработки и тестирования среды разработки предоставить простой метод интеграции, в приложение.  Она не должна использоваться в производственной среде, оно не выполняет проверку подлинности и реальную учетные данные не требуются.  Однако императивного кода в следующих шагах одинаковы для элемента готового приложения с помощью реальную проверку подлинности.  
  
## Сводка действий  
  
-   Шаг 1.задайте идентификатор и получения расширения  
  
-   Шаг 2.создание приложения ASP.NET проверяющей стороны  
  
-   Шаг 3 — предоставление локальной службы маркеров безопасности разработки подлинность пользователей  
  
-   Шаг 4 — измените приложение ASP.NET для отображения информации о состоянии вход  
  
-   Шаг 5.запуск интеграцию между WIF и приложением ASP.NET  
  
## Шаг 1.задайте идентификатор и получения расширения  
 Этот шаг описывается настройка идентификатор и получения расширения в Visual Studio 2012.  Это расширение автоматизирует процесс настройки приложений взаимодействия с конечными точками службы маркеров безопасности.  
  
#### Идентификатор задания и получения расширения  
  
1.  Запустите Visual Studio в режиме повышенными правами администратора.  
  
2.  В Visual Studio щелкните **Сервис** и щелкните **Диспетчер расширений**.  Окно **Диспетчер расширений**.  
  
3.  В **Диспетчер расширений** щелкните узел **сетевые расширения** в левой меню, затем выбирает **Галерея Visual Studio**.  
  
4.  В правом верхнем углу **Диспетчер расширений**, поиск *идентификатора и доступа к ним*.  
  
5.  Элемент **Удостоверение и доступ** появится в результаты поиска.  Щелкните его, а затем щелкните **Загрузить**.  
  
6.  Откроется диалоговое окно **Загрузить и установить**.  Если соглашаетесь с условиями лицензии, щелкните **Установить**.  
  
7.  При расширении **Удостоверение и доступ** закончило обработку задавать, перезапустите Visual Studio в режиме администратора.  
  
## Шаг 2.создание приложения ASP.NET проверяющей стороны  
 Этот шаг описывается создание приложения веб\-форм ASP.NET проверяющей стороны, интегрируется с WIF.  
  
#### Создание простого приложения ASP.NET  
  
1.  Запустите Visual Studio и щелкните **Файл**, **Создать** и **Проект**.  
  
2.  В поле **Создать проект**, щелкните **Приложение веб\-форм ASP.NET**.  
  
3.  В поле **Имя** введите `TestApp` и нажмите клавишу **ОК**.  
  
## Шаг 3 — предоставление локальной службы маркеров безопасности разработки подлинность пользователей  
 Этот шаг описание включения локальной службы маркеров безопасности разработки в приложении.  Локальная служба маркеров безопасности разработки включена с помощью расширения идентификатора и доступа для Visual Studio.  
  
#### Включить локальной службы маркеров безопасности разработки в приложении ASP.NET  
  
1.  В Visual Studio щелкните правой кнопкой мыши проект **TestApp** в **Обозреватель решений**, а затем выберите **Удостоверение и доступ**.  
  
2.  Окно **Удостоверение и доступ**.  В области **Поставщики**, выберите **Тестировать приложение с помощью локальной STS\-разработки** и нажмите кнопку **Применить**.  
  
## Шаг 4 — измените приложение ASP.NET для отображения информации о состоянии вход  
 Этот шаг описывается, как изменить приложение ASP.NET динамически отображать, подписан ли текущий пользователь в.  После того как поставщик службы маркеров безопасности настроен, WIF обрабатывает входящие служба.  Теперь необходимо настроить код приложения для возвращения результата проверки подлинности.  
  
#### Отображение состояния данных для входа  
  
1.  В Visual Studio откройте файл **Default.aspx** в проекте **TestApp**.  
  
2.  Замените существующую разметку в файл **Default.aspx** следующей разметкой.  
  
    ```  
    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>  
  
    <!DOCTYPE html>  
  
    <html>  
    <head runat="server">  
        <title>Logged In Status</title>  
    </head>  
    <body>  
        <asp:label ID="myLabel" runat="server" />  
    </body>  
    </html>  
    ```  
  
3.  Сохраните **Default.aspx**, а затем открыть его с именем файла кода программной части **Default.aspx.cs**.  
  
    > [!NOTE]
    >  **Default.aspx.cs** может скрыть под **Default.aspx** в обозревателе решений.  Если **Default.aspx.cs** не отображается, разверните **Default.aspx**, щелкнув знак треугольнике рядом с ним.  
  
4.  Замените существующий код в **Default.aspx.cs** следующим кодом:  
  
    ```csharp  
    using System;  
    using System.Web.UI;  
    using System.Security.Claims;  
  
    namespace TestApp  
    {  
        protected void Page_Load(object sender, EventArgs e)  
        {  
            ClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as ClaimsPrincipal;  
  
            if (claimsPrincipal != null)  
            {  
                myLabel.Text = "You are signed in.";  
            }  
            else  
            {  
                myLabel.Text = "You are not signed in.";  
            }  
        }  
    }  
    ```  
  
5.  Сохраните **Default.aspx.cs** и построение приложения.  
  
## Шаг 5.запуск интеграцию между WIF и приложением ASP.NET  
 Этот шаг теста описание интеграции между WIF и приложением ASP.NET.  
  
#### Выполнять интеграцию между WIF и ASP.NET  
  
1.  В Visual Studio нажмите клавишу **F5** для запуска отладки приложения.  Если ошибки не найдены, будет открыто новое окно браузера.  
  
2.  Можно заметить, что браузер автоматически перенаправляет в просьбу в службу маркеров безопасности, а затем открыть страницу Default.aspx.  Если WIF правильно настроен, необходимо проверить, что сайт отображается следующий текст: **При подписании «в»**.