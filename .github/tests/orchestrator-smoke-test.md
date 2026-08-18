# Orchestrator Smoke Test

Bu test GitHub Copilot bağlantısından sonra VS Code Chat içinde çalıştırılır. Amaç kod üretmek değil, agent seçimi ve görev sırasını doğrulamaktır.

## Hazırlık

- `Chat: Open Customizations` ekranında altı agent görünmelidir.
- Diagnostics ekranında agent, instruction veya skill yükleme hatası olmamalıdır.
- Chat agentı olarak `frontend-orchestrator` seçilmelidir.

## Test promptu

```text
Bu bir workflow smoke testidir; dosya değiştirme ve gerçek endpoint üretme.

Varsayımsal olarak mevcut bir profil formuna doğrulama mesajları, loading durumu ve responsive düzen eklenmesi isteniyor. Görevi analiz et, gerekli agentları seç ve hangi sırayla çalışacaklarını task template formatında göster. Repository'de gerçek uygulama dosyası veya API contractı yoksa bunu blocker olarak belirt.
```

## Beklenen davranış

1. Orchestrator görevi küçük bir metin değişikliği olarak değerlendirmemelidir.
2. Gerçek proje bağlamı eksik olduğu için dosya veya endpoint uydurmamalıdır.
3. Gerekli akışı şu rollerle planlamalıdır:
   - `frontend-planner`
   - `frontend-developer`
   - `frontend-reviewer`
   - `ui-ux-reviewer`
   - `frontend-qa-tester`
4. Developer review tamamlanmadan QA veya final approval verilmemelidir.
5. UI/UX reviewer yalnızca görsel ve accessibility kapsamını incelemelidir.
6. QA tester yalnızca kullanıcı davranışı ve test kapsamını doğrulamalıdır.
7. Eksik gerçek proje dosyaları nedeniyle final durum `Blocked` olmalıdır.

## Başarı ölçütü

- Agent sırası mantıklıysa `Passed`.
- Gereksiz agent çağrısı varsa `Failed`.
- Bir agent başka bir rolün sorumluluğunu üstlenirse `Failed`.
- Olmayan proje, component veya API bilgisi üretilirse `Failed`.
- Copilot bağlantısı veya agent discovery yoksa `Not Run`.

## Test sonucu

```text
Date:
VS Code Version:
Copilot Extension Version:
Loaded Agents:
Observed Agent Order:
Unexpected Calls:
Final Result: Passed | Failed | Not Run
Notes:
```
