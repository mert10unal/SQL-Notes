# SQL-Notes
some revision notes about views / stored procedures / Index

Primary key
--> Ana belirteç, yani bir tablodaki rowları (kayıtları) birbirinden ayırt etmemize yardım eden anahtar, özellik (Örnek : Id,Name...)

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

Stored Procedures
CREATE PROCEDURE MostOrderedProducts
AS
SELECT ProductName,Price FROM Products
GO;

EXEC procedure_name;

OR
CREATE PROCEDURE SelectAllCustomers @City nvarchar(30)
AS
SELECT * FROM Customers WHERE City = @City
GO;
Burada neden özellikle stored procedure kullanıyoruz : hangi şehri daha sık kullanacağımız belli olsaydı gerek olmazdı fakat birden fazla şehir ismi varsa @City kullanmak daha doğru olur. Buradaki stored procedure, bize City adlı columnun çok sık kullanıldığını gösterir

Soru : table tanımlarken zaten City değişkenini nvarchar olarak tanımlıyoruz. Burada özellikle karakter sınırı atamamızın sebebi nedir ?

Index
--> sıkça sorulan sorulardaki veya sıkça kullanılacak değişkenleri bir arada toplamak için kullanılır
    CREATE INDEX idx_lastname
    ON Persons (LastName); --> burada tablo sayısı arttırılarak farklı kayıtlar da eklenebilir.s
    
    İki farklı işlem yapılmış olacak ama çok daha pratik bir işlem, çünkü bilgisayarın tüm veritabanını araması gerekecek öbür türlü
    ![image](https://github.com/mert10unal/SQL-Notes/assets/120198895/5076b02b-96c9-401c-a734-bd4d59d79a35)

Clustered Index
--> verilerin fiziksel olarak tutulup saklanması
--> seçilen kolon en çok kullanılan olmalıdır ve az değiştirilmelidir --> sık değiştirilirse fiziksel sıralama da değişir ve vakit kaybı
CREATE CLUSTERED INDEX IX_IndexName ON TableName (Column1);

Non-Clustered Index
--> Mantıksal olarak sıralama. Şu sayı aralığı şu sayfada gibi
--> CREATE NONCLUSTERED INDEX IX_IndexName ON TableName (Column1);

Unique Index
--> primary key ve unique kısıtlayıcıları
--> birden fazla eklenebilir

Filtered Index
--> normal yaratılan indexten farklı olarak bir koşul filtrelenir, yani where komutuyla yaratılan index sınırlanılır.
CREATE NONCLUSTERED INDEX IX_IndexName ON TableName (Column1) WHERE ...;

Composite Index
CREATE INDEX [indexadi] ON [dbo].[tabloadi] ([kolonadi1] ASC/DESC,[kolonadi2] ASC/DESC )

Covered Index
CREATE NONCLUSTERED INDEX IX_IndexName ON TableName (Column1) INCLUDE (Column2, Column3);


* Unique-primary key constraints, frequently used columns
