---
title: "Vorgehensweise: Erstellen eines benutzerdefinierten Aktivit&#228;tsdesigners | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2f3aade6-facc-44ef-9657-a407ef8b9b31
caps.latest.revision: 25
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 25
---
# Vorgehensweise: Erstellen eines benutzerdefinierten Aktivit&#228;tsdesigners
Benutzerdefinierte Aktivitätsdesigner werden in der Regel implementiert, um die zugehörigen Aktivitäten mit anderen Aktivitäten zusammenzusetzen, deren Designer mit ihnen auf der Entwurfsoberfläche abgelegt werden können.Für diese Funktionalität muss ein benutzerdefinierter Aktivitätsdesigner eine "Ablagezone" bereitstellen, in der eine beliebige Aktivität platziert werden kann, sowie die Funktionen zur Verwaltung der daraus resultierenden Auflistung von Elementen auf der Entwurfsoberfläche.In diesem Thema wird beschrieben, wie ein benutzerdefinierter Aktivitätsdesigner erstellt wird, der eine solche Ablagezone enthält und die Bearbeitungsfunktionen zur Verwaltung der Auflistung von Designerelementen bereitstellt.  
  
 Benutzerdefinierte Aktivitätsdesigner erben in der Regel von <xref:System.Activities.Presentation.ActivityDesigner>. Dies ist der standardmäßige Designertyp für alle Aktivitäten ohne bestimmten Designer.Dieser Typ stellt Entwurfszeitfunktionen für die Interaktion mit dem Eigenschaftenraster und die Konfiguration von grundlegenden Aspekten wie Farbe und Symbole bereit.  
  
 <xref:System.Activities.Presentation.ActivityDesigner> verwendet zwei Hilfssteuerelemente \(<xref:System.Activities.Presentation.WorkflowItemPresenter> und <xref:System.Activities.Presentation.WorkflowItemsPresenter>\), die das Entwickeln benutzerdefinierter Aktivitätsdesigner vereinfachen.Sie behandeln die allgemeine Funktionalität wie Ziehen und Ablegen von untergeordneten Elementen sowie Löschen, Auswählen und Hinzufügen dieser untergeordneten Elemente.Das <xref:System.Activities.Presentation.WorkflowItemPresenter>\-Element unterstützt ein einzelnes untergeordnetes Benutzeroberflächenelement, das die "Ablagezone" bereitstellt. <xref:System.Activities.Presentation.WorkflowItemsPresenter> unterstützt mehrere Benutzeroberflächenelemente, darunter zusätzliche Funktionalität z. B. zum Sortieren, Verschieben, Löschen und Hinzufügen von untergeordneten Elementen.  
  
 Der zweite Hauptaspekt bei der Implementierung eines benutzerdefinierten Aktivitätsdesigners betrifft die Methode zur Bindung der grafischen Bearbeitungen an die Instanz der im Designer bearbeiteten Objekte im Arbeitsspeicher mit der [!INCLUDE[avalon2](../../../includes/avalon2-md.md)]\-Datenbindung.Hierzu dient die Modellelementstruktur, die auch zur Aktivierung der Änderungsbenachrichtigung und der Nachverfolgung von Ereignissen wie Zustandsänderungen verwendet wird.  
  
 In diesem Thema werden zwei Prozeduren beschrieben.  
  
1.  Die erste Prozedur beschreibt, wie ein benutzerdefinierter Aktivitätsdesigner mit <xref:System.Activities.Presentation.WorkflowItemPresenter> erstellt wird, der die Ablagezone für andere Aktivitäten bereitstellt.Diese Prozedur basiert auf dem [Benutzerdefinierte zusammengesetzte Designer \- Workflowelementpräsentation](../../../docs/framework/windows-workflow-foundation/samples/custom-composite-designers-workflow-item-presenter.md)\-Beispiel.  
  
2.  Die zweite Prozedur beschreibt, wie ein benutzerdefinierter Aktivitätsdesigner mit <xref:System.Activities.Presentation.WorkflowItemsPresenter> erstellt wird, der die zur Bearbeitung einer Auflistung von Elementen benötigten Funktionen bereitstellt.Diese Prozedur basiert auf dem [Benutzerdefinierte zusammengesetzte Designer – Workflowelementpräsentation](../../../docs/framework/windows-workflow-foundation/samples/custom-composite-designers-workflow-items-presenter.md)\-Beispiel.  
  
### So erstellen Sie einen benutzerdefinierten Aktivitätsdesigner, der eine Ablagezone bereitstellt, mit WorkflowItemPresenter  
  
1.  Starten Sie [!INCLUDE[vs2010](../../../includes/vs2010-md.md)].  
  
