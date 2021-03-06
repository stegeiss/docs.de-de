---
title: "SKIP (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "ESQL"
ms.assetid: e2139412-8ea4-451b-8f10-91af18dfa3ec
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# SKIP (Entity SQL)
Physisches Paging kann mithilfe der SKIP\-Unterklausel in der ORDER BY\-Klausel durchgeführt werden. SKIP kann nicht ohne die ORDER BY\-Klausel verwendet werden.  
  
## Syntax  
  
```  
  
[ SKIP n ]  
```  
  
## Argumente  
 `n`  
 Die Anzahl zu überspringender Elemente.  
  
## Hinweise  
 Wenn eine ORDER BY\-Klausel den Ausdruck SKIP als Unterklausel enthält, werden die Ergebnisse den Sortierangaben entsprechend sortiert, und das Resultset enthält die Zeilen, die auf den SKIP\-Ausdruck folgen. Mit SKIP 5 werden beispielsweise die ersten fünf Zeilen übersprungen und nur die Zeilen ab der sechsten Zeile zurückgegeben.  
  
> [!NOTE]
>  Eine [!INCLUDE[esql](../../../../../../includes/esql-md.md)]\-Abfrage ist ungültig, wenn im selben Abfrageausdruck sowohl ein TOP\-Modifizierer als auch eine SKIP\-Unterklausel vorhanden sind. In der Abfrage sollte der TOP\-Ausdruck in einen LIMIT\-Ausdruck geändert werden.  
  
> [!NOTE]
>  Die Verwendung von SKIP mit ORDER BY für Nichtschlüsselspalten kann in [!INCLUDE[ssVersion2000](../../../../../../includes/ssversion2000-md.md)] zu falschen Ergebnissen führen. Es kann vorkommen, dass mehr als die angegebene Anzahl von Zeilen übersprungen wird, wenn die Nichtschlüsselspalte Daten doppelt enthält. Der Grund dafür ist die Übersetzung von SKIP für [!INCLUDE[ssVersion2000](../../../../../../includes/ssversion2000-md.md)]. Im folgenden Code können beispielsweise mehr als fünf Zeilen übersprungen werden, wenn `E.NonKeyColumn` Werte doppelt enthält:  
>   
>  `SELECT [E] FROM Container.EntitySet AS [E] ORDER BY [E].[NonKeyColumn] DESC SKIP 5L`  
  
 In der [!INCLUDE[esql](../../../../../../includes/esql-md.md)]\-Abfrage in [diesem](https://msdn.microsoft.com/library/bb738702\(v=vs.100\).aspx#_ESQL) Beispiel wird der ORDER BY\-Operator mit SKIP verwendet, um für die von der SELECT\-Anweisung zurückgegebenen Objekte die zu verwendende Sortierreihenfolge anzugeben.  
  
## Siehe auch  
 [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md)   
 [Gewusst wie: Seitenweise durch Abfrageresultate navigieren](http://msdn.microsoft.com/de-de/ffc0f920-e7de-42e0-9b12-ef356421d030)   
 [Paging](../../../../../../docs/framework/data/adonet/ef/language-reference/paging-entity-sql.md)   
 [TOP](../../../../../../docs/framework/data/adonet/ef/language-reference/top-entity-sql.md)