---
title: "Предоставление разрешений уровня строки в SQL Server"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a55aaa12-34ab-41cd-9dec-fd255b29258c
caps.latest.revision: "5"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: c086ad08e4170d0033ae32bd730b239d5541d541
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="granting-row-level-permissions-in-sql-server"></a>Предоставление разрешений уровня строки в SQL Server
В некоторых случаях требуется более точное управление доступом к данным, чем простое предоставление, отзыв или отклонение предоставленных разрешений. Например, в приложении базы данных больницы может требоваться ограничение доступа отдельных врачей, чтобы они имели доступ к сведениям только о своих пациентах. Подобные требования существуют во многих областях, включая финансовые, юридические, правительственные и военные приложения. SQL Server 2016 помогает реализовать эти сценарии, предоставляя функциональность [безопасности на уровне строк](https://msdn.microsoft.com/library/dn765131.aspx) , которая упрощает и централизует логику доступа на уровне строк в политике безопасности. В более ранних версиях SQL Server аналогичная функциональность достигается путем использования представлений для внедрения фильтрации на уровне строк.  
  
## <a name="implementing-row-level-filtering"></a>Реализация фильтрации на уровне строк  
 Фильтрация на уровне строк используется для приложений, которые хранят сведения в одной таблице, как в приведенном выше примере приложения больницы. Для реализации фильтрации на уровне строк в каждой строке предусмотрен столбец, в котором задается отличительный параметр, например имя пользователя, метка или другой идентификатор. Вы создаете политику безопасности или представление на основе этой таблицы для фильтрации строк, к которым пользователь имеет доступ. Затем вы создаете параметризованные хранимые процедуры, контролирующие типы запросов, которые может выполнять пользователь.  
  
 В следующем примере показывается, как настроить фильтрацию на уровне строк на основе имени пользователя или имени для входа.  
  
-   Создайте таблицу и добавьте в нее столбец для хранения имени.  
  
-   Включите фильтрацию на уровне строк следующим образом.  
  
    -   Если вы используете SQL Server 2016 или более поздней версии, или [базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/), создайте политику безопасности, который добавляет предикат в таблице, ограничивающий строки возвращаются до тех, которые соответствуют любому текущего пользователя базы данных (с помощью CURRENT_USER() Встроенная функция) или текущее имя входа (с помощью встроенной функции SUSER_SNAME()):  
  
        ```tsql  
        CREATE SCHEMA Security  
        GO  
  
        CREATE FUNCTION Security.userAccessPredicate(@UserName sysname)  
            RETURNS TABLE  
            WITH SCHEMABINDING  
        AS  
            RETURN SELECT 1 AS accessResult  
            WHERE @UserName = SUSER_SNAME()  
        GO  
  
        CREATE SECURITY POLICY Security.userAccessPolicy  
            ADD FILTER PREDICATE Security.userAccessPredicate(UserName) ON dbo.MyTable,  
            ADD BLOCK PREDICATE Security.userAccessPredicate(UserName) ON dbo.MyTable  
        GO  
        ```  
  
    -   При использовании версии SQL Server до 2016 аналогичную функциональность можно реализовать с помощью представления:  
  
        ```tsql  
        CREATE VIEW vw_MyTable  
        AS  
            RETURN SELECT * FROM MyTable  
            WHERE UserName = SUSER_SNAME()  
        GO  
        ```  
  
-   Создайте хранимые процедуры для выбора, вставки, обновления и удаления данных. Если фильтрация осуществляется с помощью политики безопасности, хранимые процедуры должны выполнять эти операции непосредственно в базовой таблице; если же фильтрация осуществляется с помощью представления, хранимые процедуры должны работать с представлением. Политика безопасности или представление будет автоматически фильтровать строки, возвращаемые или изменяемые по запросам пользователя, а хранимая процедура будет обеспечивать более жесткую границу безопасности, чтобы предотвратить прямой доступ пользователей через успешно выполняемые запросы, которые могут определять наличие отфильтрованных данных.  
  
-   Для хранимых процедур, которые вставляют данные, получайте имя пользователя при помощи той же функции, которая указана в политике безопасности или в представлении, и вставляйте это значение в столбец UserName.  
  
-   Запретите роли `public` всякий доступ к таблицам (и представлениям, если они применяются). Пользователи не смогут наследовать права доступа от других ролей базы данных, поскольку предикат фильтра основан на имени пользователя или имени для входа, а не на ролях.  
  
-   Предоставьте ролям базы данных право доступа EXECUTE для хранимых процедур. Пользователи смогут иметь доступ к данным только через предоставленные хранимые процедуры.  
  
## <a name="external-resources"></a>Внешние ресурсы  
 Дополнительные сведения см. в следующих ресурсах.  
  
|||  
|-|-|  
|[Реализация безопасности на уровне строк и ячеек в конфиденциальных базах данных с помощью SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=98227) на веб-сайте SQL Server TechCenter.|Описание использования безопасности на уровне строки и ячейки для соответствия требованиям безопасности конфиденциальной базы данных.|  
  
## <a name="see-also"></a>См. также  
 [Безопасность на уровне строк](https://msdn.microsoft.com/library/dn765131.aspx)  
 [Защита приложений ADO.NET](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)  
 [Общие сведения о безопасности SQL Server](../../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)  
 [Сценарии безопасности приложений в SQL Server](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)  
 [Управление разрешениями с использованием хранимых процедур в SQL Server](../../../../../docs/framework/data/adonet/sql/managing-permissions-with-stored-procedures-in-sql-server.md)  
 [Написание безопасного динамического кода SQL в SQL Server](../../../../../docs/framework/data/adonet/sql/writing-secure-dynamic-sql-in-sql-server.md)  
 [Центр разработчиков наборов данных и управляемых поставщиков ADO.NET](http://go.microsoft.com/fwlink/?LinkId=217917)
