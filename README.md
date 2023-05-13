# SQL-Notes
some revision notes about views / stored procedures

Primary key
--> Ana belirteç, yani bir tablodaki rowları birbirinden ayırt etmemize yardım eden anahtar, özellik (Örnek : Id,Name...)

Foreign Key
--> n to n ilişkilerde tablolar arasındaki bağlantıyı kurmamızı sağlar. A'nın birden fazla B'si, B'nin de birden fazla A'sı olduğu durumlarda ara tablo eklenir ve bu tabloya foreign key bağlantısı eklenerek veri kontrolü sağlanır

Constraint
--> herhangi bir değişkeni limitleyici veya kontrol edici özellikler
    NOT NULL --> boş değer girilmesini kabul etmez
    UNIQUE --> Sadece o kayıt sütununa özel
    PRIMARY KEY --> ana belirteç
    DEFAULT --> eğer bir veri girilmezse o değere bilgisayardan girilen kayıdı ata
    CHECK --> herhangi bir columna girilen değerleri sınırlama
    Identity --> Unique ile benzer. Her bir columnun kendi identitysini gösteren bir değişkene eklenir : GENERATED ALWAYS AS IDENTITY, IDENTITY (1,1) 
    Auto Increment --> 1'den başlayıp her kayıtta 1-1 increment etmesi. Genellikle primary key özelliği olan sütunlarda kullanılır.
