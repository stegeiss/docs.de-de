---
title: "Abfragen der DataRowView-Auflistung in einer DataView | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b9070a12-1094-44d6-bb87-a23b50bcb0af
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Abfragen der DataRowView-Auflistung in einer DataView
Das <xref:System.Data.DataView>\-Objekt macht eine aufzählbare Auflistung von <xref:System.Data.DataRowView>\-Objekten verfügbar.  <xref:System.Data.DataRowView> stellt eine angepasste Ansicht eines <xref:System.Data.DataRow>\-Objekts dar und zeigt eine spezielle Version dieses <xref:System.Data.DataRow>\-Objekts in einem Steuerelement an.  Nur eine Version einer <xref:System.Data.DataRow> kann durch ein Steuerelement, wie z. B. <xref:System.Windows.Forms.DataGridView>, angezeigt werden.  Sie können auf die <xref:System.Data.DataRow> zugreifen, die von der <xref:System.Data.DataRowView> durch die <xref:System.Data.DataRowView.Row%2A>\-Eigenschaft der <xref:System.Data.DataRowView> bereitgestellt wird.  Beim Anzeigen von Werten mit einer <xref:System.Data.DataRowView> legt die <xref:System.Data.DataView.RowStateFilter%2A>\-Eigenschaft fest, welche Zeilenversion der zugrunde liegenden <xref:System.Data.DataRow> verfügbar gemacht wird.  Informationen zum Zugriff auf verschiedene Zeilenversionen mithilfe einer <xref:System.Data.DataRow> finden Sie unter [Zeilenstatus und Zeilenversion](../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md).  Da die Auflistung der durch die <xref:System.Data.DataView> bereitgestellten <xref:System.Data.DataRowView>\-Objekte aufzählbar ist, können Sie Abfragen dafür mit [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] durchführen.  
  
 Im folgenden Beispiel wird die `Product`\-Tabelle auf rotfarbige Produkte abgefragt und eine Tabelle aus der Abfrage erstellt.  Eine <xref:System.Data.DataView> wird von der Tabelle erstellt, und die <xref:System.Data.DataView.RowStateFilter%2A>\-Eigenschaft wird auf die Filterung gelöschter und geänderter Zeilen festgelegt.  Die <xref:System.Data.DataView> wird anschließend als Quelle einer LINQ\-Abfrage verwendet, und die geänderten und gelöschten <xref:System.Data.DataRowView>\-Objekte werden an ein <xref:System.Windows.Forms.DataGridView>\-Steuerelement gebunden.  
  
 [!code-csharp[DP DataView Samples#QueryDataView2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#querydataview2)]
 [!code-vb[DP DataView Samples#QueryDataView2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#querydataview2)]  
  
 Im folgenden Beispiel wird eine Tabelle von Produkten aus einer Ansicht erstellt, die an ein <xref:System.Windows.Forms.DataGridView>\-Steuerelement gebunden wird.  Die <xref:System.Data.DataView> wird auf rotfarbige Produkte abgefragt, und die geordneten Ergebnisse werden an ein <xref:System.Windows.Forms.DataGridView>\-Steuerelement gebunden.  
  
 [!code-csharp[DP DataView Samples#QueryDataView1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#querydataview1)]
 [!code-vb[DP DataView Samples#QueryDataView1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#querydataview1)]  
  
## Siehe auch  
 [Datenbindung und LINQ to DataSet](../../../../docs/framework/data/adonet/data-binding-and-linq-to-dataset.md)