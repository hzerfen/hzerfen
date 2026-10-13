# Tek Sayfalık Tekrar Kartı: Operatörler, if/switch, Döngüler (C stili)

## 1) Operatörler
- Aritmetik: `+ - * / %`. **Tam sayı bölmesi küsuratı atar:** `7/2 = 3`, `7%2 = 1`, `7/2.0 = 3.5`.
- Atama: `= += -= *= /= %=` → `x += 3` ile `x = x + 3` aynıdır.
- Artırma: `i++` (önce kullan, sonra artır), `++i` (önce artır, sonra kullan).
  `int a = 5; int b = a++;` → b=5, a=6. `int b = ++a;` → b=6, a=6.
- Karşılaştırma: `== != < > <= >=` → sonuç 1 (doğru) ya da 0 (yanlış).
- Mantıksal: `&&` (ve), `||` (veya), `!` (değil).
  Kısa devre: `&&`'de sol taraf yanlışsa sağ taraf hiç çalışmaz; `||`'de sol doğruysa sağ çalışmaz.
- Öncelik (yüksek→düşük): `! ++ --` → `* / %` → `+ -` → `< > <= >=` → `== !=` → `&&` → `||` → `=`
- **Klasik tuzak:** `if (x = 5)` atama yapar, hep doğrudur. Karşılaştırma için `==` yaz.
- C'de **0 yanlış, sıfırdan farklı her değer doğrudur.**

## 2) Koşullar
```c
if (not >= 90) printf("AA");
else if (not >= 80) printf("BA");
else printf("Kaldi");
```
- Zincirde ilk doğru olan çalışır, gerisine bakılmaz.
- `if` satırının sonuna `;` koyma: `if (x > 0);` gövdeyi boşa çıkarır.
- Tek satırdan fazla ifade varsa `{ }` şart.
- Üçlü: `sonuc = (a > b) ? a : b;`

```c
switch (gun) {
    case 1: printf("Pzt"); break;
    case 2: printf("Sal"); break;
    default: printf("Diger");
}
```
- `switch` sadece tam sayı / `char` ile çalışır (float, string olmaz).
- **`break` unutulursa sonraki case'lere düşer (fall-through).**
- `case` değerleri sabit olmalı, `default` isteğe bağlı.

## 3) Döngüler
| Döngü | Ne zaman | Not |
|---|---|---|
| `for (i=0; i<n; i++)` | Tekrar sayısı belli | başlangıç; koşul; artış |
| `while (koşul)` | Sayı belli değil | Koşul **önce** kontrol edilir, hiç çalışmayabilir |
| `do { } while (koşul);` | En az 1 kez çalışmalı | Koşul **sonda**, `;` unutma |

- `break;` döngüyü tamamen bitirir. `continue;` o turu atlar, sonraki tura geçer.
- Sonsuz döngü: `for(;;)` ya da `while(1)`.
- `for (i=0; i<5; i++)` → i = 0,1,2,3,4 (5 tur, 5 yazılmaz). Döngü bitince `i = 5`.
- İç içe döngüde toplam tur = dış × iç.
- Toplam / sayaç: döngüden **önce** `toplam = 0;` yap.

Örnek (1'den n'ye toplam):
```c
int toplam = 0;
for (int i = 1; i <= n; i++) toplam += i;
```

Çift sayıları yaz:
```c
for (i = 1; i <= 10; i++) {
    if (i % 2 != 0) continue;
    printf("%d ", i);   // 2 4 6 8 10
}
```

## 4) Sınav Tuzakları (hızlı kontrol)
1. `=` ile `==` karışıklığı.
2. Tam sayı bölmesi: `1/2` = 0.
3. `i++` / `++i` farkı ifade içinde.
4. `switch`'te `break` yok → fall-through.
5. `if(...);` ve `for(...);` sonundaki gereksiz noktalı virgül.
6. `<` ile `<=` farkı → tur sayısı bir kayar.
7. `do-while` en az bir kez çalışır, `while` hiç çalışmayabilir.
8. `&&` / `||` kısa devre yüzünden yan etkili ifade (`i++`) atlanabilir.
