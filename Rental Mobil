# Dictionary untuk menyimpan data mobil dengan struktur data CRUD
mobil_data = {}

def main_menu():
    """
    Menampilkan menu utama untuk memilih operasi CRUD dan pelaporan
    """
    while True:
        print("\n=== Main Menu Hertz ===")
        print("1. Tambah Data Mobil")
        print("2. Tampilkan Data Mobil")
        print("3. Ubah Data Mobil")
        print("4. Hapus Data Mobil")
        print("5. Laporan Pendapatan")
        print("6. Mobil Paling Sering Disewa")
        print("7. Laporan Mobil")
        print("8. Keluar")
        choice = input("Pilih menu: ")
        
        if choice == '1':
            create_menu()
        elif choice == '2':
            read_menu()
        elif choice == '3':
            update_menu()
        elif choice == '4':
            delete_menu()
        elif choice == '5':
            laporan_pendapatan()
        elif choice == '6':
            laporan_mobil_sering_disewa()
        elif choice == '7':
            laporan_mobil()
        elif choice == '8':
            print("Terima kasih, sampai jumpa!")
            break
        else:
            print("Pilihan tidak valid, silakan coba lagi.")

def create_menu():
    """
    Menu untuk menambah data mobil baru
    """
    primary_key = input("Masukkan nomor registrasi mobil: ")

    if primary_key in mobil_data:
        print("Notifikasi: Data sudah ada!")
    else:
        nama_mobil = input("Masukkan nama mobil: ")
        status = input("Masukkan status (Available/Rented): ")
        harga_sewa = float(input("Masukkan harga sewa per hari: "))
        durasi_sewa = int(input("Masukkan durasi sewa (dalam hari): "))

        penyewa = {}
        if status.lower() == 'rented':
            penyewa['nama_penyewa'] = input("Masukkan nama penyewa: ")
            penyewa['negara_asal'] = input("Masukkan negara asal penyewa: ")
        else:
            penyewa['nama_penyewa'] = None
            penyewa['negara_asal'] = None

        mobil_data[primary_key] = {
            "nama_mobil": nama_mobil,
            "status": status,
            "harga_sewa": harga_sewa,
            "durasi_sewa": durasi_sewa,
            "total_pendapatan": harga_sewa * durasi_sewa if status.lower() == 'rented' else 0,
            "penyewa": penyewa
        }

        save_option = input("Simpan data? (Y/N): ")
        if save_option.lower() == 'y':
            print("Data berhasil disimpan.")
        else:
            print("Data tidak disimpan.")
        
    main_menu()

def read_menu():
    """
    Menu untuk menampilkan data mobil
    """
    if not mobil_data:
        print("Data kosong.")
    else:
        for key, data in mobil_data.items():
            penyewa_info = f"Penyewa: {data['penyewa']['nama_penyewa']}, Negara: {data['penyewa']['negara_asal']}" if data['penyewa']['nama_penyewa'] else "Belum ada penyewa"
            print(f"Nomor Registrasi: {key}, Mobil: {data['nama_mobil']}, Status: {data['status']}, {penyewa_info}")

    main_menu()

def update_menu():
    """
    Menu untuk mengubah data mobil
    """
    primary_key = input("Masukkan nomor registrasi mobil yang ingin diubah: ")

    if primary_key in mobil_data:
        print(f"Data Lama: {mobil_data[primary_key]}")
        nama_mobil = input("Masukkan nama mobil baru: ")
        status = input("Masukkan status baru (Available/Rented): ")
        harga_sewa = float(input("Masukkan harga sewa per hari baru: "))
        durasi_sewa = int(input("Masukkan durasi sewa baru: "))

        penyewa = {}
        if status.lower() == 'rented':
            penyewa['nama_penyewa'] = input("Masukkan nama penyewa: ")
            penyewa['negara_asal'] = input("Masukkan negara asal penyewa: ")
        else:
            penyewa['nama_penyewa'] = None
            penyewa['negara_asal'] = None

        mobil_data[primary_key] = {
            "nama_mobil": nama_mobil,
            "status": status,
            "harga_sewa": harga_sewa,
            "durasi_sewa": durasi_sewa,
            "total_pendapatan": harga_sewa * durasi_sewa if status.lower() == 'rented' else 0,
            "penyewa": penyewa
        }
        print("Data berhasil diubah.")
    else:
        print("Data tidak ditemukan.")

    main_menu()

def delete_menu():
    """
    Menu untuk menghapus data mobil
    """
    primary_key = input("Masukkan nomor registrasi mobil yang ingin dihapus: ")

    if primary_key in mobil_data:
        del mobil_data[primary_key]
        print("Data berhasil dihapus.")
    else:
        print("Data tidak ditemukan.")

    main_menu()

def laporan_pendapatan():
    """
    Laporan total pendapatan dari semua mobil yang disewa
    """
    total_pendapatan = 0
    for data in mobil_data.values():
        total_pendapatan += data.get("total_pendapatan", 0)

    print(f"Total Pendapatan dari Penyewaan: ${total_pendapatan}")
    main_menu()

def laporan_mobil_sering_disewa():
    """
    Laporan mobil yang paling sering disewa berdasarkan durasi sewa
    """
    mobil_tersering = max(mobil_data.items(), key=lambda x: x[1]['durasi_sewa'], default=None)
    
    if mobil_tersering:
        print(f"Mobil yang paling sering disewa: {mobil_tersering[1]['nama_mobil']} - Durasi: {mobil_tersering[1]['durasi_sewa']} hari")
    else:
        print("Belum ada data penyewaan mobil.")

    main_menu()

def laporan_mobil():
    """
    Laporan mobil yang tersedia dan yang sedang disewa
    """
    available_mobil = [data['nama_mobil'] for data in mobil_data.values() if data['status'].lower() == 'available']
    rented_mobil = [f"{data['nama_mobil']} (Penyewa: {data['penyewa']['nama_penyewa']}, Negara: {data['penyewa']['negara_asal']})" 
                    for data in mobil_data.values() if data['status'].lower() == 'rented']

    print("\n=== Laporan Mobil Hertz ===")
    print(f"Mobil Tersedia ({len(available_mobil)}): {', '.join(available_mobil) if available_mobil else 'Tidak ada mobil yang tersedia'}")
    print(f"Mobil Sedang Disewa ({len(rented_mobil)}): {', '.join(rented_mobil) if rented_mobil else 'Tidak ada mobil yang disewa'}")

    main_menu()

# Memulai aplikasi dengan menampilkan main menu
if __name__ == "__main__":
    main_menu()
