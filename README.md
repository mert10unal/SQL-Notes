# SQL-Notes
some revision notes about views / stored procedures / Index

Primary key
--> Main identifier, i.e. the key that helps us distinguish between rows (records) in a table, property (Example: Id, Name...)

Foreign Key
--> allows us to establish the connection between tables in n to n relationships. In cases where A has more than one B and B has more than one A, an intermediate table is added and data control is provided by adding a foreign key link to this table

Constraint
--> any variable limiting or controlling properties
    NOT NULL --> does not accept an empty value
    UNIQUE --> Only for that record column
    PRIMARY KEY --> main token
    DEFAULT --> if no data is entered, assign the record entered from the computer to that value
    CHECK --> limit the values entered in any column
    Identity --> Similar to Unique. Each column is appended to a variable representing its identity: GENERATED ALWAYS AS IDENTITY, IDENTITY (1,1) 
    Auto Increment --> Starting from 1 and incrementing 1-1 in each record. Generally used in columns with primary key feature.

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
Why we use stored procedure here: If it was clear which city we would use more often, it would not be necessary, but if there is more than one city name, it would be more correct to use @City. The stored procedure here shows us that the column named City is used very often

Question : When defining the table, we already define the City variable as nvarchar. What is the reason for assigning a character limit here?

Index
--> is used to collect variables from frequently asked questions or frequently used variables together
    CREATE INDEX idx_lastname
    ON Persons (LastName); --> here different records can be added by increasing the number of tables.
    
    It will be two different operations, but it is much more practical, because the computer would have to search the entire database otherwise
    
    ![image](https://github.com/mert10unal/SQL-Notes/assets/120198895/5076b02b-96c9-401c-a734-bd4d59d79a35)

Clustered Index
--> physical retention and storage of data
--> the selected column should be the most used and changed the least --> if it is changed frequently, the physical order also changes and it is a waste of time
CREATE CLUSTERED INDEX IX_IndexName ON TableName (Column1);

Non-Clustered Index
--> Logical sorting. Such as this number range on this page
--> CREATE NONCLUSTERED INDEX IX_IndexName ON TableName (Column1);

Unique Index
--> primary key and unique constraints
--> can be added more than once

Filtered Index
--> unlike the normal created index, a condition is filtered, i.e. the index created with the where command is restricted.
CREATE NONCLUSTERED INDEX IX_IndexName ON TableName (Column1) WHERE ...;

Composite Index
CREATE INDEX [indexadi] ON [dbo].[tabloadi] ([columnadi1] ASC/DESC,[columnadi2] ASC/DESC )

Covered Index
CREATE NONCLUSTERED INDEX IX_IndexName ON TableName (Column1) INCLUDE (Column2, Column3);


* Unique-primary key constraints, frequently used columns

Truncate :  Tablonun verileriyle beraber geçmişi de silinir. Tabloda 10 tane veri varsa bu veriler silinir ve yeni veriler eklenince id 1 olur.
delete : Tablonun verileri silinir. Tabloda 10 kayıt varsa silinen veriden sonra eklenen değerin idsi 11 olur.

__________________________________________________________________________________________________________________________________________

Nesne-Class Nedir ?
Class'lar, nesnelerin nasıl oluşturulacağını ve nasıl davranacaklarını belirleyen bir dizi alan ve yöntem içerir. Alanlar, nesnenin durumunu temsil eden veri elemanlarıdır, yöntemler ise nesnenin davranışını tanımlar. Nesneler ise fonksiyonlar ve sınıf yapılarına göre içine farklı değerler alabilir. Örneğin araba classının içinde renk ve marka belirten iki fonksiyon olsun. Bu fonksiyonlar üzerinden markası Audi, rengi ise gri olan bir nesne tanımlanabilir.

Ctor Nedir ?
- Bir sınıf oluşturulduğunda otomatik olarak getirilen bir yapıdır. Ana classtan ayıran şey bir dönüş tipinin olmamasıdır fakat isimleri aynı olmalıdır. Ctorlar değer döndürmez. Bir ctorun avantajı, bir sınıfın nesnesi oluşturulduğunda çağrılmasıdır. Alanlar (Column Field) için başlangıç değerlerini ayarlamak için kullanılabilir (nesnenin bir değişkenine değer atama)

Inheritance
- Bir sınıfın başka sınıfın attributelerini yani özelliklerini miras edebilmesi olayıdır. Çok sık kullanırız çünkü hem daha az kod yazmış oluruz hem de ana classa bağlı olarak bir sürü sub-class oluşturabiliriz. Örneğin her aracın rengi ve tekeri vardır. Bu özellikler ana class’ta tanımlandıktan sonra bir daha tanımlanırsa kod uzar. Bunun yerine inheritance yöntemiyle bunu sağlayabiliriz
- Class B : variable type A

Polymorphism
- Esneklik ve kullanışlılık
- Araba classının farklı markalarda sub-classları olsun ve araba classının da Horsepower adında bir özelliği olsun. Bu özellik tüm arabalarda vardır fakat fakat içerdiği değer her sub-classa göre farklılık gösterir. Veya horsepower üzerinden işlem yapan bir fonksiyonumuz olsun. Bu fonksiyonda horsepower özelliğinin her subclassa göre farklı değer döndürmesi de polymorphisme örnek gösterilebilir.

Encapsulation
- 

