---
title: "Создание приложений многоадресной рассылки с помощью транспорта определяемой пользователем функции | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7485154a-6e85-4a67-a9d4-9008e741d4df
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Создание приложений многоадресной рассылки с помощью транспорта определяемой пользователем функции
Приложения многоадресной рассылки одновременно отправляют маленькие сообщения большому количеству получателей без необходимости установления прямого соединения.Подобные приложения прежде всего ориентируются на скорость выполнения, а не на надежность.Другими словами, отправка данных точно в срок важнее обеспечения доставки конкретного сообщения.WCF теперь поддерживает создание приложений многоадресной рассылки с помощью <xref:System.ServiceModel.UdpBinding>.Этот транспорт может оказаться полезным в тех случаях, когда служба должна одновременно отправлять маленькие сообщения множеству клиентов.Пример подобной службы — приложение, работающее с биржевыми сводками.  
  
## Реализация приложения многоадресной рассылки  
 Чтобы реализовать приложение многоадресной рассылки, определите контракт службы и реализуйте контракт службы для каждого программного компонента, который должен отвечать на сообщения многоадресной рассылки.Например, приложение для работы с биржевыми сводками может определить такой контракт:  
  
```  
// Shared contracts between the client and the service  
    [ServiceContract]  
    interface IStockTicker  
    {  
        [OperationContract(IsOneWay = true)]  
        void SendStockInfo(StockInfo[] stockInfo);  
    }  
  
    [DataContract]  
    class StockInfo  
    {  
        [DataMember]  
        public string Symbol;  
  
        [DataMember]  
        public float Price;  
  
        public StockInfo(string symbol, float price)  
        {  
            this.Symbol = symbol;  
            this.Price = price;  
        }  
    }  
  
```  
  
 Каждое приложение, которое хочет получать сообщения многоадресной рассылки, должно разместить службу, реализующую данный интерфейс.Ниже представлен образец кода, демонстрирующий получение сообщений многоадресной рассылки:  
  
```  
// Service Address  
            string serviceAddress = "soap.udp://224.0.0.1:40000";  
            // Binding  
            UdpBinding myBinding = new UdpBinding();  
            // Host  
            ServiceHost host = new ServiceHost(typeof  
                (StockTickerService), new Uri(serviceAddress));  
            // Add service endpoint  
            host.AddServiceEndpoint(typeof(IStockTicker), myBinding, string.Empty);  
            // Openup the service host  
            host.Open();  
  
            Console.WriteLine("Start receiving stock information");  
            Console.ReadLine();  
  
```  
  
 Приложение задает UDP\-адрес, который будут прослушивать все службы.Создается новый объект <xref:System.ServiceModel.ServiceHost>, и конечная точка службы предоставляется с помощью <xref:System.ServiceModel.UdpBinding>.Затем <xref:System.ServiceModel.ServiceHost> открывается и ожидает передачи данных для входящих сообщений.  
  
 В подобном варианте работы приложения клиент отправляет сообщения многоадресной рассылки.Каждая служба, которая ожидает прослушивания по правильному UDP\-адресу, получит сообщения многоадресной рассылки.Ниже приведен пример клиента, который отправляет сообщения многоадресной рассылки:  
  
```  
// Multicast Address  
            string serviceAddress = "soap.udp://224.0.0.1:40000";  
  
            // Binding  
            UdpBinding myBinding = new UdpBinding();  
  
            // Channel factory  
            ChannelFactory<IStockTicker> factory  
                = new ChannelFactory<IStockTicker>(myBinding,  
                            new EndpointAddress(serviceAddress));  
  
            // Call service  
            IStockTicker proxy = factory.CreateChannel();  
  
            while (true)  
            {  
                // This will continue to mulicast stock information   
                proxy.SendStockInfo(GetStockInfo());  
                Console.WriteLine(String.Format("sent stock info at {0}", DateTime.Now));  
                // Wait for one second before sending another update  
                System.Threading.Thread.Sleep(new TimeSpan(0, 0, 1));  
            }  
  
```  
  
 Данный код создает сводку биржевых данных и затем использует контракт службы IStockTicker для многоадресной отправки сообщений и вызова служб, слушающих определенный UDP\-адрес.  
  
### Протокол UDP и надежный обмен сообщениями  
 Привязка к UDP\-протоколу не поддерживает надежный обмен сообщениями из\-за особенностей самого протокола UDP.Если вам необходимо подтвердить получение сообщений удаленной конечной точкой, используйте транспорт, поддерживающий надежный обмен сообщениями, например протокол HTTP или TCP.Дополнительные сведения о надежном обмене сообщениями см. по адресу http:\/\/go.microsoft.com\/fwlink\/?LinkId\=231830  
  
### Двусторонняя многоадресная отправка сообщений  
 Хотя сообщения многоадресной рассылки обычно отправляются в одну сторону, транспорт UdpBinding поддерживает обмен сообщениями в режиме запрос\-ответ.Сообщения, отправленные с помощью транспорта UDP, содержат адреса отправителя и получателя.Следует соблюдать предосторожность при использовании адреса отправителя, так как он может быть изменен злоумышленниками в ходе доставки сообщения.Адрес можно проверить с помощью следующего кода:  
  
```  
if (address.AddressFamily == AddressFamily.InterNetwork)  
          {  
              // IPv4  
              byte[] addressBytes = address.GetAddressBytes();  
              return ((addressBytes[0] & 0xE0) == 0xE0);  
          }  
          else  
          {  
              // IPv6   
              return address.IsIPv6Multicast;  
          }  
  
```  
  
 Данный код проверяет первый байт из адреса отправителя, чтобы определить, содержит ли он байт 0xE0, который означает, что это адрес многоадресной рассылки.  
  
### Вопросы безопасности  
 При прослушивании сообщений многоадресной рассылки маршрутизатору отправляется ICMP\-пакет, извещающий его о вашем прослушивании адреса многоадресной рассылки.Любой пользователь локальной подсети, имеющий соответствующие разрешения, может прослушивать пакеты подобных типов и определять прослушиваемый вами адрес и порт и многоадресной рассылки.  
  
 Не используйте IP\-адрес отправителя по соображениям безопасности.Эта информация может быт подделана, и приложение может начать отправлять ответы на другой компьютер.Включение безопасности на уровне сообщения позволяет убрать подобную угрозу безопасности.На уровне сети используйте IPSec \(Internet Protocol Security\) и\/или NAP \(Network Access Protection\).