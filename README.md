# .Net Mülakat Soruları

Mülakatlarda karşılaşılan bazı soruları içermektedir.

## Nesne Tabanlı Programlamanın dört temel kavramı nelerdir?

**Kapsülleme(Encapsulation) :** Bir nesnenin bazı özellik ve işlevleri, başka sınıf ve nesnelerden gizlenir. Veri uygulamasının geri kalanı gizlenirken yalnızca gerekli bilgilere erişilebilir.

**Soyutlama(Abstraction) :** Bir nesnenin kritik davranışını ve verilerini belirleme ve ilgisiz detayları ortadan kaldırma işlemidir.

**Kalıtım(Inheritence) :** Başka bir sınıftan yeni sınıflar oluşturma yeteneğidir. Üst sınıftaki nesnelerin davranışına erişilerek, değiştirilerek ve genişletilerek yapılır.

**Çok Biçimlilik(Polimorphism) :** İsim, tek isim, birçok form anlamına gelir. Aynı isimde ancak farklı uygulamalara sahip birden fazla methoda sahip olunması ile elde edilir.

## Referance ve Value Type nedir?

Value Type, dataları belleğin stack bölgesinde direk olarak saklayan nesnelerdir. Null değer alamazlar. Int, Char, Bool örnek verilebilir. Çoğu yerde Value Type için eş anlamlı olduğundan Primitive Type’da denmektedir.

Referance Type, dataları belleğin stack bölgesinde tutar ve ayrıca heap bölgesinde de bir referans değeri tutar. Null değer alabilir. String, Array, Class, List örnek verilebilir.

## ref ve out nedir?

Value Type'ları referansları ile methodlara parametre olarak verilmek istenildiğinde ref ve out anahtar kelimeleri kullanılması gerekir.

ref, bir method için parametre olarak kullanılırken değişken değeri bir başlangıç değeri almak zorundadır. Method içerisinde herhangi bir değişiklik yapmadan da kullanılabilir.
out, bir method için parametre olarak kullanılırken değişken değeri bir başlangıç değeri almak zorunda değildir. Method içerisinde herhangi bir değişiklik yapmadan da kullanılamaz.

```c#
public static void Main()
    {
        int refValue = 5; //başlangıç değeri atanması zorunludur.
        int outValue; //başlangıç değeri atanması zorunlu değildir.

        ChangeMethod(out outValue, ref refValue);

        Console.WriteLine("ChangeMethod'dan sonra refValue : " + refValue); //Output 7
        Console.WriteLine("ChangeMethod'dan sonra outValue: " + outValue); //Output 8
    }

    static void ChangeMethod(out int i,ref int j)
    {
          i = 8; // i argümanına bir değer atamak zorunludur.
          j = j + 2; // j için böyle bir zorunluluk yoktur.
    }
}
```

## IEnumerable ile IQueryable arasındaki fark nedir?

IEnumerable kullanılan koleksiyonlarda filtreleme yapılırken, önce tüm veriler çekilir, sonra filtreleme yapılır. Fakat IQueryable kullanılan koleksiyonlarda bir veri direkt olarak SQL tarafında filtrelenerek sadece ilgili veri bize gelir.

## Redis ve In-Memory Cache karşılaştırılması

Veri Yapıları: Memcached, basit bir anahtar-değer önbellek sistemidir ve sadece string veri türlerini destekler. Redis ise, daha karmaşık veri yapılarına (listeler, kümeler, hash'ler, vb.) ve daha fazla veri türüne (string, sayı, listeler, kümeler, hash'ler, vb.) destek verir.

Bellek Yönetimi: Memcached, bellek yönetimi için slab allocator adı verilen bir yöntem kullanır. Bu yöntem, belleği sabit boyutlu bloklara böler ve bu blokları kullanır. Redis ise, önbellek belleğini daha esnek bir şekilde yönetir ve bellek kullanımını daha iyi optimize edebilir.

Veri Saklama: Memcached, verileri bellekte saklar ve veri kaybı riski yüksektir. Redis ise, verileri bellekte saklar ve aynı zamanda verileri diskte de saklayabilir. Bu, Redis'in daha kalıcı bir veri saklama çözümü olduğu anlamına gelir.

Replication: Memcached, veri replikasyonu için birkaç farklı yöntem sunar, ancak bu yöntemler genellikle karmaşıktır ve performansı etkileyebilir. Redis ise, daha basit ve etkili bir replikasyon sistemi sunar ve veri kopyalama işlemi daha hızlı ve daha güvenilirdir.

Cluster Support: Redis, daha karmaşık veri yapılarını ve daha fazla veri türünü desteklediği için, daha büyük ölçekli uygulamalar için daha uygun olabilir. Redis, önbellek sunucularını bir küme olarak çalıştırmanıza ve verileri otomatik olarak dağıtmanıza olanak tanır. Memcached ise, daha basit bir yapıya sahiptir ve daha küçük ölçekli uygulamalar için daha uygun olabilir.

## C#’da bir Class’a farklı bir arayüz(Interface) ve Class miras(Inherit) etmem gerekiyor, sırası önemli mi ve kaç tane ekleyebilirim?

Bir Class hem Inherit hem de Interface ile kullanılacaksa önce Inherit Class sonra Interface dahil edilir. Bir tane Class Inherit alabilir, birden fazla Interface implement edilebilir. Aksi halde “Error CS1722 Base class ‘Person’ must come before any interfaces” hatası alınır.

```c#
public class Person
{
    public int Id { get; set; }
    public string Name { get; set; }
}

public class Student : Person, IDoSomething, IStudy
{
    public int SchoolNumber { get; set; }
}
```
