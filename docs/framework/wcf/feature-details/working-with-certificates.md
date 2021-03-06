---
title: "Работа с сертификатами | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "сертификаты [WCF]"
ms.assetid: 6ffb8682-8f07-4a45-afbb-8d2487e9dbc3
caps.latest.revision: 26
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 26
---
# Работа с сертификатами
Для программирования безопасности [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] обычно используются цифровые сертификаты X.509, с помощью которых выполняется проверка подлинности клиентов и серверов, шифрование, а сообщения подписываются цифровой подписью.В этом разделе содержится краткое описание функций для работы с цифровыми сертификатами X.509 и порядка использования этих функций в [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Кроме того, этот раздел включает ссылки на другие разделы с более подробным объяснением основных понятий и порядка выполнения общих задач с использованием [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] и сертификатов.  
  
 Вкратце, цифровой сертификат является частью *ключевого индикатора производительности* \(PKI\), представляющей собой систему цифровых сертификатов, центров сертификации и других центров регистрации, которые используются для проверки подлинности каждой стороны, участвующей в электронной транзакции, посредством использования асимметричного шифрования.Сертификаты выдаются центрами сертификации. Каждый сертификат имеет набор полей, в которых содержатся такие данные, как *субъект* \(сущность, которой выдается сертификат\), срок действия \(период времени, в течение которого сертификат является действительным\), издатель \(лицо, выдавшее сертификат\) и открытый ключ.В [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] каждое из этих свойств обрабатывается как утверждение <xref:System.IdentityModel.Claims.Claim>, и каждое утверждение затем подразделяется на два типа: удостоверение и право.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] о сертификатах X.509 см. в разделе [Сертификаты с открытым ключом X.509](http://go.microsoft.com/fwlink/?LinkId=209952)[!INCLUDE[crabout](../../../../includes/crabout-md.md)] об утверждении и авторизации в WCF см. в разделе [Управление утверждениями и авторизацией с помощью модели удостоверения](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] о реализации ключевого индикатора производительности см. в разделе [Windows Server 2008 R2 — службы сертификатов](http://go.microsoft.com/fwlink/?LinkId=209949).  
  
 Основной функцией сертификата является удостоверение подлинности владельца сертификата для других сторон.В сертификате содержится *открытый ключ* владельца, в то время как закрытый ключ хранится у владельца.Открытый ключ можно использовать для зашифровывания сообщений, передаваемых владельцу сертификата.Доступ к закрытому ключу имеет только владелец сертификата, поэтому только он может расшифровать эти сообщения.  
  
 Сертификаты должны выдаваться центром сертификации, который обычно является сторонним издателем сертификатов.Центр сертификации входит в состав домена Windows, чтобы можно было использовать его для выдачи сертификатов компьютерам домена.  
  
## Просмотр сертификатов  
 При работе с сертификатами зачастую необходимо просматривать их и проверять определенные свойства.Это легко выполняется с помощью консоли управления \(MMC\).[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Как просматривать сертификаты с помощью оснастки консоли MMC](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md).  
  
## Хранилища сертификатов  
 Сертификаты хранятся в хранилищах.Существует два основных хранилища, которые подразделяются на вложенные хранилища.Администратор компьютера может просматривать оба основных хранилища с помощью средства MMC.Пользователи, не являющиеся администраторами, могут просматривать только хранилище текущего пользователя.  
  
-   **Хранилище локального компьютера**.Содержит сертификаты, доступ к которым осуществляется выполняющимися на компьютере процессами, такими как [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].Это расположение используется для хранения сертификатов, удостоверяющих подлинность сервера для клиентов.  
  
-   **Хранилище текущего пользователя**.Интерактивные приложения обычно помещают сертификаты в это хранилище для текущего пользователя компьютера.В случае клиентского приложения в это хранилище обычно помещаются сертификаты, используемые для проверки подлинности пользователя при подключении к службе.  
  
 Эти два хранилища подразделяются на вложенные хранилища.Ниже представлены наиболее важные вложенные хранилища, используемые при программировании с [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
-   **Доверенные корневые центры сертификации**.Сертификаты в этом хранилище могут быть использованы для создания цепочки сертификатов, которая может вести обратно к центру сертификации в этом хранилище.  
  
    > [!IMPORTANT]
    >  Локальный компьютер неявно доверяет любому сертификату, помещенному в это хранилище, даже если он поступил не из доверенного стороннего центра сертификации.Поэтому в данное хранилище не следует помещать сертификаты, к издателям которых нет полного доверия, или если последствия не до конца ясны.  
  
-   **Личное**Это хранилище используется для хранения сертификатов, связанных с пользователем компьютера.Обычно в этом хранилище хранятся сертификаты, выданные одним из центров сертификации, сертификаты которых находятся в хранилище «Доверенные корневые центры сертификации».С другой стороны, сертификат, находящийся в этом хранилище, может быть самостоятельно выданным, и ему будет доверять приложение.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] хранилищах сертификатов см. в разделе [Хранилища сертификатов](http://go.microsoft.com/fwlink/?LinkId=88912).  
  
### Выбор хранилища  
 Выбор расположения для хранения сертификата зависит от режима и места выполнения клиента или службы.Действуют следующие общие правила.  
  
-   Если служба WCF в службе Windows, используйте хранилище **локального компьютера**.Обратите внимание, что для установки сертификатов в хранилище локального компьютера требуются привилегии администратора.  
  
-   Если служба или клиент является приложением, выполняющимся от имени учетной записи пользователя, используйте хранилище **текущего пользователя**.  
  
### Доступ к хранилищам  
 Хранилища защищаются с помощью списков управления доступом \(ACL\) аналогично папкам на компьютере.При создании службы, размещаемой в IIS, процесс [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] выполняется от имени учетной записи [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].Эта учетная запись должна иметь доступ к хранилищу, в котором содержатся используемые службой сертификаты.Каждое основное хранилище защищается с помощью списка управления доступом по умолчанию, однако списки можно изменять.При создании отдельной роли для доступа к хранилищу необходимо предоставить ей разрешение на доступ.О том, как изменить список доступа с помощью программы WinHttpCertConfig.exe, см. в разделе [Практическое руководство. Создание временных сертификатов для использования во время разработки](../../../../docs/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development.md).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] использовании сертификатов клиента в службах IIS см. в разделе [Как вызвать веб\-службу с использованием клиентского сертификата для аутентификации в веб\-приложении ASP.NET](http://go.microsoft.com/fwlink/?LinkId=88914).  
  
## Цепочка доверия и центры сертификации  
 Сертификаты создаются в иерархии, где каждый отдельный сертификат связан с выдавшим его органом сертификации.Эта ссылка указывает на сертификат органа сертификации.Далее сертификат органа сертификации связан с органом сертификации, выдавшим исходный сертификат.Процесс повторяется до тех пор, пока не будет достигнут корневой сертификат органа сертификации.Сертификат корневого органа сертификации является изначально доверенным.  
  
 Цифровые сертификаты используются для удостоверения подлинности сущности на основе этой иерархии, которая также называется *цепочкой сертификатов*.Цепочку любого сертификата вы можете просмотреть с помощью оснастки MMC, дважды щелкнув сертификат и выбрав вкладку **Путь сертификата**.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] об импорте цепочек сертификатов для центра сертификации см. в разделе [Как указать цепочку сертификатов центра сертификации, используемую для проверки сигнатур](../../../../docs/framework/wcf/feature-details/specify-the-certificate-authority-chain-verify-signatures-wcf.md).  
  
> [!NOTE]
>  Любой издатель может быть сделан доверенным корневым центром; для этого необходимо поместить сертификат издателя в хранилище сертификатов доверенных корневых центров.  
  
### Отключение механизма проверки цепочки доверия  
 При создании новой службы пользователь может использовать сертификат, который был выдан центром сертификации, отличным от доверенного, или сертификат издателя может отсутствовать в хранилище «Доверенные корневые центры сертификации».Предусмотрена возможность временного отключения механизма, проверяющего цепочку сертификатов для заданного сертификата; эта возможность должна использоваться только в процессе разработки.Чтобы отключить данный механизм, задайте для свойства `CertificateValidationMode` значение `PeerTrust` или `PeerOrChainTrust`.Эти режимы определяют, что сертификат может быть либо самостоятельно выданным \(доверие одноранговой группы\), либо являться частью цепочки доверия.Указанное свойство можно задать для любого из следующих классов.  
  
|Класс|Свойство|  
|-----------|--------------|  
|<xref:System.ServiceModel.Security.X509ClientCertificateAuthentication>|<xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.CertificateValidationMode%2A?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>|<xref:System.ServiceModel.Security.X509PeerCertificateAuthentication.CertificateValidationMode%2A?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication>|<xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.IssuedTokenServiceCredential>|<xref:System.ServiceModel.Security.IssuedTokenServiceCredential.CertificateValidationMode%2A?displayProperty=fullName>|  
  
 Свойство также вы можете задать с использованием конфигурации.Для задания режима проверки используются следующие элементы.  
  
-   [\<аутентификация\>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md)  
  
-   [\<peerAuthentication\>](../../../../docs/framework/configure-apps/file-schema/wcf/peerauthentication-element.md)  
  
-   [\<messageSenderAuthentication\>](../../../../docs/framework/configure-apps/file-schema/wcf/messagesenderauthentication-element.md)  
  
## Пользовательская проверка подлинности  
 Свойство `CertificateValidationMode` также позволяет настроить способ проверки сертификатов.По умолчанию задано значение `ChainTrust`.Чтобы использовать значение <xref:System.ServiceModel.Security.X509CertificateValidationMode>, необходимо также установить атрибут `CustomCertificateValidatorType` для сборки и типа, которые используются при проверке сертификата.Для создания пользовательского проверяющего элемента управления необходимо наследование от абстрактного класса <xref:System.IdentityModel.Selectors.X509CertificateValidator>.  
  
 При создании пользовательской структуры проверки подлинности наиболее важным методом, который необходимо переопределить, является метод <xref:System.IdentityModel.Selectors.X509CertificateValidator.Validate%2A>.Образец создания пользовательской структуры проверки подлинности см. в разделе [Проверяющий элемент управления для сертификатов X.509](../../../../docs/framework/wcf/samples/x-509-certificate-validator.md).[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Пользовательские учетные данные и проверка учетных данных](../../../../docs/framework/wcf/extending/custom-credential-and-credential-validation.md).  
  
## Использование программы Makecert.exe для создания цепочки сертификатов  
 Средство создания сертификатов \(Makecert.exe\) позволяет создавать сертификаты X.509, а также пары открытого и закрытого ключей.Закрытый ключ можно сохранить на диск, а затем использовать его для выдачи и подписи новых сертификатов, что позволяет имитировать иерархию цепочки сертификатов.Данное средство предназначено для использования только в качестве вспомогательного инструмента при разработке служб; его не следует использовать с целью создания сертификатов для фактического развертывания.При разработке службы [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], используйте следующую процедуру для создания цепочки доверия с помощью программы Makecert.exe.  
  
#### Создание цепочки доверия с помощью программы Makecert.exe  
  
1.  Создайте временный сертификат корневого центра \(самозаверяющий\) с помощью программы MakeCert.exe.Сохраните закрытый ключ на диск.  
  
2.  Воспользуйтесь новым сертификатом для выдачи другого сертификата, содержащего открытый ключ.  
  
3.  Импортируйте сертификат корневого центра в хранилище «Доверенные корневые центры сертификации».  
  
4.  Пошаговые инструкции см. в разделе [Практическое руководство. Создание временных сертификатов для использования во время разработки](../../../../docs/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development.md).  
  
## Выбор сертификата для использования  
 Наиболее распространенными вопросами о сертификатах являются следующие: какой сертификат использовать и почему?Ответ зависит от того, что программирует пользователь — клиент или службу.Ниже представлены общие рекомендации; следует иметь виду, что они не являются исчерпывающими ответами на поставленные вопросы.  
  
### Сертификаты служб  
 Основной задачей сертификатов служб является удостоверение подлинности сервера для клиентов.При проверке подлинности сервера клиентом одной из исходных проверок является сравнение значения поля **Субъект** с универсальным кодом ресурса \(URI\), используемым для обращения к службе: DNS\-имена должны совпадать.Например, если универсальным кодом ресурса службы является «http:\/\/www.contoso.com\/endpoint\/», в поле **Субъект** должно также содержаться значение «www.contoso.com».  
  
 Обратите внимание, что в этом поле может содержаться несколько значений с отдельными префиксами.Чаще всего префикс "CN" используется для указания общего имени, например, "CN \= www.contoso.com".Кроме того, поле **Субъект** может быть пустым; в этом случае в поле **Альтернативное имя субъекта** может содержаться значение поля **DNS\-имя**.  
  
 Также обратите внимание, что поле **Назначения** сертификата должно включать соответствующее значение, например «Проверка подлинности сервера» или «Проверка подлинности клиента».  
  
### Сертификаты клиентов  
 Сертификаты клиента обычно не выдаются сторонним центром сертификации.В хранилище «Личное» текущего пользователя обычно содержатся сертификаты, выданные корневым центром; в поле «Назначения» этих сертификатов задано значение «Аутентификация клиента».Клиент может использовать такой сертификат, когда требуется взаимная проверка подлинности.  
  
## Проверка отзыва сертификатов в режиме подключения к сети и автономном режиме  
  
### Срок действия сертификата  
 Каждый сертификат действителен только в течение заданного периода времени, который называется *сроком действия*.Срок действия определяется значениями полей **Действителен с** и **Действителен по** сертификата X.509.Во время проверки подлинности проверяется, не истек ли срок действия сертификата.  
  
### Список отзыва сертификатов  
 Центр сертификации может отменить действующий сертификат в любое время.Это может произойти по многим причинам, например при компрометации закрытого ключа сертификата.  
  
 В этом случае все цепочки, происходящие от отозванного сертификата, также становятся недействительными и механизмы проверки подлинности перестают им доверять.Для обозначения отозванных сертификатов каждый издатель публикует *список отзыва сертификатов*, имеющий отметку даты и времени.Этот список можно проверить с помощью режима с подключением к сети или автономного режима, задав одно из значений перечисления <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> для свойства `RevocationMode` или `DefaultRevocationMode` следующих классов: <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication>, <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>, <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication> и <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>.Значение по умолчанию для всех свойств — `Online`.  
  
 Режим можно также задать в конфигурации с помощью атрибута `revocationMode` элементов [\<authentication\>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md)[\<serviceBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md)[\<authentication\>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md)[\<endpointBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md)\) и \(\).  
  
