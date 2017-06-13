---
title: "Mage.exe (средство создания и редактирования манифеста) | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Manifest Generation and Editing tool
- Mage.exe
ms.assetid: 77dfe576-2962-407e-af13-82255df725a1
caps.latest.revision: 68
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: a32f50ce8a92fa22d9627a1510a4b3ec1087364e
ms.openlocfilehash: caa06be840f0612e94742e7ea167f02b8b8d657d
ms.contentlocale: ru-ru
ms.lasthandoff: 06/02/2017

---
# <a name="mageexe-manifest-generation-and-editing-tool"></a>Mage.exe (средство создания и редактирования манифеста)
Инструмент создания и изменения манифеста (Mage.exe) — это программа командной строки, обеспечивающая создание и изменение манифестов приложений и развертываний. Являясь программой командной строки, инструмент Mage.exe может выполняться как в пакетных скриптах, так и в других Windows-приложениях, включая приложения [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] .  
  
 Вместо программы Mage.exe можно также использовать графическое приложение MageUI.exe. Для получения дополнительной информации см. [MageUI.exe (Manifest Generation and Editing Tool, Graphical Client)](../../../docs/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client.md).  
  
 Это средство автоматически устанавливается с Visual Studio. Чтобы применить этот инструмент, воспользуйтесь командной строкой разработчика (или командной строкой Visual Studio в Windows 7). Дополнительные сведения см. в разделе [Командные строки](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 В пакет установки [!INCLUDE[vs_dev10_long](../../../includes/vs-dev10-long-md.md)] включены две версии программ Mage.exe и MageUI.exe. Чтобы просмотреть сведения о версии, запустите программу MageUI.exe, откройте меню **Справка**и выберите пункт **О программе**. В данной документации представлено описание программ Mage.exe и MageUI.exe версии 4.0.x.x.  
  
 В командной строке введите следующее.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
Mage [commands] [commandOptions]  
```  
  
#### <a name="parameters"></a>Параметры  
 В следующей таблице показаны команды, поддерживаемые программой Mage.exe. Дополнительные сведения о параметрах этих команд см. в разделах [Параметры команд "New" и "Update"](#NewUpdate) и [Параметры команды "Sign"](#Sign).  
  
|Команда|Описание|  
|-------------|-----------------|  
|**-cc, ClearApplicationCache**|Очищает кэш загруженных интерактивных приложений.|  
|**-n, -New** *fileType [newOptions]*|Создает новый файл заданного типа. Допустимыми являются следующие типы:<br /><br /> -   `Deployment`— создает новый манифест развертывания.<br />-   `Application`— создает новый манифест приложения.<br /><br /> Если для этой команды не заданы никакие дополнительные параметры, она создаст файл соответствующего типа, с соответствующими тегами по умолчанию и значениями атрибутов.<br /><br /> Чтобы задать имя и путь для нового файла, используется параметр **-ToFile** (см. в следующей таблице).<br /><br /> Чтобы создать манифест приложения со всеми сборками приложения, добавленными в раздел \<dependency> манифеста, используется параметр **-FromDirectory** (см. в следующей таблице).|  
|**-u, -Update** *[filePath] [updateOptions]*|Вносит одно или несколько изменений в файл манифеста. Задавать тип редактируемого файла не требуется. Программа Mage.exe проверит файл, используя набор эвристик, и определит, является ли он манифестом развертывания или манифестом приложения.<br /><br /> Если файл уже подписан с помощью сертификата, при использовании параметра **-Update** блок подписи ключа будет удален. Это обусловлено тем, что подпись ключа содержит хэш файла и изменение файла делает хэш недействительным.<br /><br /> Чтобы задать имя и путь нового файла вместо перезаписи существующего файла, используется параметр **-ToFile** (см. в следующей таблице).|  
|**-s, -Sign** `[signOptions]`|Использует для подписывания файла пару ключей или сертификат X509. Подписи вставляются в файлы в виде XML-элементов.<br /><br /> При подписывании манифеста, задающего значение **-TimestampUri** , необходимо подключение к Интернету.|  
|**-h, -?, -Help** *[verbose]*|Описывает все доступные команды и их параметры. Задайте параметр `verbose` , чтобы получить подробные справочные сведения.|  
  
<a name="NewUpdate"></a>   
## <a name="new-and-update-command-options"></a>Параметры команд "New" и "Update"  
 В следующей таблице приведены параметры команд `-New` и `-Update` .  
  
|Параметры|Значение по умолчанию|Применение|Описание|  
|-------------|-------------------|----------------|-----------------|  
|**-a, -Algorithm**|sha1RSA|Манифесты приложений.<br /><br /> Манифесты развертывания.|Определяет алгоритм создания дайджестов зависимостей. Допустимые значения: "sha256RSA" или "sha1RSA".<br /><br /> Используется вместе с параметром "-Update". При использовании параметра "-Sign" этот параметр не учитывается|  
|**-appc, -AppCodeBase** `manifestReference`||Манифесты развертывания.|Вставляет в файл манифеста приложения ссылку на URL-адрес или путь к файлу. Этим значением должен быть полный путь к манифесту приложения.|  
|**-appm, -AppManifest** `manifestPath`||Манифесты развертывания.|Вставляет ссылку на манифест приложения в соответствующий манифест развертывания.<br /><br /> Файл, указанный в `manifestPath` , должен существовать, в противном случае программа Mage.exe выдаст ошибку. Если файл, указанный в `manifestPath` , не является манифестом приложения, программа Mage.exe выдаст ошибку.|  
|**-cf, -CertFile** `filePath`||Все типы файлов.|Задает местонахождение цифрового сертификата X509 для подписания манифеста. Этот параметр может использоваться в сочетании с параметром **-Password** , если для сертификата требуется пароль.|  
|**-ch, -CertHash** `hashSignature`||Все типы файлов.|Хэш цифрового сертификата, хранящегося в хранилище личных сертификатов на клиентском компьютере. Соответствует строке отпечатка цифрового сертификата, отображаемого в консоли сертификатов Windows.<br /><br /> Параметр`hashSignature` может быть задан или в верхнем, или в нижнем регистре, и может предоставляться либо как единая строка, либо в виде всех октетов отпечатка, разделенных пробелами, и всего отпечатка, заключенного в кавычки.|  
|**-fd, -FromDirectory** `directoryPath`||Манифесты приложений.|Заполняет манифест приложения описаниями всех сборок и файлов, найденных в каталоге `directoryPath`и всех его подкаталогах, где `directoryPath` — это каталог, содержащий развертываемое приложение. Для каждого файла в этом каталоге программа Mage.exe определяет, является ли такой файл сборкой или статическим файлом. Если файл является сборкой, программа добавляет в приложение тег `<dependency>` и атрибут `installFrom` , указав имя, базу кода и версию сборки. Если это статический файл, программа добавляет тег `<file>` . Программа Mage.exe также будет использовать простой набор эвристик, чтобы определить главный исполняемый файл приложения, и пометит его в манифесте как точку входа приложения ClickOnce.<br /><br /> Программа Mage.exe никогда не помечает файл как файл "данных". Это необходимо сделать вручную. Для получения дополнительной информации см. [How to: Include a Data File in a ClickOnce Application](/visualstudio/deployment/how-to-include-a-data-file-in-a-clickonce-application).<br /><br /> Программа Mage.exe также создает хэш для каждого файла в зависимости от его размера. Технология ClickOnce использует эти хэши, чтобы гарантировать отсутствие злонамеренного изменения файлов развертывания с момента создания манифеста. При изменении любого из файлов развертывания можно запустить программу Mage.exe с командой **-Update** и параметром **-FromDirectory** , и она обновит хэши и версии сборки для всех указанных файлов.<br /><br /> **-FromDirectory** включает все файлы во всех подкаталогах, найденных в каталоге `directoryPath`.<br /><br /> При использовании параметра **-FromDirectory** с командой **-Update** программа Mage.exe удалит из манифеста приложения все файлы, которые больше не существуют в каталоге.|  
|**-if, -IconFile**  `filePath`||Манифесты приложений.|Задает полный путь к ICO-файлу значка. Этот значок отображается рядом с именем приложения в меню "Пуск" и в разделе "Установка или удаление программ". Если значок не задан, используется значок по умолчанию.|  
|**-ip, -IncludeProviderURL**  `url`|true|Манифесты развертывания.|Указывает, содержит ли манифест развертывания значение расположения обновления, заданное параметром **-ProviderURL**.|  
|**-i, -Install** `willInstall`|true|Манифесты развертывания.|Указывает, должно ли приложение ClickOnce устанавливаться на локальном компьютере или оно должно запускаться из Интернета. При установке приложения оно появляется в меню **Пуск** в ОС Windows. Допустимыми являются значения "true" или "t" и "false" или "f".<br /><br /> Если задан параметр **-MinVersion** и пользователь использует версию, более раннюю по сравнению с **-MinVersion** , этот параметр вызывает принудительную установку приложения, независимо от значения, переданного в **-Install**.<br /><br /> Данный параметр невозможно использовать одновременно с параметром **-BrowserHosted** . Попытка задать оба параметра в одном манифесте приведет к ошибке.|  
|**-mv, -MinVersion**  `[version]`|Версия, указанная в манифесте развертывания ClickOnce и заданная флагом **-Version** .|Манифесты развертывания.|Минимальная версия этого приложения, которую может запустить пользователь. Этот флаг делает названную версию приложения обязательным обновлением. Если разработчик выпускает версию своего программного продукта с обновлением, включающим в себя критическое изменение или устранение критической уязвимости в системе безопасности, с помощью этого флага можно указать обязательность установки этого обновления и невозможность для пользователя дальнейшего использования предыдущих версий приложения.<br /><br /> Семантика параметра`version` совпадает с семантикой аргумента флага **-Version** .|  
|**-n, -Name** `nameString`|Развертывание|Все типы файлов.|Имя, используемое для идентификации приложения. Технология ClickOnce будет использовать это имя для идентификации приложения в меню **Пуск** (если для приложения настроена автоматическая установка) и в диалоговых окнах повышения уровня разрешений. **Примечание**. Если при обновлении существующего манифеста имя издателя не указывается с помощью этого параметра, программа Mage.exe обновляет манифест, используя имя организации, заданное на компьютере. Чтобы использовать другое имя, следует обязательно задать требуемое имя издателя с помощью этого параметра.|  
|**-pwd, -Password** `passwd`||Все типы файлов.|Пароль, используемый для подписания манифеста с помощью цифрового сертификата. Должен использоваться вместе с параметром **-CertFile** .|  
|**-p, Processor** `processorValue`|Msil|Манифесты приложений.<br /><br /> Манифесты развертывания.|Архитектура микропроцессора, на которой будет выполняться это развертывание. Это значение обязательно при подготовке одной или нескольких установок, компиляция сборок которых для конкретного микропроцессора была выполнена заранее. Допустимые значения включают `msil`, `x86`, `ia64`и `amd64`. `msil` — это промежуточный язык Майкрософт, который означает, что все сборки являются независимыми от платформы, и среда CLR будет выполнять их JIT-компиляцию при первом запуске приложения.|  
|**-pu,** **-ProviderURL** `url`||Манифесты развертывания.|Задает URL-адрес, который приложение ClickOnce будет использовать для обновлений приложения.|  
|**-pub, -Publisher** `publisherName`||Манифесты приложений.<br /><br /> Манифесты развертывания.|Добавляет имя издателя в элемент описания либо манифеста развертывания, либо манифеста приложения. При использовании этого параметра для манифеста приложения должен быть также задан параметр **-UseManifestForTrust** со значением "true" или "t", в противном случае этот параметр вызовет ошибку.|  
|**-s, -SupportURL**  `url`||Манифесты приложений.<br /><br /> Манифесты развертывания.|Указывает ссылку, которая появляется в диалоговом окне "Установка и удаление программ" для приложения ClickOnce.|  
|**-ti, -TimestampUri** `uri`||Манифесты приложений.<br /><br /> Манифесты развертывания.|URL-адрес службы цифровых отметок времени. Установка меток времени в манифестах позволяет избежать повторной подписи манифестов, когда срок действия цифрового сертификата истекает до развертывания следующей версии приложения. Дополнительные сведения см. в разделе [Участники программы корневых сертификатов Windows](http://go.microsoft.com/fwlink/?LinkId=159000).|  
|**-t, -ToFile** `filePath`|— New:<br />— Deployment: deploy.application<br />— Application: application.exe.manifest<br />— Update:<br />— Входной файл.|Все типы файлов.|Задает выходной путь для созданного или измененного файла.<br /><br /> Если при использовании команды **-New** не задан параметр **-ToFile**, результат записывается в текущий рабочий каталог. Если при использовании команды **-Update** не задан параметр **-ToFile**, программа Mage.exe записывает файл обратно во входной файл.|  
|**-tr, -TrustLevel** `level`|Зависит от зоны, в которой находится URL-адрес приложения.|Манифесты приложений.|Уровень доверия, предоставляемый приложению на клиентских компьютерах. Возможными значениями являются "Internet", "Intranet" и "FullTrust".|  
|**-um, -UseManifestForTrust** `willUseForTrust`|False|Манифесты приложений.|Определяет, будет ли использоваться цифровая подпись манифеста приложения для принятия решений о доверии при выполнении приложения на клиенте. Задание значения "true" или "t" указывает, что для решений о доверии будет использоваться манифест приложения. Задание значения "false" или "f" указывает, что будет использоваться подпись манифеста развертывания.|  
|**-v, -Version** `versionNumber`|1.0.0.0|Манифесты приложений.<br /><br /> Манифесты развертывания.|Версия развертывания. Аргумент должен быть строкой допустимой версии в формате "*N.N.N.N*", где "*N*" — это 32-разрядное целое число без знака.|  
|**-wpf, -WPFBrowserApp**  `isWPFApp`|False|Манифесты приложений.<br /><br /> Манифесты развертывания.|Этот флаг используется, только если приложение является приложением Windows Presentation Foundation (WPF), размещаемым в Internet Explorer, а не автономным исполняемым файлом. Допустимыми являются значения "true" или "t" и "false" или "f".<br /><br /> Для манифестов приложений вставляет атрибут `hostInBrowser` под элементом `entryPoint` манифеста приложения.<br /><br /> Для манифестов развертывания задает значение атрибута `install` для элемента `deployment` как "false" и сохраняет манифест развертывания с расширением XBAP. Задание этого аргумента вместе с аргументом **-Install** приводит к ошибке, так как приложение, размещенное в браузере, не может быть устанавливаемым, автономным приложением.|  
  
<a name="Sign"></a>   
## <a name="sign-command-options"></a>Параметры команды "Sign"  
 В следующей таблице указаны параметры команды `-Sign` , применяемой ко всем типам файлов.  
  
|Параметры|Описание|  
|-------------|-----------------|  
|**-cf, -CertFile** `filePath`|Задает местонахождение цифрового сертификата для подписания манифеста. Этот параметр может использоваться вместе с параметром **-Password** .|  
|**-ch, -CertHash** `hashSignature`|Хэш цифрового сертификата, хранящегося в хранилище личных сертификатов на клиентском компьютере. Соответствует свойству отпечатка цифрового сертификата, отображаемого в консоли сертификатов Windows.<br /><br /> Параметр`hashSignature` может быть задан или в верхнем, или в нижнем регистре, и может предоставляться либо как единая строка, либо в виде всех октетов отпечатка, разделенных пробелами, и всего отпечатка, заключенного в кавычки.|  
|**-pwd, -Password** `passwd`|Пароль, используемый для подписания манифеста с помощью цифрового сертификата. Должен использоваться вместе с параметром **-CertFile** .|  
|**-t, -ToFile** `filePath`|Задает выходной путь для созданного или измененного файла.|  
  
## <a name="remarks"></a>Примечания  
 Все аргументы программы Mage.exe не зависят от регистра символов. Перед командами и параметрами должен быть поставлен дефис (-) или косая черта (/).  
  
 Все аргументы, используемые с командой **-Sign** , всегда можно использовать вместе с командой **-New** или **-Update** . Следующие команды являются эквивалентными.  
  
```  
mage -Sign c:\HelloWorldDeployment\HelloWorld.deploy -CertFile cert.pfx  
mage -Update c:\HelloWorldDeployment\HelloWorld.deploy -CertFile cert.pfx  
```  
  
> [!NOTE]
>  Начиная с .NET Framework 4.6.2, также поддерживаются сертификаты CNG.  
  
 Подписание — это последняя задача, которую должен выполнить разработчик, поскольку для проверки правильности подписи документа подписанный документ использует хэш файла. При внесении в файл каких-либо изменений разработчик должен снова подписать этот файл. Если подписывается документ, который уже был подписан, программа Mage.exe заменяет старую подпись новой.  
  
 При использовании параметра **-AppManifest** для заполнения манифеста развертывания программа Mage.exe предполагает, что манифест приложения будет находиться в том же каталоге, что и манифест развертывания, в подкаталоге, название которого соответствует текущей версии развертывания, и соответствующим образом настраивает манифест развертывания. Если манифест приложения будет находиться в другом месте, для указания альтернативного расположения можно использовать параметр **-AppCodeBase** .  
  
 Перед развертыванием приложения манифест развертывания и манифест приложения должны быть подписаны. Руководство по подписанию документов см. в разделе [Общие сведения о развертывании доверенных приложений](/visualstudio/deployment/trusted-application-deployment-overview).  
  
 Параметр **-TrustLevel** для манифестов приложений описывает набор разрешений, необходимых приложению для выполнения на клиентском компьютере. По умолчанию уровень доверия, назначаемый приложениями, зависит от *зоны* , в которой находится URL-адрес. Приложения, развертываемые в корпоративной сети, обычно помещаются в зоне интрасети, а приложения, развертываемые через Интернет, размещаются в зоне Интернета. Обе зоны безопасности налагают на приложение ограничения доступа к локальным ресурсам, при этом зона интрасети предоставляет чуть больше прав, чем зона Интернета. В зоне полного доверия (FullTrust) приложениям предоставляется полный доступ к локальным ресурсам компьютера. Если для помещения приложения в эту зону используется параметр **-TrustLevel** , менеджер доверия среды CLR предложит пользователю решить, следует ли предоставить повышенный уровень доверия. Если приложение развертывается в корпоративной сети, можно использовать развертывание доверенных приложений, чтобы повысить уровень доверия приложения без участия пользователя.  
  
 Манифесты приложений также поддерживают настраиваемые разделы доверия. Это помогает приложению соблюдать принцип безопасности (запрос минимально необходимых разрешений), позволяя настроить манифест на запрос только конкретных разрешений, которые требуются приложению для работы. Программа Mage.exe не поддерживает прямое добавление настраиваемого раздела доверия. Такой раздел можно добавить с помощью текстового редактора, синтаксического анализа XML или графического средства MageUI.exe. Дополнительные сведения об использовании программы MageUI.exe для добавления настраиваемых разделов доверия см. в разделе [MageUI.exe (Manifest Generation and Editing Tool, Graphical Client)](../../../docs/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client.md).  
  
 Новые манифесты, созданные с помощью программы Mage.exe версии 4, входящей в состав [!INCLUDE[vs_dev10_long](../../../includes/vs-dev10-long-md.md)], предназначены для [!INCLUDE[net_client_v40_long](../../../includes/net-client-v40-long-md.md)]. Для использования более ранних версий платформы .NET Framework следует использовать более раннюю версию программы Mage.exe. При добавлении или удалении сборок из существующего манифеста или повторном подписывании существующего манифеста программа MageUI.exe не обновляет манифест до [!INCLUDE[net_client_v40_long](../../../includes/net-client-v40-long-md.md)]. В следующих таблицах показаны эти возможности и ограничения.  
  
|Версия манифеста|Операция|Mage v2.0|Mage v4.0|  
|----------------------|---------------|---------------|---------------|  
|Манифест для приложений, предназначенных для .NET Framework версии 2.0 или 3.x|Открыть|ОК|ОК|  
||Закрыть|ОК|ОК|  
||Сохранение|ОК|ОК|  
||Повторно подписать|ОК|ОК|  
||Новый|ОК|Не поддерживается|  
||Обновить (см. ниже)|ОК|ОК|  
|Манифест для приложений, предназначенных для .NET Framework версии 4|Открыть|ОК|ОК|  
||Закрыть|ОК|ОК|  
||Сохранение|ОК|ОК|  
||Повторно подписать|ОК|ОК|  
||Новый|Не поддерживается|ОК|  
||Обновить (см. ниже)|Не поддерживается|ОК|  
  
|Версия манифеста|Обновить сведения об операции|Mage v2.0|Mage v4.0|  
|----------------------|------------------------------|---------------|---------------|  
|Манифест для приложений, предназначенных для .NET Framework версии 2.0 или 3.x|Изменить сборку|ОК|ОК|  
||Добавить сборку|ОК|ОК|  
||Удалить сборку|ОК|ОК|  
|Манифест для приложений, предназначенных для .NET Framework версии 4|Изменить сборку|Не поддерживается|ОК|  
||Добавить сборку|Не поддерживается|ОК|  
||Удалить сборку|Не поддерживается|ОК|  
  
 Программа Mage.exe создает новые манифесты, предназначенные для [!INCLUDE[net_client_v40_long](../../../includes/net-client-v40-long-md.md)]. Приложения ClickOnce, предназначенные для [!INCLUDE[net_client_v40_long](../../../includes/net-client-v40-long-md.md)] , могут работать как в [!INCLUDE[net_client_v40_long](../../../includes/net-client-v40-long-md.md)] , так и в полной версии [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]. Если приложение предназначено для полной версии [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] и не может выполняться в [!INCLUDE[net_client_v40_long](../../../includes/net-client-v40-long-md.md)], удалите клиентский элемент `<framework>` с помощью текстового редактора и повторно подпишите манифест. Ниже приведен пример элемента `<framework>` , предназначенного для [!INCLUDE[net_client_v40_long](../../../includes/net-client-v40-long-md.md)].  
  
```xml  
<framework targetVersion="4.0" profile="client" supportedRuntime="4.0.20506" />  
```  
  
## <a name="examples"></a>Примеры  
 В следующем примере показано открытие пользовательского интерфейса для программы Mage (MageUI.Exe).  
  
```  
mage  
```  
  
 В следующих примерах показано создание манифеста развертывания и манифеста приложения по умолчанию. Эти файлы создаются в текущем рабочем каталоге и называются "deploy.application" и "application.exe.manifest" соответственно.  
  
```  
mage -New Deployment  
mage -New Application  
```  
  
 В следующем примере показано создание манифеста приложения, заполненного всеми сборками и файлами ресурсов из текущего каталога.  
  
```  
mage -New Application -FromDirectory . -Version 1.0.0.0  
```  
  
 В следующем примере показано продолжение предыдущего примера с указанием имени развертывания и целевого микропроцессора. В нем также показано задание URL-адреса, который приложение ClickOnce должно использовать для проверки обновлений.  
  
```  
mage -New Application -FromDirectory . -Name "Hello, World! Application" -Version 1.0.0.0 -Processor "x86" -ProviderUrl http://internalserver/HelloWorld/  
```  
  
 В следующем примере показано создание пары манифестов для развертывания приложения WPF, размещаемого в Internet Explorer.  
  
```  
mage -New Application -FromDirectory . -Version 1.0.0.0 -WPFBrowserApp true  
mage -New Deployment -AppManifest 1.0.0.0\application.manifest -WPFBrowserApp true  
```  
  
 В следующем примере в манифест развертывания добавляются сведения из манифеста приложения и задается база кода для местонахождения манифеста приложения.  
  
```  
mage -Update HelloWorld.deploy -AppManifest 1.0.0.0\application.manifest -AppCodeBase http://internalserver/HelloWorld.deploy  
```  
  
 В следующем примере изменяется манифест развертывания для принудительного обновления установленной у пользователя версии.  
  
```  
mage -Update c:\HelloWorldDeployment\HelloWorld.deploy -MinVersion 1.1.0.0  
```  
  
 В следующем примере манифест развертывания получает указание извлекать манифест приложения из другого каталога.  
  
```  
mage -Update HelloWorld.deploy -AppCodeBase http://anotherserver/HelloWorld/1.1.0.0/  
```  
  
 В следующем примере существующий манифест развертывания подписывается с помощью цифрового сертификата в текущем рабочем каталоге.  
  
```  
mage -Sign deploy.application -CertFile cert.pfx -Password <passwd>  
```  
  
## <a name="see-also"></a>См. также  
 [Развертывание и безопасность технологии ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment)   
 [Пошаговое руководство. Развертывание вручную приложения ClickOnce](/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-application)   
 [Общие сведения о развертывании доверенных приложений](/visualstudio/deployment/trusted-application-deployment-overview)   
 [MageUI.exe (средство создания и редактирования манифестов, графический клиент)](../../../docs/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client.md)   
 [Командные строки](../../../docs/framework/tools/developer-command-prompt-for-vs.md)