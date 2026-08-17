---
name: frontend
description: Frontend görevlerini mevcut proje yapısına uygun, type-safe, erişilebilir ve doğrulanabilir şekilde yürütür. Component, sayfa, form, state, API entegrasyonu, responsive arayüz veya frontend testi oluşturma ve değiştirme görevlerinde kullan.
---

# Frontend Workflow

## Çalışma sırası

1. Görevi ve acceptance criteria'yı netleştir.
2. `.github/instructions/` ve `.github/contracts/` dosyalarını oku.
3. İlgili component, route, hook, service, test ve package scriptlerini incele.
4. Mevcut patternleri kullanarak minimum gerekli değişikliği yap.
5. Görevle ilgili loading, error, empty, responsive ve accessibility durumlarını değerlendir.
6. Uygun lint, type-check, test veya build komutlarını çalıştır.
7. Sonucu contract formatında ve kanıtlarıyla raporla.

## Kurallar

- Var olmayan API endpointi, contract, component veya package üretme.
- Görev dışı refactor ve yeni dependency ekleme.
- Mevcut state, styling ve test yaklaşımını koru.
- Secret veya hassas veriyi frontend koduna ekleme.
- Test çalıştırılmadıysa başarılı olarak raporlama.
- Kritik bilgi eksikse tahmin etme; `Blocked` bildir.

## Tamamlanma kontrolü

- Acceptance criteria karşılandı mı?
- Yalnızca izin verilen dosyalar değişti mi?
- Type-check veya build hatası var mı?
- İlgili testler çalıştı mı?
- Bilinen riskler raporlandı mı?
