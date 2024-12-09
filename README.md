# latihan-OOP
LATIHAN

    class FormInputMahasiswa:
    def input_data(self):
        """
        Metode untuk menginput data mahasiswa.
        """
        print("\n=== Form Input Data Mahasiswa ===")
        nim = input("Masukkan NIM: ").strip()
        nama = input("Masukkan Nama: ").strip()
        jurusan = input("Masukkan Jurusan: ").strip()
        angkatan = input("Masukkan Tahun Angkatan: ").strip()

        # Validasi sederhana
        if not nim or not nama or not jurusan or not angkatan.isdigit():
            print("Data tidak valid. Silakan coba lagi.")
            return None

        return {
            "nim": nim,
            "nama": nama,
            "jurusan": jurusan,
            "angkatan": int(angkatan),
        }

    class KelolaDataMahasiswa:
    def _init_(self):
        """
        Inisialisasi class untuk mengelola data mahasiswa.
        """
        self.data_mahasiswa = []
        self.form = FormInputMahasiswa()

    def tampilkan_data(self):
        """
        Menampilkan semua data mahasiswa.
        """
        if not self.data_mahasiswa:
            print("\nBelum ada data mahasiswa.")
            return

        print("\n=== Data Mahasiswa ===")
        for i, mhs in enumerate(self.data_mahasiswa, start=1):
            print(f"Mahasiswa {i}:")
            print(f"  NIM      : {mhs['nim']}")
            print(f"  Nama     : {mhs['nama']}")
            print(f"  Jurusan  : {mhs['jurusan']}")
            print(f"  Angkatan : {mhs['angkatan']}")
        print("======================")

    def cari_data(self, nim):
        """
        Mencari data mahasiswa berdasarkan NIM.
        """
        for mhs in self.data_mahasiswa:
            if mhs["nim"] == nim:
                return mhs
        return None

    def tambah_data(self):
        """
        Menambahkan data mahasiswa baru.
        """
        mahasiswa_baru = self.form.input_data()
        if mahasiswa_baru:
            self.data_mahasiswa.append(mahasiswa_baru)
            print("Data mahasiswa berhasil ditambahkan!")

    def hapus_data(self, nim):
        """
        Menghapus data mahasiswa berdasarkan NIM.
        """
        mahasiswa = self.cari_data(nim)
        if mahasiswa:
            self.data_mahasiswa.remove(mahasiswa)
            print("Data mahasiswa berhasil dihapus!")
        else:
            print("Data mahasiswa dengan NIM tersebut tidak ditemukan.")

    def ubah_data(self, nim):
        """
        Mengubah data mahasiswa berdasarkan NIM.
        """
        mahasiswa = self.cari_data(nim)
        if mahasiswa:
            print("\n=== Ubah Data Mahasiswa ===")
            print(f"Data saat ini: {mahasiswa}")
            mahasiswa_baru = self.form.input_data()
            if mahasiswa_baru:
                mahasiswa.update(mahasiswa_baru)
                print("Data mahasiswa berhasil diubah!")
        else:
            print("Data mahasiswa dengan NIM tersebut tidak ditemukan.")

    # Contoh penggunaan
    if __name__ == "__main__":
    kelola = KelolaDataMahasiswa()

    while True:
        print("\nMenu:")
        print("1. Tampilkan Data Mahasiswa")
        print("2. Cari Data Mahasiswa")
        print("3. Tambah Data Mahasiswa")
        print("4. Hapus Data Mahasiswa")
        print("5. Ubah Data Mahasiswa")
        print("6. Keluar")
        pilihan = input("Pilih menu (1/2/3/4/5/6): ").strip()

        if pilihan == "1":
            kelola.tampilkan_data()
        elif pilihan == "2":
            nim = input("Masukkan NIM untuk mencari: ").strip()
            mahasiswa = kelola.cari_data(nim)
            if mahasiswa:
                print(f"\nData Ditemukan: {mahasiswa}")
            else:
                print("Data tidak ditemukan.")
        elif pilihan == "3":
            kelola.tambah_data()
        elif pilihan == "4":
            nim = input("Masukkan NIM untuk menghapus: ").strip()
            kelola.hapus_data(nim)
        elif pilihan == "5":
            nim = input("Masukkan NIM untuk mengubah: ").strip()
            kelola.ubah_data(nim)
        elif pilihan == "6":
            print("Keluar dari program.")
            break
        else:
            print("Pilihan tidak valid. Silakan coba lagi.")
