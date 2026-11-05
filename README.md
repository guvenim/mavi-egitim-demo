# Python for Fabric Notebooks — Eğitim Demo Verisi

Bu repo **Python for Fabric Notebooks** eğitimindeki "API'den dosya okuyup tabloya yazma" demosu için hazırlanmıştır.

| Dosya | İçerik |
|---|---|
| `magaza_hedefleri_2025.xlsx` | 30 mağaza × 12 ay net ciro hedefi (TL). **Sentetik veridir**, gerçek bir kuruma ait değildir. |

Fabric notebook'tan anahtarsız okuma:

```python
import io, requests, pandas as pd

URL = "https://raw.githubusercontent.com/<kullanici>/<repo>/main/magaza_hedefleri_2025.xlsx"
r = requests.get(URL, timeout=30)
r.raise_for_status()
ham = pd.read_excel(io.BytesIO(r.content), sheet_name="Hedefler", header=3, thousands=".")
```

Dosyada gerçek hayattaki Excel'lerin tipik sorunları kasıtlı olarak bırakıldı: başlık satırları, birleştirilmiş hücreler, geniş format (ay kolonları), metin olarak girilmiş sayılar, boş hücreler ve "Genel Toplam" satırı.