2.  Zeigen Sie im Menü **Datei** auf **Neu**, und klicken Sie dann auf **Projekt**.  
  
     Das Dialogfeld **Neues Projekt** wird angezeigt.  
  
3.  Wählen Sie im Bereich **Installierte Vorlagen** in der von Ihnen bevorzugten Sprachkategorie die Option **Windows**.  
  
4.  Wählen Sie im Bereich **Vorlagen** die Option **WPF\-Anwendung** aus.  
  
5.  Geben Sie im Feld **Name**`UsingWorkflowItemPresenter` ein.  
  
6.  Geben Sie im Feld **Speicherort** das Verzeichnis ein, in dem das Projekt gespeichert werden soll, oder klicken Sie auf **Durchsuchen**, um zu dem Verzeichnis zu navigieren.  
  
7.  Akzeptieren Sie im Feld **Projektmappe** den Standardwert.  
  
8.  Klicken Sie auf **OK**.  
  
9. Klicken Sie im **Projektmappen\-Explorer** mit der rechten Maustaste auf die Datei "MainWindows.xaml", wählen Sie **Löschen**, und bestätigen Sie den Vorgang im Dialogfeld **Microsoft Visual Studio** mit **OK**.  
  
10. Klicken Sie im **Projektmappen\-Explorer** mit der rechten Maustaste auf das Projekt "UsingWorkflowItemPresenter", und wählen Sie **Hinzufügen** und dann **Neues Element…**, um das Dialogfeld **Neues Element hinzufügen** zu öffnen. Wählen Sie dann im Abschnitt **Installierte Vorlagen** auf der linken Seite die Kategorie **WPF**.  
  
11. Wählen Sie die Vorlage **Fenster \(WPF\)** aus, benennen Sie sie in `RehostingWFDesigner` um, und klicken Sie auf **Hinzufügen**.  
  
12. Öffnen Sie die Datei "RehostingWFDesigner.xaml", und fügen Sie den folgenden Code ein, um die Benutzeroberfläche für die Anwendung zu definieren.  
  
    ```  
  
    <Window x:Class=" UsingWorkflowItemPresenter.RehostingWFDesigner"  
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
            xmlns:sapt="clr-namespace:System.Activities.Presentation.Toolbox;assembly=System.Activities.Presentation"  
            xmlns:sys="clr-namespace:System;assembly=mscorlib"  
            Title="Window1" Height="600" Width="900">  
        <Window.Resources>  
            <sys:String x:Key="AssemblyName">System.Activities, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35</sys:String>  
        </Window.Resources>  
        <Grid>  
            <Grid.ColumnDefinitions>  
                <ColumnDefinition Width="2*"/>  
                <ColumnDefinition Width="7*"/>  
                <ColumnDefinition Width="3*"/>  
            </Grid.ColumnDefinitions>  
            <Border Grid.Column="0">  
                <sapt:ToolboxControl Name="Toolbox">  
                    <sapt:ToolboxCategory CategoryName="Basic">  
                        <sapt:ToolboxItemWrapper AssemblyName="{StaticResource AssemblyName}" >  
                            <sapt:ToolboxItemWrapper.ToolName>  
                                System.Activities.Statements.Sequence  
                            </sapt:ToolboxItemWrapper.ToolName>  
                           </sapt:ToolboxItemWrapper>  
                        <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                            <sapt:ToolboxItemWrapper.ToolName>  
                                System.Activities.Statements.WriteLine  
                            </sapt:ToolboxItemWrapper.ToolName>  
  
                        </sapt:ToolboxItemWrapper>  
                        <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                            <sapt:ToolboxItemWrapper.ToolName>  
                                System.Activities.Statements.If  
                            </sapt:ToolboxItemWrapper.ToolName>  
  
                        </sapt:ToolboxItemWrapper>  
                        <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                            <sapt:ToolboxItemWrapper.ToolName>  
                                System.Activities.Statements.While  
                            </sapt:ToolboxItemWrapper.ToolName>  
  
                        </sapt:ToolboxItemWrapper>  
                    </sapt:ToolboxCategory>  
                </sapt:ToolboxControl>  
            </Border>  
            <Border Grid.Column="1" Name="DesignerBorder"/>  
            <Border Grid.Column="2" Name="PropertyBorder"/>  
        </Grid>  
    </Window>  
  
    ```  
  
