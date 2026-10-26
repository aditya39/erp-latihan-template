# erp-latihan

Project contoh untuk workshop Agentic AI: backend ERP sederhana (customer, sales order, faktur) milik perusahaan fiktif PT Nusantara Rasa. Semua data dan kredensial di repo ini **dummy**.

## Mulai

Butuh JDK 17 atau lebih baru dan Maven 3.9+ (atau pakai `./mvnw`, di Windows PowerShell `.\mvnw.cmd`, yang mengunduh Maven sendiri).

```
mvn -q test            # semua test harus lulus
mvn spring-boot:run    # aplikasi di http://localhost:8080
```

Dokumentasi API: http://localhost:8080/swagger-ui.html

## Endpoint

| Method | Path | Isi |
|---|---|---|
| GET | `/api/customers`, `/api/customers/{kode}` | Daftar dan detail customer (filter `?segmen=TOKO`) |
| GET | `/api/produk` | Daftar produk aktif |
| POST | `/api/sales-orders` | Buat sales order |
| GET | `/api/sales-orders`, `/api/sales-orders/{id}` | Daftar dan detail SO (filter `?status=`) |
| POST | `/api/sales-orders/{id}/setujui` | Setujui SO yang menunggu persetujuan atau ditahan |
| POST | `/api/sales-orders/impor` | Impor SO terbuka dari CSV sistem lama |
| POST | `/api/faktur/{soId}` | Terbitkan faktur |
| GET | `/api/faktur` | Daftar faktur |

Contoh membuat SO:

```
curl -X POST http://localhost:8080/api/sales-orders -H "Content-Type: application/json" \
  -d '{"kodeCustomer": "CUS-022", "diskonTambahan": 1.0, "item": [{"kodeProduk": "BSK-001", "qty": 100}]}'
```

Aturan bisnisnya ada di [docs/aturan-bisnis.md](docs/aturan-bisnis.md).

## Folder lain

- `alert/`: contoh alert monitoring, dipakai latihan agent on call
- `scripts/kirim-alert.sh` (Git Bash, macOS, Linux) dan `scripts/kirim-alert.ps1` (PowerShell): mengirim alert ke routine
