
# Functional Dependency

Bir işlevsel bağımlılık ```X -> Y``` şeklinde gösterilir. Burada X sol tarafı, Y ise sağ tarafı temsil eder. X nitelik kümesinin değerleri, Y nitelik kümesinin değerlerini belirler. Y nitelik kümesinin değerleri, X nitelik kümesinin değerlerini belirlemez. X’in değerleri değiştiğinde Y’nin değerleri de değişebilir ancak Y’nin değerleri değiştiğinde, X’nin değerleri değişmez.

# Süper anahtar ve anahtar farkı

Süper anahtar, bir ilişkideki diğer tüm nitelikleri belirleyebilen bir nitelik kümesidir. Örneğin, ```R(A,B,C)``` ilişkisinde ```A -> B ve B -> C``` işlevsel bağımlılıkları varsa, A bir süper anahtardır çünkü A hem B’yi hem de C’yi belirler.

Anahtar ise bir ilişkideki diğer tüm nitelikleri belirleyebilen en küçük süper anahtardır. Örneğin, ```R(A,B,C)``` ilişkisinde ```A -> B ve B -> C``` işlevsel bağımlılıkları varsa, A bir anahtardır çünkü A hem B’yi hem de C’yi belirler ve A’dan daha küçük bir süper anahtar yoktur.

Dolayısıyla, her anahtar aynı zamanda bir süper anahtardır ancak her süper anahtar bir anahtar değildir. Örneğin, ```R(A,B,C)``` ilişkisinde ```A -> B ve B -> C``` işlevsel bağımlılıkları varsa, AB de bir süper anahtardır çünkü AB hem B’yi hem de C’yi belirler. Ancak, AB bir anahtar değildir çünkü AB’den daha küçük bir süper anahtar (A) vardır.

# Nontrivial

Nontrivial (önemsiz olmayan) işlevsel bağımlılık, sol tarafın sağ tarafın bir parçası (alt kümesi) olmadığı bir işlevsel bağımlılıktır. 

Örneğin, ```A -> B``` bir nontrivial işlevsel bağımlılıktır çünkü A (sol taraf), B (sağ taraf) 'nin bir parçası (alt kümesi) değildir. Ancak, ```AB -> B``` trivial (önemsiz) bir işlevsel bağımlılıktır çünkü AB, B’nin bir alt kümesidir.

Bu sorunun çözümünde verilen dört işlevsel bağımlılık ```(AB -> C, BC -> D, CD -> A ve AD -> B)``` ve bu işlevsel bağımlılıklardan türetilen sekiz işlevsel bağımlılık ```(AB -> D, AD -> C, BC -> A, CD -> B, ABC -> D, ABD -> C, ACD -> B ve BCD -> A)``` olmak üzere toplam 12 adet nontrivial işlevsel bağımlılık bulunmaktadır.

Ayrıca, bu ilişkinin anahtarları AB, AD, BC ve CD’dir. Bu nedenle, sol tarafında bu anahtarların biri olmayan herhangi bir işlevsel bağımlılık BCNF ihlalidir. Ancak, verilen FD’lerin hepsinde sol taraf bir anahtar olduğu için BCNF ihlali yoktur.

#

BCNF (Boyce-Codd Normal Form) ve 3NF (Third Normal Form) her ikisi de veritabanı tasarımı yöntemleridir. Her ikisi de veritabanındaki tekrarları azaltmayı ve veri tutarlılığını sağlamayı amaçlar.

# 3NF

Örneğin, R(A,B,C) ilişkisinde ```A -> B ve B -> C``` işlevsel bağımlılıkları var. Bu işlevsel bağımlılıklardan yola çıkarak A’nın bir süper anahtar olduğunu söyleyebiliriz çünkü ```A -> B -> C``` işlevsel bağımlılıklarından yola çıkarak A’nın hem B’yi hem de C’yi belirlediğini görebiliriz. Ayrıca, A, en küçük süper anahtar olduğu için aynı zamanda bir anahtar niteliğidir.

3NF kurallarına göre, bir ilişkinin her işlevsel bağımlılığında **sol tarafın bir süper anahtar olması gerekir**. Bu örnekteki ```A -> B``` işlevsel bağımlılığında sol taraf (A) bir süper anahtardır.

Ancak, BCNF kurallarına göre, bir ilişkinin her işlevsel bağımlılığında sol tarafın bir süper anahtar olması gerekir. Bu örnekteki ```B -> C``` işlevsel bağımlılığında, sol taraf (B) birincil anahtar değildir. Dolayısıyla bu ilişki BCNF’ye uymaz.


# BCNF 

Bu ilişkiyi BCNF’ye uygun hale getirmek için ayrıştırma yapmamız gerekir. Ayrıştırma işlemi, bir ilişkiyi birden fazla ilişkiye bölmektir. Bu işlemi yaparken, her bir alt ilişkinin BCNF’ye uygun olmasına dikkat ederiz.

Örneğimizdeki ```R(A,B,C)``` ilişkisini BCNF’ye uygun hale getirmek için ```B -> C``` işlevsel bağımlılığını ele alırız çünkü bu işlevsel bağımlılık BCNF’yi ihlal etmektedir. Bu işlevsel bağımlılığı kullanarak ```R1(B,C)``` ve ```R2(A,B)``` ilişkilerini oluştururuz.

```R1(B,C)``` ilişkisinde ```B -> C``` işlevsel bağımlılığı vardır ve sol taraf (B) bir süper anahtardır. Dolayısıyla bu ilişki BCNF’ye uyar.

```R2(A,B)``` ilişkisinde ```A -> B``` işlevsel bağımlılığı vardır ve sol taraf (A) bir süper anahtardır. Dolayısıyla bu ilişki de BCNF’ye uyar.

Sonuç olarak, ```R(A,B,C)``` ilişkisini ```R1(B,C)``` ve ```R2(A,B)``` ilişkilerine ayrıştırdığımızda her iki ilişki de BCNF’ye uygun hale gelir.