13. Um einem Aktivitätsdesigner einen Aktivitätstyp zuzuordnen, müssen Sie den Aktivitätsdesigner im Metadatenspeicher registrieren.Fügen Sie hierzu der `RehostingWFDesigner`\-Klasse die `RegisterMetadata`\-Methode hinzu.Erstellen Sie innerhalb des Bereichs der `RegisterMetadata`\-Methode ein <xref:System.Activities.Presentation.Metadata.AttributeTableBuilder>\-Objekt, und rufen Sie die <xref:System.Activities.Presentation.Metadata.AttributeTableBuilder.AddCustomAttributes%2A>\-Methode auf, um dem Objekt die Attribute hinzuzufügen.Rufen Sie die <xref:System.Activities.Presentation.Metadata.MetadataStore.AddAttributeTable%2A>\-Methode auf, um dem Metadatenspeicher das <xref:System.Activities.Presentation.Metadata.AttributeTable>\-Objekt hinzuzufügen.Der folgende Code enthält die Rehosting\-Logik für den Designer.Damit werden die Metadaten registriert, die `SimpleNativeActivity` wird in die Toolbox eingefügt und der Workflow wird erstellt.Fügen Sie diesen Code in die Datei "RehostingWFDesigner.xaml.cs" ein.  
  
    ```  
  
    using System;  
    using System.Activities.Core.Presentation;  
    using System.Activities.Presentation;  
    using System.Activities.Presentation.Metadata;  
    using System.Activities.Presentation.Toolbox;  
    using System.Activities.Statements;  
    using System.ComponentModel;  
    using System.Windows;  
  
    namespace UsingWorkflowItemPresenter  
    {  
        // Interaction logic for RehostingWFDesigner.xaml  
        public partial class RehostingWFDesigner  
        {  
            public RehostingWFDesigner()  
            {  
                InitializeComponent();  
            }  
  
            protected override void OnInitialized(EventArgs e)  
            {  
                base.OnInitialized(e);  
                // register metadata  
                (new DesignerMetadata()).Register();  
                RegisterCustomMetadata();  
                // add custom activity to toolbox  
                Toolbox.Categories.Add(new ToolboxCategory("Custom activities"));  
                Toolbox.Categories[1].Add(new ToolboxItemWrapper(typeof(SimpleNativeActivity)));  
  
                // create the workflow designer  
                WorkflowDesigner wd = new WorkflowDesigner();  
                wd.Load(new Sequence());  
                DesignerBorder.Child = wd.View;  
                PropertyBorder.Child = wd.PropertyInspectorView;  
  
            }  
  
            void RegisterCustomMetadata()  
            {  
                AttributeTableBuilder builder = new AttributeTableBuilder();  
                builder.AddCustomAttributes(typeof(SimpleNativeActivity), new DesignerAttribute(typeof(SimpleNativeDesigner)));  
                MetadataStore.AddAttributeTable(builder.CreateTable());  
            }  
        }  
    }  
  
    ```  
  
14. Klicken Sie im Projektmappen\-Explorer mit der rechten Maustaste auf das Verzeichnis "References", und wählen Sie **Verweis hinzufügen…**, um das Dialogfeld **Verweis hinzufügen** zu öffnen.  
  
15. Klicken Sie auf die Registerkarte **.NET**, suchen Sie die Assembly mit dem Namen **System.Activities.Core.Presentation**, wählen Sie sie aus, und klicken Sie auf **OK**.  
  
16. Fügen Sie auf die gleiche Weise den folgenden Assemblys Verweise hinzu:  
  
    1.  System.Data.DataSetExtensions.dll  
  
    2.  System.Activities.Presentation.dll  
  
    3.  System.ServiceModel.Activities.dll  
  
17. Öffnen Sie die Datei "App.xaml", und ändern Sie den StartUpUri\-Wert in "RehostingWFDesigner.xaml".  
  
18. Klicken Sie im **Projektmappen\-Explorer** mit der rechten Maustaste auf das Projekt "UsingWorkflowItemPresenter", und wählen Sie **Hinzufügen** und dann **Neues Element…**, um das Dialogfeld **Neues Element hinzufügen** zu öffnen. Wählen Sie dann im Abschnitt **Installierte Vorlagen** auf der linken Seite die Kategorie **Workflow**.  
  
19. Wählen Sie die Vorlage **Aktivitätsdesigner** aus, weisen Sie ihr den Namen `SimpleNativeDesigner` zu, und klicken Sie auf **Hinzufügen**.  
  
