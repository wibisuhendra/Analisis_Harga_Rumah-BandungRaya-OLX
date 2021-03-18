# Analisis_Harga_Rumah-BandungRaya-OLX
Melakukan data gathering menggunakan selenium dan beautiful soup, melakukan data cleansing, kemudian menganalisis serta membangun model berdasarkan data-data tersebut.

Data yang digunakan pada analisis ini adalah data yang diambil dari aplikasi web OLX dengan filter Rumah dijual di Kota Bandung. Data diambil menggunakan library bahasa pemrograman python yaitu beautifulsoup dan selenium. Selenium digunakan untuk melakukan interaksi dengan ajax yang ada pada web tersebut, dimana pada OLX terdapat tombol ‘muat lainnya’ untuk memperoleh item yang lebih banyak sehingga dibutuhkan interaksi terhadap tombol tersebut. 


Kemudian ditemukan bahwa pada OLX hanya dapat menampilkan 1000 item dalam satu halaman, sehingga data dibagi lagi menjadi beberapa filter berdasarkan harga, yaitu:
•	price_max_250000000',
•	price_between_250000000_to_400000000',
•	price_between_400000000_to_500000000',
•	price_between_500000000_to_650000000',
•	price_between_650000000_to_750000000',
•	price_between_750000000_to_950000000',
•	price_between_950000000_to_1500000000',
•	price_between_1500000000_to_3000000000',
•	price_between_3000000000_to_5000000000',
•	price_min_5000000000'
sehingga diperoleh 8597 item. Kemudian item-item tersebut diambil masing-masing url yang menuju halaman produknya menggunakan beautifulsoup, hal ini bertujuan untuk memperoleh data yang lebih lengkap karena apabila hanya mengambil data dari itembox saja hanya akan memperoleh data seperti yang ditampilkan dibawah. 



Link-link tersebut kemudian dibuka menggunakan urlopen, dan beautifulsoup untuk memperoleh data-data sebagai berikut:
•	'ID':ID Iklan,
•	'title': Judul Iklan,
•	'bedroom': Jumlah Kamar,  
•	'bathroom': Jumlah Kamar Mandi, 
•	'landsqr': Luas Tanah, 
•	'buildingsqr': Luas Bangunan, 
•	'cert': Sertifikat,
•	'loc': Lokasi1,
•	'location': Lokasi2, 
•	‘floor': Lantai,
•	‘postTime': Waktu iklan dipasang,
•	‘numOfFac': jumlah fasilitas, 
•	‘fac': fasilitas,
•	‘desc': deskripsi iklan,
•	‘price': harga
Data yang diperoleh berjumlah 8304, jumlah tidak sama dengan url yang ada dikarenakan beberapa iklan sudah dihapus oleh pemiliki iklan. 


Terdapat cukup banyak nilai null pada data tersebut hal ini disebabkan karena pemilik iklan yang tiadk mencantumkan data secara lengkap, sehingga beberapa data tersebut dihapuskan, selain itu terdapat beberapa iklan dengan data yang sama (data ganda), data anomali seperti luas tanah 900000m2, jumlah lantai 999 lantai, hal ini kemungkinan diakibatkan pemilik iklan yang mengisi iklan secara asal, selain itu juga terdapat data yang merupakan apartemen sehingga memiliki spesifikasi yang berbeda. Untuk menangani permasalah tersebut data-data tersebut dihapus, sehingga jumlah data yang terakhir ada 7107 baris, proses ini dilakukan menggunakan ms excel dan jupyter notebook. 
Untuk melakukan training dan membuat model maka atribut yang digunakan adalah bedroom, bathroom, landsqr, buildingsqr, cert, location, floor, numOfFac, dan price, dimana price adalah variabel dependennya. Kemudian data-data tersebut diambil untuk proses feature engineering untuk selanjutnya dibuat model berdasarkan data-data tersebut. Selain itu juga dilakukan analisis korelasi serta analisis harga rumah terhadap lokasi rumah tersebut


Dalam proses Feature Engineering dilakukan dua pekerjaan, yang pertama adalah one hot encoding terhadap data kategori, yaitu location dan cert, dan yang kedua adalah feature selection dimana kedua pekerjaan ini dilakukan untuk memperoleh model yang lebih baik. One hot encoding menambahkan jumlah atribut menjadi 73 atribut total. Proses feature selection dilakukan menggunakan Lasso regression dengan parameter alpha = 0.005,  dan random_state = 0, dimana hasilnya adalah semua atribut dapat digunakan. Sehingga tidak ada atribut yang digunakan pada proses training model regresi. 



