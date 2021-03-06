---
title: "&lt;message&gt; von &lt;wsDualHttpBinding&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 75101744-eed8-4d61-91f4-5fc4473a21f2
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# &lt;message&gt; von &lt;wsDualHttpBinding&gt;
Definiert die Sicherheitseinstellungen für [\<wsDualHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md) auf Nachrichtenebene.  
  
## Syntax  
  
```  
  
<message   
      clientCredentialType="None/Windows/UserName/Certificate/CardSpace"  
     negotiateServiceCredential="Boolean"  
   algorithmSuite="Basic128/Basic192/Basic256/Basic128Rsa15/Basic256Rsa15/TripleDes/TripleDesRsa15/Basic128Sha256/Basic192Sha256/TripleDesSha256/Basic128Sha256Rsa15/Basic192Sha256Rsa15/Basic256Sha256Rsa15/TripleDesSha256Rsa15"/>  
</message>  
```  
  
## Typ  
 <xref:System.ServiceModel.MessageSecurityOverHttp>  
  
## Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute, untergeordnete Elemente sowie übergeordnete Elemente beschrieben.  
  
### Attribute  
  
|Attribut|Beschreibung|  
|--------------|------------------|  
|algorithmSuite|Dies ist optional.  Legt die Nachrichtenverschlüsselungs\- und Key Wrap\-Algorithmen fest.  Die Algorithmen und die Schlüsselgröße werden durch die <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>\-Klasse ermittelt.  Diese Algorithmen entsprechen den in der Security Policy Language \(WS\-SecurityPolicy\)\-Spezifikation angegebenen Algorithmen.<br /><br /> Unten sind mögliche Werte aufgeführt.  Der Standardwert ist `Basic256`.|  
|clientCredentialType|Dies ist optional.  Gibt den Typ der Anmeldeinformationen an, die bei der Clientauthentifizierung im Sicherheitsmodus über `Message` verwendet werden.  Unten sind mögliche Werte aufgeführt.  Die Standardeinstellung ist `Windows`.<br /><br /> Dieses Attribut ist vom Typ <xref:System.ServiceModel.MessageCredentialType>.|  
|negotiateServiceCredential|Dies ist optional.  Ein boolescher Wert, der angibt, ob die Dienstanmeldeinformationen auf dem Client out\-of\-band bereitgestellt oder vom Dienst für den Client über einen Aushandlungsvorgang abgerufen werden.  Eine solche Verhandlung ist Vorläufer zum üblichen Nachrichtenaustausch.<br /><br /> Wenn das `clientCredentialType`\-Attribut None, Username oder Certificate lautet, wird durch Festlegen dieses Attributs auf `false` angegeben, dass das Dienstzertifikat auf dem Client out\-of\-band verfügbar ist und der Client das Dienstzertifikat \(unter Verwendung von [\<serviceCertificate\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)\) im [\<serviceCredentials\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)\-Dienstverhalten angeben muss.  Dieser Modus ist mit SOAP\-Stapeln interoperabel, die WS\-Trust und WS\-SecureConversation implementieren.<br /><br /> Wenn das `ClientCredentialType`\-Attribut `Windows` lautet, wird durch Festlegen dieses Attributs auf `false` die Kerberos\-basierte Authentifizierung angegeben.  Dies bedeutet, dass Client und Dienst Teil der gleichen Kerberos\-Domäne sein müssen.  Dieser Modus ist mit SOAP\-Stapeln interoperabel, die das Kerberos\-Tokenprofil \(gemäß der Definition in OASIS WSS TC\) sowie WS\-Trust und WS\-SecureConversation implementieren.  Wenn dieses Attribut `true` lautet, wird eine .NET SOAP\-Aushandlung verursacht, die den SPNego\-Austausch über SOAP\-Nachrichten tunnelt.<br /><br /> Die Standardeinstellung ist `true`.|  
  
## algorithmSuite\-Attribut  
  