20. Öffnen Sie die Datei "SimpleNativeDesigner.xaml", und fügen Sie den folgenden Code ein.Beachten Sie, dass in diesem Code <xref:System.Activities.Presentation.ActivityDesigner> als Stammelement verwendet wird. Er zeigt, wie <xref:System.Activities.Presentation.WorkflowItemPresenter> mithilfe von Bindung in Ihren Designer integriert wird, sodass im zusammengesetzten Aktivitätsdesigner ein untergeordneter Typ angezeigt werden kann.  
  
    > [!NOTE]
    >  Mit dem Schema für <xref:System.Activities.Presentation.ActivityDesigner> können Sie dem benutzerdefinierten Aktivitätsdesigner nur ein untergeordnetes Element hinzufügen. Bei diesem Element kann es sich jedoch um ein `StackPanel`, ein `Grid` oder um ein anderes zusammengesetztes Benutzeroberflächenelement handeln.  
  
    ```  
  
    <sap:ActivityDesigner x:Class=" UsingWorkflowItemPresenter.SimpleNativeDesigner"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:sap="clr-namespace:System.Activities.Presentation;assembly=System.Activities.Presentation"  
        xmlns:sapv="clr-namespace:System.Activities.Presentation.View;assembly=System.Activities.Presentation">  
        <sap:ActivityDesigner.Resources>  
            <DataTemplate x:Key="Collapsed">  
                <StackPanel>  
                    <TextBlock>This is the collapsed view</TextBlock>  
                </StackPanel>  
            </DataTemplate>  
            <DataTemplate x:Key="Expanded">  
                <StackPanel>  
                    <TextBlock>Custom Text</TextBlock>  
                    <sap:WorkflowItemPresenter Item="{Binding Path=ModelItem.Body, Mode=TwoWay}"  
                                            HintText="Please drop an activity here" />  
                </StackPanel>  
            </DataTemplate>  
            <Style x:Key="ExpandOrCollapsedStyle" TargetType="{x:Type ContentPresenter}">  
                <Setter Property="ContentTemplate" Value="{DynamicResource Collapsed}"/>  
                <Style.Triggers>  
                    <DataTrigger Binding="{Binding Path=ShowExpanded}" Value="true">  
                        <Setter Property="ContentTemplate" Value="{DynamicResource Expanded}"/>  
                    </DataTrigger>  
                </Style.Triggers>  
            </Style>  
        </sap:ActivityDesigner.Resources>  
        <Grid>  
            <ContentPresenter Style="{DynamicResource ExpandOrCollapsedStyle}" Content="{Binding}" />  
        </Grid>  
    </sap:ActivityDesigner>  
  
    ```  
  
21. Klicken Sie im **Projektmappen\-Explorer** mit der rechten Maustaste auf das Projekt "UsingWorkflowItemPresenter", und wählen Sie **Hinzufügen** und dann **Neues Element…**, um das Dialogfeld **Neues Element hinzufügen** zu öffnen. Wählen Sie dann im Abschnitt **Installierte Vorlagen** auf der linken Seite die Kategorie **Workflow**.  
  
22. Wählen Sie die Vorlage **Codeaktivität** aus, weisen Sie ihr den Namen `SimpleNativeActivity` zu, und klicken Sie auf **Hinzufügen**.  
  
23. Implementieren Sie die `SimpleNativeActivity`\-Klasse, indem Sie den folgenden Code in die Datei "SimpleNativeActivity.cs" einfügen.  
  
    ```  
  
    using System.Activities;  
  
    namespace UsingWorkflowItemPresenter  
    {  
        public sealed class SimpleNativeActivity : NativeActivity  
        {  
            // this property contains an activity that will be scheduled in the execute method  
    // the WorkflowItemPresenter in the designer is bound to this to enable editing  
    // of the value  
            public Activity Body { get; set; }  
  
            protected override void CacheMetadata(NativeActivityMetadata metadata)  
            {  
               metadata.AddChild(Body);  
               base.CacheMetadata(metadata);  
  
            }  
  
            protected override void Execute(NativeActivityContext context)  
            {  
                context.ScheduleActivity(Body);  
            }  
        }  
    }  
  
    ```  
  
24. Wählen Sie im Menü **Erstellen** die Option **Projektmappe erstellen** aus.  
  
25. Wählen Sie im Menü **Debuggen** die Option **Starten ohne Debugging** aus, um das neu gehostete benutzerdefinierte Entwurfsfenster zu öffnen.  
  
### So erstellen Sie einen benutzerdefinierten Aktivitätsdesigner mit WorkflowItemsPresenter  
  
1.  Die Prozedur für den zweiten benutzerdefinierten Aktivitätsdesigner ist bis auf wenige Änderungen identisch mit der ersten Prozedur. Die erste Änderung besteht darin, der zweiten Anwendung den Namen `UsingWorkflowItemsPresenter` zuzuweisen.Außerdem wird mit dieser Anwendung keine neue benutzerdefinierte Aktivität definiert.  
  
