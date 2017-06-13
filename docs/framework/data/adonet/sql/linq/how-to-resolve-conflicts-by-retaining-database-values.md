---
title: "Как разрешать конфликты параллелизма путем сохранения значений базы данных | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b475cf72-9e64-4f6e-99c1-af7737bc85ef
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Как разрешать конфликты параллелизма путем сохранения значений базы данных
Чтобы согласовать различия между ожидаемыми и фактическими значениями базы данных до повторной отправки изменений, можно воспользоваться <xref:System.Data.Linq.RefreshMode> для сохранения значений, найденных в базе данных.  Текущие значения в объектной модели при этом перезаписываются.  Для получения дополнительной информации см. [Оптимистичный параллелизм. Общие сведения](../../../../../../docs/framework/data/adonet/sql/linq/optimistic-concurrency-overview.md).  
  
> [!NOTE]
>  Во всех случаях запись на клиенте сначала обновляется путем извлечения обновленных данных из базы данных.  Это действие гарантирует успешное выполнение следующей попытки обновления при тех же проверках параллелизма.  
  
## Пример  
 В данном сценарии, когда Пользователь1 пытается отправить изменения, возникает исключение <xref:System.Data.Linq.ChangeConflictException>, поскольку Пользователь2 в это время изменил столбцы "Помощник" и "Отдел".  Эта ситуация представлена в следующей таблице.  
  
||Диспетчер|Помощник|Отдел|  
|------|---------------|--------------|-----------|  
|Исходное состояние базы данных при отправке запросов Пользователем1 и Пользователем2.|Алексеи|Мария|Продажи|  
|Пользователь1 готовится отправить изменения.|Алексей||Маркетинг|  
|Пользователь2 уже отправил изменения.||Инна|Служба|  
  
 Пользователь1 решает устранить этот конфликт путем перезаписи текущих значений из объектной модели более новыми значениями базы данных.  
  
 При устранении Пользователем1 конфликта с помощью <xref:System.Data.Linq.RefreshMode> результат в базе данных будет соответствовать данным в следующей таблице.  
  
||Диспетчер|Помощник|Отдел|  
|------|---------------|--------------|-----------|  
|Новое состояние после устранения конфликта.|Алексеи<br /><br /> \(исходное значение\)|Инна<br /><br /> \(от Пользователя2\)|Служба<br /><br /> \(от Пользователя2\)|  
  
 В следующем примере кода показано, как перезаписать текущие значения из объектной модели значениями базы данных  \(проверка или пользовательская обработка конфликтов отдельных членов не выполняется\).  
  
 [!code-csharp[System.Data.Linq.RefreshMode#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.refreshmode/cs/program.cs#1)]
 [!code-vb[System.Data.Linq.RefreshMode#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.refreshmode/vb/module1.vb#1)]  
  
## См. также  
 [Как управлять конфликтами изменений](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)