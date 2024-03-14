##  Code.c
```sh
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_LENGTH 2024
#define MIN_LENGTH 1945

void lessThanRequired (int* lengthOfText){
    printf("The length of your text is less than specified, please update your text\n");
    *lengthOfText = MIN_LENGTH;
}

void equalThanRequired (int* lengthOfText){
    printf("Thank you, Your text length is correct\n");
}

void moreThanRequired (int* lengthOfText){
    printf("Your text is to long, please reduce the text\n");
    *lengthOfText = MIN_LENGTH;
}

int checkLenghtRequirement(char* text){
    int length = strlen(text);
    if (length < MIN_LENGTH)
        return 0;
    else if (length == MIN_LENGTH)
        return 1;
    else
        return 2;
}

int main() {
    int lengthOfText, selectOption;
    FILE *fptr = NULL;
    char text[MAX_LENGTH];

    fptr = fopen("file.txt", "r");

    if(fptr == NULL){
        printf("Error");
        exit(1);
    }

    fgets(text, MAX_LENGTH, fptr);

    fclose(fptr);

    selectOption = checkLenghtRequirement(text);

       // TODO
    // Pada fungsi checkLenghtRequirement akan mengembalikan sebuah angka
    // angka tersebut digunakan untuk memilih secara otomatis salah satu fungsi yang harus diisi
    // jika fungsi checkLenghtRequirement() mengembalikan nilai 0, maka
    //      tampilkan - > The length of your text is less than specified, please update your text
    //      update nilai lengthOfText ke minimum requirement melalui pointer menggunakan operasi aritmatika

    // jika fungsi checkLenghtRequirement() mengembalikan nilai 1, maka
    //      tampilkan - > Thank you, Your text length is correct

    // jika fungsi checkLenghtRequirement() mengembalikan nilai 2, maka
    //      tampilkan - > Your text is to long, please reduce the text
    //      update nilai lengthOfText ke minimum requirement melalui pointer menggunakan operasi aritmatika
    //
    // Catatan :
    //      - tidak diperkenankan menggunakan if atau switch dalam perpindahan fungsi
    //        sesuai dengan requirement diatas.
    //      - baris kode tidak lebih dari 100 (include comment ini)
    //      - tidak diperkenankan mengganti yang tertera pada starter code dalam alasan apapun

    void (*functions[3])(int*) = {lessThanRequired, equalThanRequired, moreThanRequired};

    lengthOfText = strlen(text);
    functions[selectOption](&lengthOfText);

    printf("\nThe Length is updated to %d", lengthOfText);

    return 0;
}
```

### Penjelasan

