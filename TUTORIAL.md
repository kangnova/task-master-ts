# Tutorial Belajar TypeScript: Membuat Aplikasi Task Master

Selamat datang! Dokumen ini dirancang untuk membimbing Anda langkah demi langkah dalam mempelajari TypeScript melalui pembuatan aplikasi manajemen tugas sederhana (*Task Master*).

## 📋 Prasyarat
Sebelum memulai, pastikan Anda sudah menginstal:
1.  **Node.js**: Unduh dan instal dari [nodejs.org](https://nodejs.org/).
2.  **Visual Studio Code (VS Code)**: Editor kode yang disarankan.

---

## 🚀 Langkah 1: Persiapan Proyek

Mari kita mulai dengan menyiapkan folder proyek kita. Buka terminal (Command Prompt atau PowerShell) di dalam folder `task-master-ts`.

### 1. Inisialisasi `package.json`
Jalankan perintah ini untuk membuat file konfigurasi proyek Node.js:
```bash
npm init -y
```
Ini akan membuat file `package.json` yang berguna untuk mencatat pustaka (library) yang kita gunakan.

### 2. Instalasi TypeScript
Kita perlu menginstal TypeScript dan alat bantu `ts-node` (untuk menjalankan kode TS secara langsung) sebagai dependensi pengembangan (*devDependencies*):
```bash
npm install -D typescript ts-node
```

### 3. Konfigurasi TypeScript
Buat file konfigurasi TypeScript `tsconfig.json` dengan perintah:
```bash
npx tsc --init
```
Ini akan membuat file dasar. Jangan khawatir tentang isinya sekarang, pengaturan default sudah cukup bagus untuk memulai.

---

## 📝 Langkah 2: Memahami Dasar TypeScript

TypeScript adalah JavaScript dengan **Tipe Data**. Ini membantu kita menangkap error sebelum kode dijalankan.

Buat folder bernama `src` dan file baru di dalamnya bernama `index.ts`.
Mari kita coba kode pertama:

```typescript
// src/index.ts

// Tipe data eksplisit
let pesan: string = "Halo, TypeScript!";
let angka: number = 100;
let isAktif: boolean = true;

console.log(pesan);
console.log(`Angka: ${angka}, Status: ${isAktif}`);
```

Jalankan kode tersebut dengan perintah:
```bash
npx ts-node src/index.ts
```

---

## 🛠️ Langkah 3: Membuat Aplikasi Task Master

Sekarang kita akan membangun aplikasi manajemen tugas. Kita akan belajar tentang **Interface**, **Enum**, dan **Class**.

### 1. Menggunakan `Enum` untuk Status Tugas
Enum (Enumeration) memungkinkan kita mendefinisikan sekumpulan konstanta bernama. Ini sangat berguna untuk status.

Tambahkan kode ini ke `src/index.ts` (hapus kode sebelumnya):

```typescript
// Mendefinisikan status tugas
enum TaskStatus {
    Pending = "Pending",
    InProgress = "Sedang Dikerjakan",
    Completed = "Selesai"
}
```

### 2. Menggunakan `Interface` untuk Struktur Data
Interface mendefinisikan bentuk (shape) dari sebuah objek. Ini seperti "kontrak" yang harus dipenuhi oleh objek tersebut.

Tambahkan di bawah enum:

```typescript
interface Task {
    id: number;
    title: string;
    status: TaskStatus;
    completedAt?: Date; // Tanda '?' berarti properti ini opsional
}
```

### 3. Membuat Class `TaskManager`
Kita akan membuat class untuk mengelola daftar tugas (tambah, tampilkan, ubah status).

```typescript
class TaskManager {
    private tasks: Task[] = []; // Array untuk menyimpan daftar tugas
    private nextId: number = 1;

    // Menambahkan tugas baru
    addTask(title: string): void {
        const newTask: Task = {
            id: this.nextId++,
            title: title,
            status: TaskStatus.Pending
        };
        this.tasks.push(newTask);
        console.log(`[+] Tugas ditambahkan: "${title}"`);
    }

    // Menampilkan semua tugas
    listTasks(): void {
        console.log("\n--- Daftar Tugas ---");
        this.tasks.forEach(task => {
            console.log(`${task.id}. [${task.status}] ${task.title}`);
        });
        console.log("--------------------\n");
    }

    // Mengubah status tugas
    updateTaskStatus(id: number, status: TaskStatus): void {
        const task = this.tasks.find(t => t.id === id);
        if (task) {
            task.status = status;
            if (status === TaskStatus.Completed) {
                task.completedAt = new Date();
            }
            console.log(`[U] Status tugas "${task.title}" diubah menjadi: ${status}`);
        } else {
            console.log(`[!] Tugas dengan ID ${id} tidak ditemukan.`);
        }
    }
}
```

### 4. Menjalankan Aplikasi
Terakhir, mari kita gunakan class yang sudah kita buat.

```typescript
// --- Main Program ---

const myTaskManager = new TaskManager();

// 1. Tambah tugas
myTaskManager.addTask("Belajar TypeScript Dasar");
myTaskManager.addTask("Membuat Project Pertama");

// 2. Tampilkan tugas
myTaskManager.listTasks();

// 3. Update tugas
myTaskManager.updateTaskStatus(1, TaskStatus.InProgress);
myTaskManager.updateTaskStatus(2, TaskStatus.Completed);

// 4. Tampilkan lagi untuk melihat perubahan
myTaskManager.listTasks();
```

---

## ✅ Langkah 4: Eksekusi Akhir

Simpan file `src/index.ts` Anda.
Jalankan kembali di terminal:

```bash
npx ts-node src/index.ts
```

Jika berhasil, Anda akan melihat output log penambahan tugas, daftar tugas, dan perubahan status di terminal Anda.

Selamat! Anda telah berhasil membuat aplikasi TypeScript pertama Anda dengan konsep Tipe Data, Enum, Interface, dan Class.
