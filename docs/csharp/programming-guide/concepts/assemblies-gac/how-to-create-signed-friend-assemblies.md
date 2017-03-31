---
title: "Практическое руководство. Создание подписанных дружественных сборок (C#) | Документы Майкрософт"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: bab62063-61e6-453f-905f-77673df9534e
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 890cead4b28b8532dd7bd7f571defe7e280e4cdc
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-signed-friend-assemblies-c"></a>Практическое руководство. Создание подписанных дружественных сборок (C#)
В этом примере демонстрируется использование дружественных сборок со сборками, имеющими строгие имена. Обе сборки должны иметь строгое имя. Хотя обе сборки в этом примере используют одинаковые ключи, вы можете использовать для двух сборок разные ключи.  
  
### <a name="to-create-a-signed-assembly-and-a-friend-assembly"></a>Создание подписанной и дружественной сборки  
  
1.  Откройте окно командной строки.  
  
2.  Используйте следующую последовательность команд в средстве задания строгих имен для формирования файла ключа и отображения его открытого ключа. Дополнительные сведения см. на странице [Sn.exe (Strong Name Tool)](https://msdn.microsoft.com/library/k5b5tt23) (Sn.exe: средство строгих имен).  
  
    1.  Создайте ключ строгого имени для этого примера и сохраните его в файле FriendAssemblies.snk:  
  
         `sn -k FriendAssemblies.snk`  
  
    2.  Извлеките открытый ключ из FriendAssemblies.snk и поместите его в файл FriendAssemblies.publickey:  
  
         `sn -p FriendAssemblies.snk FriendAssemblies.publickey`  
  
    3.  Выведите на экран открытый ключ, хранящийся в файле FriendAssemblies.publickey:  
  
         `sn -tp FriendAssemblies.publickey`  
  
3.  Создайте файл C# с именем `friend_signed_A`, содержащий приведенный ниже код. Код использует атрибут <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> для объявления friend_signed_B в качестве дружественной сборки.  
  
     Средство задания строгих имен создает новый открытый ключ при каждом запуске. Таким образом, необходимо заменить открытый ключ в следующем коде только что созданным открытым ключом, как показано в следующем примере.  
  
    ```csharp  
    // friend_signed_A.cs  
    // Compile with:   
    // csc /target:library /keyfile:FriendAssemblies.snk friend_signed_A.cs  
    using System.Runtime.CompilerServices;  
  
    [assembly: InternalsVisibleTo("friend_signed_B, PublicKey=0024000004800000940000000602000000240000525341310004000001000100e3aedce99b7e10823920206f8e46cd5558b4ec7345bd1a5b201ffe71660625dcb8f9a08687d881c8f65a0dcf042f81475d2e88f3e3e273c8311ee40f952db306c02fbfc5d8bc6ee1e924e6ec8fe8c01932e0648a0d3e5695134af3bb7fab370d3012d083fa6b83179dd3d031053f72fc1f7da8459140b0af5afc4d2804deccb6")]  
    class Class1  
    {  
        public void Test()  
        {  
            System.Console.WriteLine("Class1.Test");  
            System.Console.ReadLine();  
        }  
    }  
    ```  
  
4.  Скомпилируйте и подпишите сборку friend_signed_A с помощью приведенной ниже команды.  
  
    ```csharp  
    csc /target:library /keyfile:FriendAssemblies.snk friend_signed_A.cs  
    ```  
  
5.  Создайте файл C# с именем `friend_signed_B`, содержащий следующий код. Поскольку сборка friend_signed_A указывает сборку friend_signed_B в качестве дружественной сборки, код в сборке friend_signed_B может обращаться к типам и членам `internal` в сборке friend_signed_A. Файл содержит следующий код.  
  
    ```csharp  
    // friend_signed_B.cs  
    // Compile with:   
    // csc /keyfile:FriendAssemblies.snk /r:friend_signed_A.dll /out:friend_signed_B.exe friend_signed_B.cs  
    public class Program  
    {  
        static void Main()  
        {  
            Class1 inst = new Class1();  
            inst.Test();  
        }  
    }  
    ```  
  
6.  Откомпилируйте и подпишите сборку friend_signed_B с помощью следующей команды.  
  
    ```csharp  
    csc /keyfile:FriendAssemblies.snk /r:friend_signed_A.dll /out:friend_signed_B.exe friend_signed_B.cs  
    ```  
  
     Имя сборки, созданное компилятором, должно соответствовать имени дружественной сборки, переданной в атрибут <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>. Необходимо явно указать имя выходной сборки (EXE или DLL) с помощью параметра компилятора `/out`.  Дополнительные сведения см. в разделе [/out (параметры компилятора C#)](../../../../csharp/language-reference/compiler-options/out-compiler-option.md).  
  
7.  Запустите файл friend_signed_B.exe.  
  
     Программа выводит строку "Class1.Test".  
  
## <a name="net-framework-security"></a>Безопасность платформы .NET Framework  
 Существует сходство между атрибутом <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> и классом <xref:System.Security.Permissions.StrongNameIdentityPermission>. Основное различие заключается в том, что <xref:System.Security.Permissions.StrongNameIdentityPermission> могут требоваться разрешения безопасности для выполнения определенного раздела кода, тогда как атрибут <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> контролирует видимость типов и членов `internal`.  
  
## <a name="see-also"></a>См. также  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>   
 [Сборки и глобальный кэш сборок (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/index.md)   
 [Дружественные сборки (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/friend-assemblies.md)   
 [Практическое руководство. Создание неподписанных дружественных сборок (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/how-to-create-unsigned-friend-assemblies.md)   
 [/keyfile](../../../../visual-basic/reference/command-line-compiler/keyfile.md)   
 [Sn.exe (средство строгих имен)](https://msdn.microsoft.com/library/k5b5tt23)   
 [Создание и использование сборок со строгими именами](https://msdn.microsoft.com/library/xwb8f617)   
 [Руководство по программированию на C#](../../../../csharp/programming-guide/index.md)