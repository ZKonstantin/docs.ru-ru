---
title: "Поставщик WMI | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 462f0db3-f4a4-4a4b-ac26-41fc25c670a4
caps.latest.revision: 35
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 35
---
# Поставщик WMI
В этом образце показано, как собирать данные из служб [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] во время выполнения, используя встроенный в [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] поставщик инструментария управления Windows \(WMI\).  Кроме того, в образце показано, как добавлять в службу пользовательский объект инструментария WMI.  Этот образец активирует поставщик инструментария WMI для [Начало работы](../../../../docs/framework/wcf/samples/getting-started-sample.md) и показывает, как собирать данные из службы `ICalculator` во время выполнения.  
  
 Инструментарий WMI \- это реализованный корпорацией Майкрософт стандарт управления предприятием через Интернет \(WBEM\).  Дополнительные сведения о пакете WMI SDK см. в библиотеке MSDN.  \(http:\/\/msdn.microsoft.com\/library\/default.asp?url\=\/library\/wmisdk\/wmi\/wmi\_start\_page.asp\).  WBEM является отраслевым стандартом предоставления приложениями инструментария управления для внешних средств управления.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] реализует поставщик инструментария WMI, компонент, предоставляющий инструментарий в среде выполнения с помощью совместимого с WBEM интерфейса.  Средства управления могут подключаться к службам через интерфейс во время выполнения.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] предоставляет атрибуты служб, такие как адреса, привязки, поведения и прослушиватели.  
  
 Встроенный поставщик инструментария WMI активируется в файле конфигурации приложения.  Это делается с помощью атрибута `wmiProviderEnabled` [\<диагностика\>](../../../../docs/framework/configure-apps/file-schema/wcf/diagnostics.md) в разделе [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md), как показано в следующем примере конфигурации.  
  
```  
<system.serviceModel>  
    ...  
    <diagnostics wmiProviderEnabled="true" />  
    ...  
</system.serviceModel>  
  
```  
  
 Эта запись конфигурации предоставляет интерфейс инструментария WMI.  Теперь приложения управления могут подключаться через этот интерфейс и обращаться к инструментарию управления приложения.  
  
## Пользовательский объект WMI  
 Добавление в службу объектов WMI позволяет предоставлять доступ к пользовательским сведениям, а также к сведениям встроенного поставщика WMI.  Для этого необходимо опубликовать схему службы в инструментарии WMI с помощью приложения Installutil.exe.  Соответствующие инструкции, а также более подробные сведения, см в инструкция по установке в конце этого раздела.  
  
