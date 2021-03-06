---
title: "&lt;claimTypeRequirements&gt; von &lt;message&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f95c5ecd-abb6-4b77-a6d7-a38727f4a142
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;claimTypeRequirements&gt; von &lt;message&gt;
Gibt eine Auflistung von erforderlichen Anspruchstypen an.  
  
 Die Auflistung wird vom Dienst verwendet, um erforderliche und optionale Ansprüche anzugeben, die sich in dem vom Client für den Dienstzugriff verwendeten ausgestellten Token befinden müssen.  Der Dienst macht die erforderlichen Anspruchstypen in Metadaten verfügbar, wenn die WSDL\-Veröffentlichung aktiviert wurde, aber WCF erfordert nicht, dass das ausgestellte Token die angegebenen Anspruchstypen enthält.  Dienste, die versuchen, erforderliche Anspruchstypen durchzusetzen, sollten mit Autorisierungsrichtlinien verwendet werden.  
  
 Bei verbundenen Clients enthält diese Auflistung die Liste erforderlicher und optionaler Ansprüche, die an den Sicherheitstokendienst in der Clientanforderung für einen ausgestellten Token gesendet wird.  
  
## Siehe auch  
 <xref:System.ServiceModel.FederatedMessageSecurityOverHttp.ClaimTypeRequirements%2A>   
 <xref:System.ServiceModel.Security.Tokens.ClaimTypeRequirement>   
 <xref:System.ServiceModel.Configuration.FederatedMessageSecurityOverHttpElement.ClaimTypeRequirements%2A>   
 <xref:System.ServiceModel.Configuration.ClaimTypeElementCollection>   
 <xref:System.ServiceModel.Configuration.ClaimTypeElement>