# Program Manajemen Pengiriman(Tubes Semester 1)
## 1. Deskripsi dan Spesifikasi Program
Program ini merupakan sebuah sistem manajemen pengiriman barang yang dibangun menggunakan bahasa pemrograman C. Berikut adalah beberapa komponen utama dalam program ini:

### Array dan Struktur Data

- Program menggunakan array dari struktur Pengiriman untuk menyimpan data pengiriman barang.
- Struktur **Pengiriman** memiliki beberapa atribut, seperti nama pengirim, tujuan pengiriman, berat barang, nama penerima, kode resi, harga, timestamp, dan status.

### Fungsi-fungsi

- **float hitungHarga(float berat):** Fungsi ini digunakan untuk menghitung harga pengiriman berdasarkan berat barang.
- **void newLine():** Prosedur ini digunakan untuk membersihkan buffer input.
- **void tampilkanKodeResi(struct Pengiriman data):** Prosedur ini menampilkan kode resi dari data pengiriman.
- **void tampilkanData(struct Pengiriman data):** Prosedur ini menampilkan seluruh informasi dari satu data pengiriman.
- **void cariData(struct Pengiriman data[], int jumlah_data, char kode_resi_cari[10]):** Prosedur ini mencari dan menampilkan data berdasarkan kode resi.
- **void tampilkanSemuaData(struct Pengiriman data[], int jumlah_data):** Prosedur ini menampilkan seluruh data pengiriman.
- **int compareTimestampAsc(const void a, const void b):** Fungsi pembanding untuk pengurutan ascending berdasarkan timestamp.
- **int compareTimestampDesc(const void a, const void b):** Fungsi pembanding untuk pengurutan descending berdasarkan timestamp.
- **void urutkanData(struct Pengiriman data[], int jumlah_data, int urutan):** Prosedur ini mengurutkan data berdasarkan tanggal pengiriman.
- **void simpanDataKeFileCSV(struct Pengiriman data[], int jumlah_data):** Prosedur ini menyimpan data pengiriman ke dalam file CSV.
- **void bacaDataDariFile(struct Pengiriman data[], int jumlah_data):** Prosedur ini membaca data pengiriman dari file CSV.


### Fungsi
- **int main():** Fungsi utama program yang mengandung logika menu, pengolahan data, dan interaksi dengan pengguna.
## 2. User Manual