1. `#include <stdio.h>:` Mengimpor file header standar input-output dalam C.
2. `#include <stdlib.h>:` Mengimpor file header standar library dalam C.
3. `#include <string.h>:` Mengimpor file header untuk fungsi string dalam C.
4. `#define MAX_LENGTH 2024:` Mendefinisikan konstanta `MAX_LENGTH` dengan nilai 2024.
5. `#define MIN_LENGTH 1945:` Mendefinisikan konstanta `MIN_LENGTH` dengan nilai 1945.
Fungsi `lessThanRequired`, `equalThanRequired`, dan `moreThanRequired` adalah fungsi yang akan dipanggil berdasarkan panjang teks. Mereka menerima pointer ke `lengthOfText` dan memodifikasi nilai tersebut jika perlu.
6. `void lessThanRequired (int* lengthOfText):` Mendefinisikan fungsi `lessThanRequired` yang menerima pointer ke integer.
7. `printf("The length of your text is less than specified, please update your text\n");`: Menampilkan pesan bahwa panjang teks kurang dari yang ditentukan.
8. `lengthOfText = MIN_LENGTH;`: Mengubah nilai yang ditunjuk oleh `lengthOfText` menjadi `MIN_LENGTH`.
9. `void equalThanRequired (int* lengthOfText)`: Mendefinisikan fungsi `equalThanRequired` yang menerima pointer ke integer.
10. `printf("Thank you, Your text length is correct\n");`: Menampilkan pesan bahwa panjang teks sudah benar.
11. `void moreThanRequired (int* lengthOfText)`: Mendefinisikan fungsi moreThanRequired yang menerima pointer ke integer.
12. `printf("Your text is to long, please reduce the text\n");`: Menampilkan pesan bahwa teks terlalu panjang.
13. `*lengthOfText = MIN_LENGTH;`: Mengubah nilai yang ditunjuk oleh `lengthOfText` menjadi `MIN_LENGTH`.
Fungsi `checkLenghtRequirement` memeriksa panjang teks dan mengembalikan 0, 1, atau 2 tergantung pada panjang teks tersebut.
14. `int checkLenghtRequirement(char* text)`: Mendefinisikan fungsi `checkLenghtRequirement`yang menerima pointer ke char (string)
15. `int length = strlen(text);`: Menghitung panjang string menggunakan fungsi `strlen` dan menyimpannya dalam variabel `length`.
16. `if (length < MIN_LENGTH) return 0;`: Jika panjang kurang dari `MIN_LENGTH`, fungsi mengembalikan 0.
17. `else if (length == MIN_LENGTH) return 1;` Jika panjang sama dengan `MIN_LENGTH`, fungsi mengembalikan 1.
18. `else return 2;` Jika panjang lebih dari `MIN_LENGTH`, fungsi mengembalikan 2.
Fungsi main adalah titik masuk program. Di dalamnya, program membuka file teks, membaca teksnya, memeriksa panjang teks, dan memanggil fungsi yang sesuai.
19. `int main()`: Mendefinisikan fungsi `main`.
20. `int lengthOfText, selectOption;` Mendeklarasikan dua variabel integer, `lengthOfText` dan `selectOption`
21. `FILE *fptr = NULL;` Mendeklarasikan pointer ke `FILE` dan menginisialisasinya dengan `NULL`.
22. `char text[MAX_LENGTH];`: Mendeklarasikan array karakter text dengan ukuran `MAX_LENGTH`.
23. `fptr = fopen("file.txt", "r");`: Membuka file bernama “file.txt” untuk dibaca dan menyimpan pointer ke file tersebut dalam `fptr`.
24. `if(fptr == NULL){ printf("Error"); exit(1); }`: Jika file tidak dapat dibuka (misalnya, file tidak ada), program mencetak “Error” dan keluar dengan status 1.
25. `fgets(text, MAX_LENGTH, fptr);` Membaca teks dari file dan menyimpannya dalam array `text`.
26. `fclose(fptr);`: Menutup file.
27. `selectOption = checkLenghtRequirement(text);`: Memeriksa panjang teks dan menyimpan hasilnya dalam `selectOption`.
28. `void (*functions[3])(int*) = {lessThanRequired, equalThanRequired, moreThanRequired};`: Mendeklarasikan array dari pointer ke fungsi dan menginisialisasikannya dengan tiga fungsi yang telah didefinisikan sebelumnya.
29. `lengthOfText = strlen(text);`: Menghitung panjang teks dan menyimpannya dalam `lengthOfText`
30. `functionsselectOption;` Memanggil fungsi yang sesuai berdasarkan selectOption dan memberikan alamat dari `lengthOfText` sebagai argumen.
31. `printf("\nThe Length is updated to %d", lengthOfText);`: Mencetak panjang teks yang telah diperbarui.
32. `return 0;`: Mengakhiri fungsi main dan mengembalikan 0, menandakan bahwa program telah berjalan dengan sukses.

## Output

Program ini membaca teks dari file bernama file.txt dan memeriksa panjang teks tersebut. Berikut adalah penjelasan output yang dihasilkan:

- Jika panjang teks kurang dari `MIN_LENGTH `(1945), program akan mencetak pesan “The length of your text is less than specified, please update your text” dan mengubah `lengthOfText` menjadi `MIN_LENGTH`.
- Jika panjang teks sama dengan `MIN_LENGTH`, program akan mencetak pesan “Thank you, Your text length is correct”.
- Jika panjang teks lebih dari `MIN_LENGTH`, program akan mencetak pesan “Your text is too long, please reduce the text” dan mengubah `lengthOfText` menjadi `MIN_LENGTH`.
  