## Доступ к сведениям WMI  
 Доступ к данным инструментария WMI может осуществляться несколькими различными способами.  Корпорация Майкрософт предоставляет интерфейсы API инструментария WMI API для скриптов, приложений [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)], приложений C\+\+ и [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] \(http:\/\/msdn.microsoft.com\/library\/default.asp?url\=\/library\/wmisdk\/wmi\/using\_wmi.asp\).  
  
 В этом образце используется два скрипта Java: один \- для перечисления выполняющихся на компьютере служб и некоторых их свойств, а второй \- для просмотра пользовательских данных инструментария WMI.  Скрипт открывает подключение к поставщику инструментария WMI, анализирует данные и отображает собранные данные.  
  
 Запустите образец путем создания выполняющегося экземпляра службы [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  Во время работы службы выполните каждый из скриптов Java с помощью следующей команды командной строки:  
  
```  
cscript EnumerateServices.js  
  
```  
  
 Этот скрипт обращается к хранящемуся в службе инструментированию и создает следующий результат:  
  
```  
Microsoft (R) Windows Script Host Version 5.6  
Copyright © Microsoft Corporation 1996-2001. All rights reserved.  
  
1 service(s) found.  
|-PID:           5776  
|-DistinguishedName:  CalculatorService@http://localhost/ServiceModelSamples/service.svc  
|-Endpoints:     1 endpoints  
  |-CalculatorService.ICalculator@http://localhost/ServiceModelSamples/service.svc  
    |-Address:                        http://localhost/ServiceModelSamples/service.svc  
    |-CounterInstanceName:  
    |-AddressHeaders:                 0  
    |-ContractType:                   Contract.Name='ICalculator'  
    |-BindingElements:                4 bindings  
      |-BindingElements[0]  
        |-Type:                       TransactionFlowBindingElement  
      |-BindingElements[1]  
        |-Type:                       SymmetricSecurityBindingElement  
      |-BindingElements[2]  
        |-Type:                       TextMessageEncodingBindingElement  
        |-MaxReadPoolSize:            64  
        |-MaxWritePoolSize:           16  
      |-BindingElements[3]  
        |-Type:                       HttpTransportBindingElement  
        |-ManualAddressing:           false  
        |-MaxBufferSize:              65536  
        |-AllowCookies:               false  
        |-AuthenticationScheme:       Anonymous  
        |-BypassProxyOnLocal:         false  
        |-HostNameComparisonMode:     StrongWildcard  
        |-ProxyAddress:               null  
        |-ProxyAuthenticationScheme:  Anonymous  
        |-Realm:  
        |-TransferMode:               Buffered  
        |-UseDefaultWebProxy:         true  
|-Behaviors:     5 behaviors  
      |-Behavior[0]  
      |-Type:                       ServiceBehaviorAttribute  
        |-AddressFilterMode:               Exact  
        |-AutomaticSessionShutdown:        true  
        |-ConcurrencyMode:                 Single  
        |-IncludeExceptionDetailInFaults:  false  
        |-InstanceContextMode:             PerSession  
        |-TransactionIsolationLevel:       Unspecified  
        |-TransactionTimeout:              null  
        |-ValidateMustUnderstand:          true  
      |-Behavior[1]  
      |-Type:                       AspNetCompatibilityRequirementsAttribute  
      |-Behavior[2]  
      |-Type:                       ServiceDebugBehavior  
      |-Behavior[3]  
      |-Type:                       ServiceAuthorizationBehavior  
      |-Behavior[4]  
      |-Type:                       Behavior  
```  
  
 Затем выполните второй скрипт Java, чтобы отобразить пользовательские данные WMI:  
  
```  
cscript EnumerateCustomObjects.js  
```  
  
 Этот скрипт обращается к хранящемуся в службах пользовательскому инструментированию и создает следующий результат:  
  
```  
  
1 WMIObject(s) found.  
|-PID:           30285bfd-9d66-4c4e-9be2-310499c5cef5  
|-InstanceId:    3839  
|-WMIInfo:       User Defined WMI Information.  
  
```  
  
 Сценарий показывает, что на компьютере запущена одна служба.  Служба предоставляет одну конечную точку, реализующую контракт `ICalculator`.  Параметры поведения и привязки, реализуемых конечной точкой, задаются в виде отдельных элементов стека обмена сообщениями.  
  
 Инструментарий WMI не ограничивается инструментированием управления инфраструктуры [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  Приложение может предоставлять собственные относящиеся к домену элементы данных, используя для этого такой же механизм.  Инструментарий WMI представляет собой единый механизм для контроля веб\-службы и управления ею.  
  
#### Настройка, сборка и выполнение образца  
  
1.  Убедитесь, что выполнена [Процедура однократной настройки образцов Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Для сборки выпуска .NET C\# или Visual Basic этого решения следуйте инструкциям в разделе [Построение образцов Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Опубликуйте схему служб в WMI, запустив программу InstallUtil.exe \(по умолчанию файл InstallUtil.exe расположен в папке «%WINDIR%\\Microsoft.NET\\Framework\\v4.0.30319»\) для файла service.dll в каталоге размещения.  Эту операцию нужно выполнять только в том случае, если в файл service.dll были внесены изменения.  Дополнительные сведения см. в подразделе "Предоставление данных управления с помощью инструментирования приложений" на странице http:\/\/msdn2.microsoft.com\/library\/ms186147.aspx в разделе "Практическое руководство. Публикация схемы в WMI для инструментированного приложения".  
  
4.  При выполнении образца в конфигурации с одним или с несколькими компьютерами следуйте инструкциям в разделе [Выполнение примеров Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
    > [!NOTE]
    >  Если платформа [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] устанавливалась после ASP.NET, может потребоваться выполнить команду "%WINDIR%\\ Microsoft.Net\\Framework\\v3.0\\Windows Communication Foundation\\servicemodelreg.exe " \-r \-x, чтобы предоставить учетной записи ASPNET разрешение на публикацию объектов WMI.  
  
5.  Для просмотра данных из образцов, доступных через WMI, следует воспользоваться командами: `cscript EnumerateServices.js` или `cscript EnumerateCustomObjects.js`.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере.  Перед продолжением проверьте следующий каталог \(по умолчанию\).  
>   
>  `<диск_установки>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Образцы Windows Communication Foundation \(WCF\) и Windows Workflow Foundation \(WF\) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780), чтобы загрузить все образцы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Этот образец расположен в следующем каталоге.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\WMIProvider`  
  
## См. также  
 [Примеры мониторинга AppFabric](http://go.microsoft.com/fwlink/?LinkId=193959)