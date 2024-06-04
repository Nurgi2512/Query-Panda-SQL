# Query-Panda-SQL
Tutorial Bagaimana Cara Melakukan Query Menggunakan Pandasql
Contoh: <br>
Bagaimana melakukan query untuk mendapatkan kota-kota dari worldcity yang merupakan:
- berada di antara 33 - 40 'latitude'
- berada di antara 100 - 140 'longitude'
- merupakan kota 'primary' pada kolom 'capital'
- memiliki populasi lebih dari 20 juta

  ```Python
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