Setelah itu, program akan mencetak “The Length is updated to” diikuti dengan nilai `lengthOfText` yang telah diperbarui.

Sebagai contoh, jika file `file.txt` berisi teks dengan panjang 2000, output program akan seperti ini:
```sh
Your text is too long, please reduce the text
The Length is updated to 1945
```
![alt text](https://github.com/idilhaq05/project/blob/main/Photo/Screenshot%202024-03-14%20085204.png?raw=true)

![alt text](https://github.com/idilhaq05/project/blob/main/Photo/Screenshot%202024-03-14%20093516.png?raw=true)

![alt text](https://github.com/idilhaq05/project/blob/main/Photo/Screenshot%202024-03-14%20095236.png?raw=true)



## Cara Penggunaan

Untuk menjalankan kode ini, perlu untuk mengikuti langkah-langkah berikut:

1. Simpan kode: Pertama,  menyimpan kode ini ke dalam file dengan ekstensi `.c`. 
2. Siapkan file teks: Kode ini membaca teks dari file bernama `file.txt`. Pastikan file dengan nama tersebut di direktori yang sama dengan file kode . File ini harus berisi teks yang ingin diperiksa panjangnya.
3. Kompilasi: Anda perlu mengkompilasi kode menggunakan kompiler C. Jika Anda menggunakan GCC, kita bisa membuka terminal dan mengetikkan perintah berikut di direktori yang sama dengan file kode:
```sh
 gcc text_length_checker.c -o text_length_checker
```

Perintah ini akan mengkompilasi kode  dan menghasilkan file eksekusi bernama `text_length_checker`.

4. Jalankan program: Setelah berhasil mengkompilasi kode, kita bisa menjalankan program dengan mengetikkan perintah berikut di terminal:
```sh
./text_length_checker
```

Program akan membaca teks dari `file.txt`, memeriksa panjang teks, dan memanggil fungsi yang sesuai berdasarkan panjang teks tersebut.

## Cara Kerja Program

1. Membaca File: Program ini membuka dan membaca file teks dengan nama “file.txt”. Teks dari file tersebut disimpan dalam array karakter `text`.
2. Memeriksa Panjang Teks: Panjang teks yang dibaca dari file diperiksa menggunakan fungsi `checkLenghtRequirement`. Fungsi ini membandingkan panjang teks dengan `MIN_LENGTH` dan mengembalikan 0, 1, atau 2 tergantung pada hasil perbandingan tersebut.
3. Memilih Fungsi yang Sesuai: Program ini memiliki array functions yang berisi pointer ke tiga fungsi: `lessThanRequired`, `equalThanRequired`, dan `moreThanRequired`. Berdasarkan nilai yang dikembalikan oleh checkLenghtRequirement, salah satu dari tiga fungsi ini dipanggil.
- Jika `checkLenghtRequirement `mengembalikan 0 (panjang teks kurang dari `MIN_LENGTH`), fungsi `lessThanRequired `dipanggil. Fungsi ini mencetak pesan bahwa teks terlalu pendek dan mengubah `lengthOfText` menjadi `MIN_LENGTH`
- Jika `heckLenghtRequirement `mengembalikan 1 (panjang teks sama dengan `MIN_LENGTH`), fungsi `equalThanRequired `dipanggil. Fungsi ini mencetak pesan bahwa panjang teks sudah benar.
- Jika `checkLenghtRequirement` mengembalikan 2 (panjang teks lebih dari `MIN_LENGTH`), fungsi `moreThanRequired` dipanggil. Fungsi ini mencetak pesan bahwa teks terlalu panjang dan mengubah `lengthOfText` menjadi `MIN_LENGTH`
4. Menampilkan Panjang Teks yang Diperbarui: Setelah fungsi yang sesuai dipanggil, program mencetak “The Length is updated to” diikuti dengan nilai `lengthOfText` yang telah diperbarui.
