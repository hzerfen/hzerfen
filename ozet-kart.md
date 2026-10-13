# Tek Sayfalık Tekrar Kartı: Operatörler, if/switch, Döngüler (Java)
Kaynak: Computer Programming I (Operators, Control Structures, Loop Structures) slaytları.

## 1) Operatörler
- Atama `=`: önce sağ taraf hesaplanır, sonra sola atanır. `x = x + 1;` (x=2 ise x=3).
- Aritmetik: `+ - * / %`. Tam sayı bölmesi küsuratı atar: `7/2 = 3`, `7%2 = 1`.
- Birleşik atama: `x += c` → `x = x + c`, `x -= c` → `x = x - c`. `=+` ve `=-` diye yazılmaz.
- Artırma/azaltma:
  - `y = x++;` önce kullan, sonra artır. x=5 → **y=5, x=6**
  - `z = ++x;` önce artır, sonra kullan. x=5 → **z=6, x=6**
  - `i=3` iken `println(++i)` → 4, `println(i++)` → 4 yazar, sonra i=5.
- Karşılaştırma: `== != > < >= <=` ve `!` (değil). Sonuç `true`/`false` (boolean).
- Üçlü (ternary): `max = (a > b) ? a : b;` koşul doğruysa ilk, yanlışsa ikinci ifade.
- Mantıksal: `&&` (ve), `||` (veya). Tek `&` ve `|` bit düzeyindedir.

| && | true | false |   | \|\| | true | false |
|---|---|---|---|---|---|---|
| **true** | true | false | | **true** | true | true |
| **false** | false | false | | **false** | true | false |

- Bit operatörleri: `&` AND, `|` OR, `^` XOR, `~` NOT. Örnek: a=0011 1100, b=0000 1101 →
  `a&b`=0000 1100, `a|b`=0011 1101, `a^b`=0011 0001, `~a`=1100 0011.
- Kaydırma: `<<` sola, `>>` işaretli sağa (işaret biti korunur), `>>>` işaretsiz sağa (boşluğa 0 gelir).
  `a=0011 1100 (60)` → `a << 2` = 240, `a >> 2` = 15.
  Negatiflerde fark: `1111 1110 >> 1` = `1111 1111` (-1), `>>> 1` = `0111 1111` (127).
- **Kaydırma değişkeni değiştirmez:** `i=2; i<<1;` → i hâlâ 2. `j = i<<1;` → j=4.
- Negatif sayı = pozitifin bitlerini ters çevir + 1 (2'ye tümleyen).
- Öncelik (yüksek→düşük): sonek `expr++ expr--` → birli `++expr --expr +expr -expr ~ !` →
  `* / %` → `+ -` → kaydırma `<< >> >>>` → ilişkisel `< > <= >= instanceof` → eşitlik `== !=` →
  `&` → `^` → `|` → `&&` → `||` → `?:` → atama `= += -= ...`

## 2) if / else if / else
```java
if (i >= 5) { System.out.println("Large"); }
else if (i <= 2) { System.out.println("Small"); }
else { System.out.println("Average"); }
```
- Koşul `true` ise blok çalışır. Zincirde **ilk doğru olan** çalışır, gerisi atlanır.
- `{ }` yoksa sadece **sonraki tek satır** koşulludur. Hep `{ }` kullan.
- `if (koşul);` → `;` boş ifade olur, if etkisiz kalır. Yapma.
- `if`, `else if`, `else` tek bir bloktur; arasına başka ifade (`k++;`) koyarsan **derleme hatası**.
- Birden fazla ayrı `if` yerine `else if` kullan (biri doğruysa diğerleri olamaz).

## 3) switch
```java
switch (month) {
    case 1: monthString = "January"; break;
    case 2: monthString = "February"; break;
    default: monthString = "Invalid month"; break;
}
```
- Değişkenin değerine göre case seçer. **Sadece eşitlik** kontrol eder; `if` her koşulu kontrol eder (daha esnek).
- **`break` yoksa fall-through:** eşleşen case'ten sonraki tüm case'ler çalışır. month=8 iken break'siz: August, September, ..., December.
- İstisna: `case 1: case 3: case 5: ... numDays = 31; break;` (birden çok case aynı işi yapar).
- Artık yıl: `((year % 4 == 0) && !(year % 100 == 0)) || (year % 400 == 0)` → 2000 için Şubat 29 gün.

## 4) Döngüler
```java
while (koşul) { ... }                 // koşul önce kontrol, hiç çalışmayabilir
do { ... } while (koşul);             // koşul sonda, EN AZ 1 kez çalışır, ; unutma
for (int i = 1; i < 11; i++) { ... }  // başlangıç; bitiş koşulu; artış
for (int item : numbers) { ... }      // for-each: dizi/koleksiyon elemanları
```
- `for` içinde başlatma bir kez çalışır, artış her turdan sonra çalışır, koşul `false` olunca biter.
- Birden çok değişken: `for (int i=1, j=10; i<j; i++, j--)`.
- Sonsuz döngü: `while (true) { }` veya `for ( ; ; ) { }`.
- Sayı belliyse `for`, belli değilse `while` tercih et. Toplam için döngüden önce `int sum = 0;`.
- Döngü kontrol ifadeleri:
  - `break;` içinde bulunduğu en içteki döngü/switch'i bitirir. Etiketli: `break dis;` dıştaki etiketli döngüyü bitirir (Java'da `goto` yok).
  - `continue;` sadece o turu atlar, sonraki tura geçer. (`if (i==5) continue;` → 5 yazılmaz.)
  - `return;` metottan çıkar.
- Tur sayıları:
  - `for(int i=0;i<10;i++)` → **10**
  - `for(int i=0;i<1;i++)` → **1**
  - `for(int i=0;i==0;i++)` → **1**
  - `for(int i=5;i<=1;i++)` → **0** (hiç çalışmaz)

## 5) Sınav Tuzakları
1. `x++` ile `++x` farkı (atama içinde).
2. Tam sayı bölmesi: `1/2 = 0`.
3. `&&`/`||` (boolean) ile `&`/`|` (bit) karışıklığı.
4. `>>` işareti korur, `>>>` 0 doldurur. Kaydırma değişkeni değiştirmez.
5. switch'te `break` unutmak → fall-through.
6. `if(...);` ve `for(...);` sonundaki `;`.
7. `<` ile `<=` farkı, tur sayısını kaydırır.
8. `do-while` en az bir kez çalışır.
9. Aynı isimli değişkeni `for` içinde tekrar tanımlama (`int i; for(int i=...)` derleme hatası).
