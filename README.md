# Query-Panda-SQL
Tutorial Bagaimana Cara Melakukan Query Menggunakan Pandasql
Contoh: <br>
Bagaimana melakukan query untuk mendapatkan kota-kota dari worldcity yang merupakan:
- berada di antara 33 - 40 'latitude'
- berada di antara 100 - 140 'longitude'
- merupakan kota 'primary' pada kolom 'capital'
- memiliki populasi lebih dari 20 juta


``` sql
query = """
SELECT DISTINCT city  
FROM worldcity  
WHERE lat BETWEEN 33 AND 40  
AND lng BETWEEN 100 AND 140  
AND capital = 'primary'  
AND population > 20000000  
"""

sql_run(query)
```
## Temukan kota-kota dari worldcity yang memenuhi semua kondisi ini:
- populasi kota tersebut melebih populasi dari kota terbanyak penduduknya di negara Filipina. (Maksudnya: misalnya kota X adalah kota di Filipina yang paling banyak penduduknya. Kita mau daftar kota-kota yang jumlah penduduknya lebih besar dari kota X tersebut), DAN
- ada kota di Amerika Serikat (uscity) dengan nama kota yang sama dengan kota-kota pilihan

Keluarkan hanya nama kota-kota yang memenuhi 2 syarat di atas saja, tidak usah kolom-kolom lain.

##### NOTE: Hilangkan duplicate rows.
```sql
   query = '''
    SELECT DISTINCT w.city
    FROM worldcity w
    JOIN
    uscity u ON u.city = w.city
    WHERE w.population > (SELECT MAX(population) FROM worldcity WHERE country = 'Philippines')
    
'''

sql_run(query)
```

## Temukan kota-kota di Amerika Serikat (uscity) yang memenuhi semua kondisi berikut:
- memiliki nama 'city' yang tidak sama dengan 'state_name', dan juga
- memiliki populasi di atas rata-rata populasi kota-kota di 'county_name' Miami-Dade, dan juga
- terdiri dari dua atau lebih kata (contoh: Los Angeles, New York)

Output yang diharapkan hanya kolom 'city' saja, tidak usah kolom yang lain
```sql
    query = '''
    SELECT city
    FROM uscity
    WHERE city <> state_name
      AND population > (
        SELECT AVG(population)
        FROM uscity
        WHERE county_name = 'Miami-Dade'
      )
      AND city like "% %";
'''

sql_run(query)

```


