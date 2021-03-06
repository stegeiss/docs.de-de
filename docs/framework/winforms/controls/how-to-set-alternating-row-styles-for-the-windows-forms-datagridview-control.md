---
title: "Gewusst wie: Festlegen von abwechselnden Zeilenstilen f&#252;r das DataGridView-Steuerelement in Windows Forms | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Datenblätter, Zeilenformate"
  - "DataGridView-Steuerelement [Windows Forms], Zeilenformate"
  - "Zeilen, Datenblätter"
ms.assetid: 699ef759-458c-426d-ac87-7c7e71b018ae
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Gewusst wie: Festlegen von abwechselnden Zeilenstilen f&#252;r das DataGridView-Steuerelement in Windows Forms
Tabellendaten werden oft in einem Ledger\-ähnlichen Format präsentiert, bei dem die einzelnen Zeilen abwechselnde Hintergrundfarben haben.  Dieses Format erleichtert es dem Benutzer, zu erkennen, welche Zellen sich in jeder Zeile befinden, insbesondere bei breiten Tabellen mit vielen Spalten.  
  
 Mit dem <xref:System.Windows.Forms.DataGridView>\-Steuerelement können Sie vollständige Stilinformationen für abwechselnde Zeilen angeben.  Auf diese Weise können Sie Stileigenschaften wie Vordergrundfarbe und Schriftart zusätzlich zur Hintergrundfarbe verwenden, um abwechselnde Zeilen zu unterscheiden.  
  
 Visual Studio bietet Unterstützung für diese Aufgabe.  Siehe auch [Gewusst wie: Festlegen von abwechselnden Zeilenstilen für das Windows Forms\-Steuerelement DataGridView mithilfe des Designers](http://msdn.microsoft.com/library/3z9sk148%20\(v=vs.110\)).  
  
### So legen Sie abwechselnde Zeilenstile programmgesteuert fest  
  
-   Legen Sie die Eigenschaften der <xref:System.Windows.Forms.DataGridViewCellStyle>\-Objekte fest, die von der <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A>\- und der <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A>\-Eigenschaft der <xref:System.Windows.Forms.DataGridView> zurückgegeben werden.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#068](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#068)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#068](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#068)]  
  
    > [!NOTE]
    >  Die Stile, die über die <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A>\- und die <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A>\-Eigenschaft angegeben sind, überschreiben die Stile, die auf Spalten\- und <xref:System.Windows.Forms.DataGridView>\-Ebene festgelegt sind, werden jedoch durch die Stile überschrieben, die auf der einzelnen Zeilen\- und Zellenebene festgelegt sind.  Weitere Informationen finden Sie unter [Zellstile im DataGridView\-Steuerelement in Windows Forms](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md).  
  
## Kompilieren des Codes  
 Für dieses Beispiel benötigen Sie Folgendes:  
  
-   Ein <xref:System.Windows.Forms.DataGridView>\-Steuerelement namens `dataGridView1`.  
  
-   Verweise auf die Assemblys <xref:System?displayProperty=fullName>, <xref:System.Drawing?displayProperty=fullName> und <xref:System.Windows.Forms?displayProperty=fullName>.  
  
## Robuste Programmierung  
 Um maximale Skalierbarkeit zu erreichen, sollten Sie <xref:System.Windows.Forms.DataGridViewCellStyle>\-Objekte für mehrere Zeilen, Spalten oder Zellen, in denen dieselben Stile verwendet werden, gemeinsam verwenden, anstatt die Stileigenschaften für jedes einzelne Element festzulegen.  Weitere Informationen finden Sie unter [Empfohlene Vorgehensweisen für das Skalieren des DataGridView\-Steuerelements in Windows Forms](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md).  
  
## Siehe auch  
 <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewCellStyle>   
 [Grundlegende Formatierungen und Formate im DataGridView\-Steuerelement in Windows Forms](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)   
 [Zellstile im DataGridView\-Steuerelement in Windows Forms](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)   
 [Empfohlene Vorgehensweisen für das Skalieren des DataGridView\-Steuerelements in Windows Forms](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md)   
 [Gewusst wie: Festlegen von Schriftart\- und Farbstilen im DataGridView\-Steuerelement in Windows Forms](../../../../docs/framework/winforms/controls/how-to-set-font-and-color-styles-in-the-windows-forms-datagridview-control.md)