|Wert|Beschreibung|  
|----------|------------------|  
|Basic128|Verwendet Aes128\-Verschlüsselung, Sha1 für den Nachrichtenhash und Rsa\-oaep\-mgf1p für Key Wrap.|  
|Basic192|Verwendet Aes192\-Verschlüsselung, Sha1 für den Nachrichtenhash und Rsa\-oaep\-mgf1p für Key Wrap.|  
|Basic256|Verwendet Aes256\-Verschlüsselung, Sha1 für den Nachrichtenhash und Rsa\-oaep\-mgf1p für Key Wrap.|  
|Basic256Rsa15|Verwendet Aes256\-Nachrichtenverschlüsselung, Sha1 für den Nachrichtenhash und Rsa15 für Key Wrap.|  
|Basic192Rsa15|Verwendet Aes192 für die Nachrichtenverschlüsselung, Sha1 für den Nachrichtenhash und Rsa15 für Key Wrap.|  
|TripleDes|Verwendet TripleDes\-Verschlüsselung, Sha1 für den Nachrichtenhash und Rsa\-oaep\-mgf1p für Key Wrap.|  
|Basic128Rsa15|Verwendet Aes128 für die Nachrichtenverschlüsselung, Sha1 für den Nachrichtenhash und Rsa15 für Key Wrap.|  
|TripleDesRsa15|Verwendet TripleDes\-Verschlüsselung, Sha1 für den Nachrichtenhash und Rsa15 für Key Wrap.|  
|Basic128Sha256|Verwendet Aes256\-Nachrichtenverschlüsselung, Sha256 für den Nachrichtenhash und Rsa\-oaep\-mgf1p für Key Wrap.|  
|Basic192Sha256|Verwendet Aes192 für die Nachrichtenverschlüsselung, Sha256 für den Nachrichtenhash und Rsa\-oaep\-mgf1p für Key Wrap.|  
|Basic256Sha256|Verwendet Aes256\-Nachrichtenverschlüsselung, Sha256 für den Nachrichtenhash und Rsa\-oaep\-mgf1p für Key Wrap.|  
|TripleDesSha256|Verwendet TripleDes für die Nachrichtenverschlüsselung, Sha256 für den Nachrichtenhash und Rsa\-oaep\-mgf1p für Key Wrap.|  
|Basic128Sha256Rsa15|Verwendet Aes128 für die Nachrichtenverschlüsselung, Sha256 für den Nachrichtenhash und Rsa15 für Key Wrap.|  
|Basic192Sha256Rsa15|Verwendet Aes192 für die Nachrichtenverschlüsselung, Sha256 für den Nachrichtenhash und Rsa15 für Key Wrap.|  
|Basic256Sha256Rsa15|Verwendet Aes256 für die Nachrichtenverschlüsselung, Sha256 für den Nachrichtenhash und Rsa15 für Key Wrap.|  
|TripleDesSha256Rsa15|Verwendet TripleDes für die Nachrichtenverschlüsselung, Sha256 für den Nachrichtenhash und Rsa15 für Key Wrap.|  
  
## clientCredentialType\-Attribut  
  
|Wert|Beschreibung|  
|----------|------------------|  
|Keine|Dies ermöglicht dem Dienst, mit anonymen Clients zu interagieren.  Auf Dienstseite wird dadurch angegeben, dass der Dienst keine Clientanmeldeinformationen erfordert.  Auf Clientseite wird dadurch angegeben, dass der Client keine Clientanmeldeinformationen bereitstellt.|  
|Windows|Dies ermöglicht SOAP\-Austausch im Rahmen des authentifizierten Kontexts von Windows\-Anmeldeinformationen.  Wenn das `negotiateServiceCredential`\-Attribut auf `true` festgelegt ist, wird entweder eine SSPI\-Verhandlung oder Kerberos \(ein interoperabler Standard\) ausgeführt.|  
|UserName|Ermöglicht es dem Dienst, vom Client zu fordern, sich über eine UserName\-Anmeldeinformation zu authentifizieren.  [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] unterstützt kein Kennwortdigest und keine ableitenden Schlüssel mit Kennwörtern sowie keine Verwendung solcher Schlüssel für die Nachrichtensicherheit.  [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] setzt prinzipiell durch, dass der Transport geschützt wird, wenn der Identitätsnachweis über UserName erfolgt.  Dieser Modus führt entweder zu einem interoperablen Austausch oder zu einer nicht interoperablen Aushandlung basierend auf dem `negotiateServiceCredential`\-Attribut.|  
|Zertifikat|Ermöglicht dem Dienst, die Forderung zu stellen, dass der Client über ein Zertifikat authentifiziert werden muss.  Wenn der Nachrichtensicherheitsmodus verwendet wird und das `negotiateServiceCredential`\-Attribut auf `false` gesetzt ist, muss dem Client das Dienstzertifikat zur Verfügung gestellt werden.|  
|IssuedToken|Gibt ein benutzerdefiniertes Token an, das in der Regel von einem Sicherheitstokendienst ausgegeben wird.|  
  
### Untergeordnete Elemente  
 Keine  
  
### Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|------------------|  
|[\<Sicherheit\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wsdualhttpbinding.md)|Definiert die Sicherheitsfunktionen für [\<wsDualHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md).|  
  
## Siehe auch  
 <xref:System.ServiceModel.Configuration.WSDualHttpSecurityElement.Message%2A>   
 <xref:System.ServiceModel.WSDualHttpSecurity.Message%2A>   
 <xref:System.ServiceModel.Configuration.MessageSecurityOverTcpElement>   
 <xref:System.ServiceModel.MessageSecurityOverHttp>   
 [Sichern von Diensten und Clients](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [Bindungen](../../../../../docs/framework/wcf/bindings.md)   
 [Konfigurieren der vom System bereitgestellten Bindungen](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/de-de/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<Bindung\>](../../../../../docs/framework/misc/binding.md)