2.  Die Hauptunterschiede sind in den Dateien "CustomParallelDesigner.xaml" und "RehostingWFDesigner.xaml.cs" enthalten.Hier stammt der Code aus der Datei "CustomParallelDesigne.xaml" zur Definition der Benutzeroberfläche.  
  
    ```  
    <sap:ActivityDesigner x:Class=" UsingWorkflowItemsPresenter.CustomParallelDesigner"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:sap="clr-namespace:System.Activities.Presentation;assembly=System.Activities.Presentation"  
        xmlns:sapv="clr-namespace:System.Activities.Presentation.View;assembly=System.Activities.Presentation">  
        <sap:ActivityDesigner.Resources>  
            <DataTemplate x:Key="Collapsed">  
                <TextBlock>This is the Collapsed View</TextBlock>  
            </DataTemplate>  
            <DataTemplate x:Key="Expanded">  
                <StackPanel>  
                    <TextBlock HorizontalAlignment="Center">This is the</TextBlock>  
                    <TextBlock HorizontalAlignment="Center">extended view</TextBlock>  
                    <sap:WorkflowItemsPresenter HintText="Drop Activities Here"  
                                        Items="{Binding Path=ModelItem.Branches}">  
                        <sap:WorkflowItemsPresenter.SpacerTemplate>  
                            <DataTemplate>  
                                <Ellipse Width="10" Height="10" Fill="Black"/>  
                            </DataTemplate>  
                        </sap:WorkflowItemsPresenter.SpacerTemplate>  
                        <sap:WorkflowItemsPresenter.ItemsPanel>  
                            <ItemsPanelTemplate>  
                                <StackPanel Orientation="Horizontal"/>  
                            </ItemsPanelTemplate>  
                        </sap:WorkflowItemsPresenter.ItemsPanel>  
                    </sap:WorkflowItemsPresenter>  
                </StackPanel>  
            </DataTemplate>  
            <Style x:Key="ExpandOrCollapsedStyle" TargetType="{x:Type ContentPresenter}">  
                <Setter Property="ContentTemplate" Value="{DynamicResource Collapsed}"/>  
                <Style.Triggers>  
                    <DataTrigger Binding="{Binding Path=ShowExpanded}" Value="true">  
                        <Setter Property="ContentTemplate" Value="{DynamicResource Expanded}"/>  
                    </DataTrigger>  
                </Style.Triggers>  
            </Style>  
        </sap:ActivityDesigner.Resources>  
        <Grid>  
            <ContentPresenter Style="{DynamicResource ExpandOrCollapsedStyle}" Content="{Binding}"/>  
        </Grid>  
    </sap:ActivityDesigner>  
  
    ```  
  
3.  Hier stammt der Code aus der Datei "RehostingWFDesigner.xaml.cs" zur Bereitstellung der Rehosting\-Logik.  
  
    ```  
  
    using System;  
    using System.Activities.Core.Presentation;  
    using System.Activities.Presentation;  
    using System.Activities.Presentation.Metadata;  
    using System.Activities.Statements;  
    using System.ComponentModel;  
    using System.Windows;  
  
    namespaceUsingWorkflowItemsPresenter  
    {  
        public partial class RehostingWfDesigner : Window  
        {  
            public RehostingWfDesigner()  
            {  
                InitializeComponent();  
            }  
  
            protected override void OnInitialized(EventArgs e)  
            {  
                base.OnInitialized(e);  
                // register metadata  
                (new DesignerMetadata()).Register();  
                RegisterCustomMetadata();  
  
                // create the workflow designer  
                WorkflowDesigner wd = new WorkflowDesigner();  
                wd.Load(new Sequence());  
                DesignerBorder.Child = wd.View;  
                PropertyBorder.Child = wd.PropertyInspectorView;  
  
            }  
  
            void RegisterCustomMetadata()  
            {  
                AttributeTableBuilder builder = new AttributeTableBuilder();  
                builder.AddCustomAttributes(typeof(Parallel), new DesignerAttribute(typeof(CustomParallelDesigner)));  
                MetadataStore.AddAttributeTable(builder.CreateTable());  
            }  
        }  
    }  
    ```  
  
## Siehe auch  
 <xref:System.Activities.Presentation.ActivityDesigner>   
 <xref:System.Activities.Presentation.WorkflowItemPresenter>   
 <xref:System.Activities.Presentation.WorkflowItemsPresenter>   
 <xref:System.Activities.Presentation.WorkflowViewElement>   
 <xref:System.Activities.Presentation.Model.ModelItem>   
 [Anpassen des Workflowentwurfsvorgangs](../../../docs/framework/windows-workflow-foundation//customizing-the-workflow-design-experience.md)