### Menu Utama
Program memiliki enam menu utama:
- **Tambah Data Pengiriman:** Pengguna dapat memasukkan informasi pengiriman baru.
- **Cari Data Pengiriman:** Pengguna dapat mencari data berdasarkan kode resi.
- **Tampilkan Semua Data Pengiriman:** Menampilkan seluruh data pengiriman.
- **Urutkan Data Berdasarkan Tanggal:** Mengurutkan data berdasarkan tanggal pengiriman.
- **Edit Status Pengiriman:** Mengedit status pengiriman berdasarkan kode resi.
- **Keluar:** Keluar dari program.
### Penggunaan Menu
#### 1. Tambah Data Pengiriman
- Pengguna diminta memasukkan informasi pengiriman seperti nama pengirim, tujuan pengiriman, berat barang, dan nama penerima.
- Program secara otomatis menghasilkan kode resi, menghitung harga, dan menetapkan timestamp.
- Pengguna memilih status pengiriman (Ongoing atau Delivered).
#### 2. Cari Data Pengiriman
- Pengguna diminta memasukkan kode resi yang ingin dicari.
- Jika ditemukan, program akan menampilkan informasi pengiriman. Jika tidak, pesan bahwa data tidak ditemukan ditampilkan.
#### 3. Tampilkan Semua Data Pengiriman
- Menampilkan seluruh data pengiriman yang telah dimasukkan.
#### 4. Urutkan Data Berdasarkan Tanggal
- Pengguna diminta memilih urutan pengurutan (Ascending atau Descending) berdasarkan tanggal pengiriman.
- Program akan menampilkan data yang sudah diurutkan.
#### 5. Edit Status Pengiriman
- Pengguna diminta memasukkan kode resi yang ingin diedit statusnya.
- Jika data ditemukan, pengguna memilih status baru (Ongoing atau Delivered). Jika tidak, pesan bahwa data tidak ditemukan ditampilkan.
#### 6. Keluar
- Keluar dari program.
## 3. Code.c
```sh
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <time.h>

struct Pengiriman {
    char nama_pengirim[50];
    char tujuan_pengiriman[50];
    float berat_barang;
    char nama_penerima[50];
    char kode_resi[10];
    float harga;
    time_t timestamp;
    char status[20];
};

float hitungHarga(float berat) {
    const float harga_per_kg = 10.0;
    return berat * harga_per_kg;
}

void newLine() {
    int c;
    while ((c = getchar()) != '\n' && c != EOF);
}

void tampilkanKodeResi(struct Pengiriman data) {
    printf("Kode Resi        : %s\n", data.kode_resi);
}

void tampilkanData(struct Pengiriman data) {
    printf("Nama Pengirim   : %s\n", data.nama_pengirim);
    printf("Tujuan Pengiriman: %s\n", data.tujuan_pengiriman);
    printf("Berat Barang     : %.2f kg\n", data.berat_barang);
    printf("Nama Penerima    : %s\n", data.nama_penerima);
    printf("Kode Resi        : %s\n", data.kode_resi);
    printf("Harga            : Rp.%.2f\n", data.harga);

    char timestamp_str[20];
    strftime(timestamp_str, sizeof(timestamp_str), "%Y-%m-%d %H:%M:%S", localtime(&data.timestamp));
    printf("Timestamp        : %s\n", timestamp_str);

    printf("Status           : %s\n", data.status);

    printf("-----------------------------\n");
}

void cariData(struct Pengiriman data[], int jumlah_data, char kode_resi_cari[10]) {
    int ditemukan = 0;
    for (int i = 0; i < jumlah_data; i++) {
        if (strcmp(data[i].kode_resi, kode_resi_cari) == 0) {
            tampilkanData(data[i]);
            ditemukan = 1;
            break;
        }
    }

    if (!ditemukan) {
        printf("Data tidak ditemukan.\n");
    }
}

void tampilkanSemuaData(struct Pengiriman data[], int jumlah_data) {
    if (jumlah_data > 0) {
        printf("\nSemua Data Pengiriman:\n");
        for (int i = 0; i < jumlah_data; i++) {
            printf("Data ke-%d:\n", i + 1);
            tampilkanData(data[i]);
        }
    } else {
        printf("Tidak ada data yang diinput.\n");
    }
}

int compareTimestampAsc(const void *a, const void *b) {
    return ((struct Pengiriman *)a)->timestamp - ((struct Pengiriman *)b)->timestamp;
}

int compareTimestampDesc(const void *a, const void *b) {
    return ((struct Pengiriman *)b)->timestamp - ((struct Pengiriman *)a)->timestamp;
}

void urutkanData(struct Pengiriman data[], int jumlah_data, int urutan) {
    if (urutan == 1) {
        qsort(data, jumlah_data, sizeof(struct Pengiriman), compareTimestampAsc);
        printf("\nData Pengiriman diurutkan berdasarkan tanggal secara ascending:\n");
    } else if (urutan == 2) {
        qsort(data, jumlah_data, sizeof(struct Pengiriman), compareTimestampDesc);
        printf("\nData Pengiriman diurutkan berdasarkan tanggal secara descending:\n");
    } else {
        printf("Pilihan tidak valid.\n");
        return;
    }

    tampilkanSemuaData(data, jumlah_data);
}

void simpanDataKeFileText(struct Pengiriman data[], int jumlah_data) {
    FILE *file = fopen("data_pengiriman.txt", "w");
    if (file != NULL) {
        // Print header
        fprintf(file, "Nama Pengirim;Tujuan Pengiriman;Berat Barang;Nama Penerima;Kode Resi;Harga;Timestamp;Status\n");

        for (int i = 0; i < jumlah_data; i++) {
            // Use fprintf to write data to file
            fprintf(file, "%s;%s;%.2f;%s;%s;%.2f;%ld;%s\n", data[i].nama_pengirim, data[i].tujuan_pengiriman,
                    data[i].berat_barang, data[i].nama_penerima, data[i].kode_resi, data[i].harga,
                    data[i].timestamp, data[i].status);
        }

        fclose(file);
        printf("Data berhasil disimpan ke data_pengiriman.txt.\n");
    } else {
        printf("Gagal membuka file untuk penulisan data.\n");
    }
}

void bacaDataDariFileText(struct Pengiriman data[], int *jumlah_data) {
    FILE *file = fopen("data_pengiriman.txt", "r");
    if (file != NULL) {
        // Read the header and discard it
        fscanf(file, "Nama Pengirim;Tujuan Pengiriman;Berat Barang;Nama Penerima;Kode Resi;Harga;Timestamp;Status\n");

        while (fscanf(file, "%49[^;];%[^;];%f;%[^;];%[^;];%f;%ld;%[^\n]\n",
                      data[*jumlah_data].nama_pengirim, data[*jumlah_data].tujuan_pengiriman,
                      &data[*jumlah_data].berat_barang, data[*jumlah_data].nama_penerima,
                      data[*jumlah_data].kode_resi, &data[*jumlah_data].harga,
                      &data[*jumlah_data].timestamp, data[*jumlah_data].status) == 8) {
            (*jumlah_data)++;
        }

        fclose(file);
    } else {
        printf("File tidak ditemukan atau gagal membuka file untuk membaca data.\n");
    }
}

int main() {
    const int maks_data = 100;
    struct Pengiriman data[maks_data];
    int jumlah_data = 0;

    bacaDataDariFileText(data, &jumlah_data);

    int pilihan, urutan;
    char kode_resi_cari[10];

    do {
        printf("\nMenu:\n");
        printf("1. Tambah Data Pengiriman\n");
        printf("2. Cari Data Pengiriman\n");
        printf("3. Tampilkan Semua Data Pengiriman\n");
        printf("4. Urutkan Data Berdasarkan Tanggal\n");
        printf("5. Edit Status Pengiriman\n");
        printf("6. Keluar\n");
        printf("Pilih menu (1-6): ");
        scanf("%d", &pilihan);
        newLine();

        switch (pilihan) {
            case 1:
                printf("\nMasukkan data pengiriman\n");
                printf("Nama Pengirim   : ");
                fgets(data[jumlah_data].nama_pengirim, sizeof(data[jumlah_data].nama_pengirim), stdin);
                strtok(data[jumlah_data].nama_pengirim, "\n");

                printf("Tujuan Pengiriman: ");
                fgets(data[jumlah_data].tujuan_pengiriman, sizeof(data[jumlah_data].tujuan_pengiriman), stdin);
                strtok(data[jumlah_data].tujuan_pengiriman, "\n");

                printf("Berat Barang (kg): ");
                scanf("%f", &data[jumlah_data].berat_barang);
                newLine();

                printf("Nama Penerima    : ");
                fgets(data[jumlah_data].nama_penerima, sizeof(data[jumlah_data].nama_penerima), stdin);
                strtok(data[jumlah_data].nama_penerima, "\n");

                sprintf(data[jumlah_data].kode_resi, "R%03d", jumlah_data + 1);

                data[jumlah_data].harga = hitungHarga(data[jumlah_data].berat_barang);

                data[jumlah_data].timestamp = time(NULL);

                printf("\nKode Resi yang telah diinput:\n");
                tampilkanKodeResi(data[jumlah_data]);

                printf("\nPilih status pengiriman (1. Ongoing, 2. Delivered): ");
                int status_choice;
                scanf("%d", &status_choice);
                newLine();

                switch (status_choice) {
                    case 1:
                        strcpy(data[jumlah_data].status, "Ongoing");
                        break;
                    case 2:
                        strcpy(data[jumlah_data].status, "Delivered");
                        break;
                    default:
                        printf("Pilihan status tidak valid. Status di set default sebagai Ongoing.\n");
                        strcpy(data[jumlah_data].status, "Ongoing");
                }

                jumlah_data++;
                simpanDataKeFileText(data, jumlah_data);
                break;

            case 2:
                printf("\nMasukkan kode resi untuk mencari data: ");
                fgets(kode_resi_cari, sizeof(kode_resi_cari), stdin);
                strtok(kode_resi_cari, "\n");
                cariData(data, jumlah_data, kode_resi_cari);
                break;

            case 3:
                tampilkanSemuaData(data, jumlah_data);
                break;

            case 4:
                printf("\nPilih urutan pengurutan:\n");
                printf("1. Ascending\n");
                printf("2. Descending\n");
                printf("Pilih urutan (1-2): ");
                scanf("%d", &urutan);
                newLine();

                urutkanData(data, jumlah_data, urutan);
                break;

            case 5:
                printf("\nMasukkan kode resi untuk mengedit status: ");
                fgets(kode_resi_cari, sizeof(kode_resi_cari), stdin);
                strtok(kode_resi_cari, "\n");
                cariData(data, jumlah_data, kode_resi_cari);

                int index;
                for (index = 0; index < jumlah_data; index++) {
                    if (strcmp(data[index].kode_resi, kode_resi_cari) == 0) {
                        break;
                    }
                }

                if (index < jumlah_data) {
                    printf("Pilih status baru (1. Ongoing, 2. Delivered): ");
                    int status_choice;
                    scanf("%d", &status_choice);
                    newLine();

                    switch (status_choice) {
                        case 1:
                            strcpy(data[index].status, "Ongoing");
                            break;
                        case 2:
                            strcpy(data[index].status, "Delivered");
                            break;
                        default:
                            printf("Pilihan status tidak valid. Status tidak diubah.\n");
                    }
                } else {
                    printf("Data tidak ditemukan.\n");
                }
                break;

            case 6:
                simpanDataKeFileText(data, jumlah_data);
                printf("Program selesai.\n");
                break;

            default:
                printf("Pilihan tidak valid. Silakan pilih lagi.\n");
        }
    } while (pilihan != 6);

    return 0;
}
```
