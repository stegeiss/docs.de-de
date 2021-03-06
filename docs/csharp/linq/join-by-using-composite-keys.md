---
title: "Verknüpfen mithilfe eines zusammengesetzten Schlüssels"
description: "Vorgehensweise: Verknüpfen mithilfe eines zusammengesetzten Schlüssels."
keywords: .NET, .NET Core, C#
author: BillWagner
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: da70b54d-3213-45eb-8437-fbe75cbcf935
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f504c9dabcd7ca2d198d58c6d81e1fde1052e3be
ms.lasthandoff: 03/13/2017

---
# <a name="join-by-using-composite-keys"></a>Verknüpfen mithilfe eines zusammengesetzten Schlüssels

In diesem Beispiel erfahren Sie, wie sie Verknüpfungsvorgänge durchführen können, in denen Sie mehr als einen Schlüssel zur Definition einer Übereinstimmung verwenden möchten. Dies können Sie mithilfe eines zusammengesetzten Schlüssels machen. Ein zusammengesetzter Schlüssel wird als anonymer oder benannter Typ mit den Werten, die Sie vergleichen möchten, erstellt. Wenn die Abfragevariable über Methodengrenzen hinweg übergeben wird, verwenden Sie einen benannten Typ, der für den Schlüssel <xref:System.Object.Equals%2A> und <xref:System.Object.GetHashCode%2A> außer Kraft setzt. Der Name der Eigenschaften und die Reihenfolge, in der diese auftreten, muss in jedem Schlüssel identisch sein.  
  
## <a name="example"></a>Beispiel  
 In folgendem Beispiel erfahren Sie, wie Sie einen zusammengesetzten Schlüssel verwenden können, um Daten aus drei Tabellen zu verknüpfen:  
  
```csharp  
var query = from o in db.Orders  
    from p in db.Products  
    join d in db.OrderDetails   
        on new {o.OrderID, p.ProductID} equals new {d.OrderID,        d.ProductID} into details  
        from d in details  
        select new {o.OrderID, p.ProductID, d.UnitPrice};  
```  
  
 Typrückschluss für zusammengesetzte Schlüssel hängt von den Namen der Eigenschaften in den Schlüsseln und deren Reihenfolge ab. Wenn die Eigenschaften der Quellsequenz nicht dieselben Namen haben, müssen Sie ihnen im Schlüssel neue Namen zuweisen. Wenn in den Tabellen `Orders` und `OrderDetails` beispielsweise unterschiedliche Namen für die Spalten verwendet werden, können Sie zusammengesetzte Schlüssel erstellen, indem Sie identische Namen in den anonymen Typen zuweisen:  
  
```csharp  
join...on new {Name = o.CustomerName, ID = o.CustID} equals   
    new {Name = d.CustName, ID = d.CustID }  
```  
  
 Zusammengesetzte Schlüssel können auch in einer `group`-Klausel verwendet werden.  

## <a name="see-also"></a>Siehe auch  
 [LINQ-Abfrageausdrücke](index.md)   
 [Join-Klausel](../language-reference/keywords/join-clause.md)   
 [group-Klausel](../language-reference/keywords/group-clause.md)