## Метод SetCertificate  
 В [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] часто требуется задать сертификат или набор сертификатов, который служба или клиент будет использовать для проверки подлинности, шифрования или подписи сообщения.Это можно сделать программно с помощью метода `SetCertificate` различных классов, представляющих сертификаты X.509.Следующие классы используют метод `SetCertificate` для задания сертификата.  
  
|Класс|Метод|  
|-----------|-----------|  
|<xref:System.ServiceModel.Security.PeerCredential>|<xref:System.ServiceModel.Security.PeerCredential.SetCertificate%2A>|  
|<xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>|<xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A>|  
|<xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential>|<xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A>|  
|<xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential>|  
|<xref:System.ServiceModel.Security.X509CertificateInitiatorServiceCredential.SetCertificate%2A>|  
  
 Метод `SetCertificate` позволяет задать хранилище и его расположение, тип поиска \(параметр `x509FindType`\), определяющий поле сертификата, и значение, которое требуется найти в данном поле.Например, следующий код создает экземпляр <xref:System.ServiceModel.ServiceHost> и задает сертификат службы, используемый с целью удостоверения подлинности службы для клиентов, с помощью метода `SetCertificate` .  
  
 [!code-csharp[c_WorkingWithCertificates#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_workingwithcertificates/cs/source.cs#1)]
 [!code-vb[c_WorkingWithCertificates#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_workingwithcertificates/vb/source.vb#1)]  
  
### Несколько сертификатов с одинаковыми значениями полей  
 В хранилище может содержаться несколько сертификатов с одним и тем же именем субъекта.Поэтому если для параметра `x509FindType` задано значение <xref:System.Security.Cryptography.X509Certificates.X509FindType> или <xref:System.Security.Cryptography.X509Certificates.X509FindType>, и существует несколько сертификатов с таким значением, возникает исключение, поскольку в этом случаеневозможноопределить,какой именно сертификат требуется использовать.Это можно подавить, задав для параметра `x509FindType` значение <xref:System.Security.Cryptography.X509Certificates.X509FindType>.В поле отпечатка содержится уникальное значение, которое можно использовать для поиска конкретного сертификата в хранилище.Однако у данного подхода есть свой недостаток: если сертификат был отозван или обновлен, метод `SetCertificate` выполнить не удастся, поскольку исходный отпечаток на будет найден.А если сертификат является недействительным, проверка подлинности не будет пройдена.Это можно подавить, задав для параметра `x590FindType` значение <xref:System.Security.Cryptography.X509Certificates.X509FindType> и указав имя издателя.Если указывать издателя не требуется, можно также задать одно из значений перечисления <xref:System.Security.Cryptography.X509Certificates.X509FindType>, например <xref:System.Security.Cryptography.X509Certificates.X509FindType>.  
  
## Сертификаты в конфигурации  
 Сертификаты также можно задать с использованием конфигурации.В случае создания службы учетные данные, включая сертификаты, указываются в разделе [\<serviceBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md).В случае программирования клиента сертификаты указываются в разделе [\<endpointBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md).  
  
## Сопоставление сертификата с учетной записью пользователя  
 Службы IIS и Active Directory предусматривают возможность сопоставления сертификата с учетной пользовательской записью Windows.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] об этой возможности см. в разделе [Сопоставление сертификатов с учетными записями пользователей](http://go.microsoft.com/fwlink/?LinkId=88917).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] сопоставлении Active Directory см. в разделе [Сопоставление сертификатов клиентов с помощью функции сопоставления службы каталогов](http://go.microsoft.com/fwlink/?LinkId=88918).  
  
 Если эта функция включена, можно задать для свойства <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.MapClientCertificateToWindowsAccount%2A> класса <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> значение `true`.В конфигурации можно задать для атрибута `mapClientCertificateToWindowsAccount` элемента [\<аутентификация\>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md)`true значение` , как показано в следующем примере кода.  
  
```  
<serviceBehaviors>  
 <behavior name="MappingBehavior">  
  <serviceCredentials>  
   <clientCertificate>  
    <authentication certificateValidationMode="None" mapClientCertificateToWindowsAccount="true" />  
   </clientCertificate>  
  </serviceCredentials>  
 </behavior>  
</serviceBehaviors>  
```  
  
 Сопоставление сертификата X.509 с маркером, представляющим учетную запись пользователя Windows, считается повышением привилегий, поскольку после сопоставления маркер Windows может использоваться для получения доступа к защищенным ресурсам.Поэтому перед сопоставлением необходимо проверить, что сертификат X.509 соответствует политике домена.Проверку этого требования обеспечивает пакет безопасности *SChannel* .  
  
 При использовании [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] или более поздней версии [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] позволяет убедиться, что сертификат соответствует политике домена перед его сопоставлением с учетной записью Windows.  
  
 В первом выпуске [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] сопоставление выполняется без обращения к политике домена.Поэтому более старые приложения, которые работали при использовании первого выпуска, могут не работать, если включено сопоставление и сертификат X.509 не удовлетворяет требованиям политики домена.  
  
## См. также  
 <xref:System.ServiceModel.Channels>   
 <xref:System.ServiceModel.Security>   
 <xref:System.ServiceModel>   
 <xref:System.Security.Cryptography.X509Certificates.X509FindType>   
 [Защита служб и клиентов](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)