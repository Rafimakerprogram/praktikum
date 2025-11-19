Terminal Racer

## *Deskripsi Program*

Program ini merupakan game sederhana berbasis ASCII di console yang bertemakan permainan “racing” atau “endless runner”. Pemain mengontrol karakter *A* untuk menghindari obstacle *X* yang jatuh dari atas layar. Program menggunakan sistem level, scoring, collision detection, dan leaderboard yang tersimpan menggunakan file.

### *Fungsi Program*

* Menyediakan permainan ASCII racing yang interaktif.
* Menyimpan dan menampilkan skor pemain.
* Menjalankan mekanisme level dan obstacle secara otomatis.

### *Data yang Dikelola*

* *Posisi player*
* *Peta permainan (map)* berupa vector string
* *Score dan level*
* *Data leaderboard* (nama + skor) menggunakan file eksternal

### *Fitur Utama*

1. Menu utama (Play, Instructions, Leaderboard, Exit)
2. Kontrol real-time menggunakan keyboard (A, D, Q)
3. Map scrolling seperti endless runner
4. Obstacle acak yang muncul setiap frame
5. Sistem level otomatis berdasarkan skor
6. Perhitungan skor dengan multiplier
7. Collision detection untuk Game Over
8. Leaderboard tersimpan di file
9. ASCII display yang diperbarui setiap frame

### *Penggunaan struct dan fstream*

* Program menggunakan `struct Entry' untuk menyimpan:

  cpp
  struct Entry {
      string name;
      int score;
  };
  
* File leaderboard.txt dibaca dan ditulis menggunakan fstream:

  * Menambahkan skor baru
  * Membaca leaderboard
  * Menyimpan leaderboard terurut

### *Tujuan Program*

* Melatih pemahaman konsep dasar C++ seperti array, vector, struct, loop, random number, file handling, dan algoritma sorting.
* Memberikan simulasi game sederhana berbasis teks.

---

## *Algoritma yang Digunakan*

### *1. Algoritma Scrolling Map*

Algoritma ini membuat map bergerak dari atas ke bawah.

*Cara kerja:*

* Elemen baris ke-i diisi dengan baris ke-i - 1
* Baris paling atas diisi obstacle baru
* Player selalu ditempatkan di baris paling bawah

*Penggunaan dalam program:* menjaga efek “racing” agar obstacle terlihat jatuh.

---

### *2. Algoritma Random Obstacle Generation*

Setiap frame, obstacle muncul berdasarkan probabilitas tertentu (obstacleChance).

*Cara kerja:*

* Untuk setiap kolom:
  if (rand() % 100 < obstacleChance) → generate X
* Chance meningkat setiap naik level

*Penggunaan dalam program:* menciptakan obstacle yang membuat game lebih sulit.

---

### *3. Algoritma Sorting Leaderboard*

Leaderboard diurutkan berdasarkan skor tertinggi menggunakan fungsi sort().

*Cara kerja:*

* Mengurutkan vector Entry berdasarkan score secara descending
* Menggunakan lambda comparator:

  cpp
  sort(board.begin(), board.end(), [](Entry a, Entry b){
      return a.score > b.score;
  });
  

*Penggunaan dalam program:* memastikan leaderboard menampilkan skor tertinggi di posisi atas.

---

## *Potongan Kode Penting*

### *1. Scrolling Map*

cpp
for (int i = HEIGHT - 1; i > 0; i--)
    map[i] = map[i - 1];


### *2. Generate Obstacle Baru*

cpp
string newRow(WIDTH, EMPTY);
for (int i = 0; i < WIDTH; i++) {
    if (rand() % 100 < obstacleChance) newRow[i] = OBSTACLE;
}
map[0] = newRow;


### *3. Sorting Leaderboard*

cpp
sort(board.begin(), board.end(), [](Entry a, Entry b){
    return a.score > b.score;
});


### *4. Collision Detection*

cpp
if (map[HEIGHT - 1][playerPos] == OBSTACLE) {
    cout << "GAME OVER!\n";
    // save score & exit
}


---

## *Pembagian Tugas Anggota*

| Nama         | NPM     | Tugas                            |
| ------------ | ------- | -------------------------------- |
| Raffa        | NPM     | Gameplay, map scrolling, scoring |
| (Isi Nama 2) | (NPM 2) | Leaderboard & file handling      |
| (Isi Nama 3) | (NPM 3) | UI menu & instructions           |

(Silakan ganti sesuai kebutuhan kelompok)

---

## *Cara Menjalankan Program*

1. Install compiler C++ (g++ / MinGW / Visual Studio).
2. Compile program:

   sh
   g++ -o racing main.cpp
   
3. Jalankan:

   sh
   ./racing
   
4. Pastikan file leaderboard.txt ada (atau akan otomatis dibuat).

> Program hanya berjalan di Windows karena memakai conio.h dan windows.h.

---

## *Struktur Folder*

```
project-folder/
├── main.cpp
├── leaderboard.txt
└── README.md
