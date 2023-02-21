docker compose digunakan untuk mempermudah membuat container.
sifat docker compose adalah isolated per project, (semua perintah akan dijalankan/berfungsi di folder/project kita berada, ketika kita menjalankan di project/folder a maka folder b,c dan d tidak akan terpengaruh.)
secara default folder yang kita buat adalah nama dari project tersebut.

command / perintah:
- docker compose create : digunakan untuk membuat container secara otomatis (this).
- docker compose start : digunakan untuk menjalankan semua container, karena pada defaltnya tidak akan aktif otomatis (this).
- docker compose ps : digunakan untuk menampilkan container yang sedang aktif (this).
- docker compose stop : digunakan untuk menghentikan (stop) container yang sedang aktif.
- docker compose down : digunakan untuk menghapus container, secara otomatis network akan di hapus otomatis juga, (this).
- docker compose ls : digunakan untuk melihat semua project yang sedang aktif/berjalan.
- docker events : digunakan untuk melihat kejadian secara realtime container
- docker compose build : digunakan untuk membuat image dari docker compose



config didalam service yaml:
- services : dalam config docker compose, container disimpan dalam configurasi bernama services
- komentar : menggunakan hashtag (#)
- ports:
    - short sintaks "porthost:portcontainer" contoh 8080:80
    - long sintaks ditulis dalam bentuk object long array, target: (port didalam container), published: (target host), protocol: (tcp/udp), mode: host
- environment: digunakan untuk menambahkan nilai/value ke dalam container
- volumes: digunakan untuk menggunakan bind/volume
    - bind
    - short sintaks, SOURCE:TARGET:MODE, source adalah sumber dari host, target adalah destination di container, dan mode adalah permision
    - long sintaks, menggunakan nested array object, type: bind, source: (sumber host), target: (file/folder di container), read_only: (true/false)
    - volume
    - short sintaks, NAMAVOLUME:TARGETDATA
    - long sintaks, menggunakan nested array object, type: volume, source: (nama volume), target: (file/folder di container), read_only: (true/false)
- network: secara otomatis akan membuat network per project, maka setiap container akan terhubung satu sama lain, tetapi kita bisa membuat dan menggunakannya
- depeend-on: digunakan untuk mengurutkan container mana yang akan dibuat terlebih dahulu.
- restart: secara default ketika kontainer mati maka container tidak akan running lagi, kita bisa mengaktifkan container tersebut dengan perintah restart
    - no: (default)
    - always: (akan selalu restart jika container berhenti)
    - on-failure: (akan restart ketika terjadi error dengan indikasi exit)
    - unless-stoped: (selalu restart container sampai container dimatikan manual)
- deploy: digunakan untuk mengatur resource limit seperti cpu, ram.
    - reservation (limit-at atau garansi minimal yang didapat)
    - limits (max-limit atau batas maksimal resource yang digunakan)
- build: kita bisa membuild file dockerfile langsung menggunakan docker compose, detailnya cek folde build
- healthcheck: semua perintah healthcheck sama dengan di docker file
- merge file compose: docker compose -f fileutama.yaml -f fileextend.yaml create, kelebihannya kita tidak perlu memuat image terus menerus, cukup 1x


config diluar services yaml:
- volume, membuat volume
    volumes:
        volume-mongo1:
        name: volume-mongo1
- network, membuat network secara manual
    networks:
    network_example:
        name: network_example
        driver: bridge