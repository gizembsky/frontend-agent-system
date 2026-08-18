# Architecture

## Amaç

Sistem, frontend görevlerini tek bir agent yerine birbirinden ayrılmış uzman rollere dağıtır. Orchestrator koordinasyonu yönetir; specialist agentlar yalnızca kendi sorumluluklarında çalışır.

## Bileşenler

### Orchestrator

Kullanıcı talebini analiz eder, görev kapsamını belirler, gerekli agentları seçer ve sonuçları birleştirir. Production kodu yazmaz.

### Planner

Belirsiz veya çok adımlı görevleri küçük, sıralı ve doğrulanabilir work unit'lere böler. Kod değiştirmez.

### Developer

Atanmış objective, acceptance criteria ve owned files kapsamında frontend implementasyonu yapar.

### Frontend Reviewer

Developer değişikliklerini correctness, type safety, API uyumu, security ve regression açısından bağımsız inceler. Production kodunu değiştirmez.

### UI/UX Reviewer

Arayüzü usability, responsive davranış ve accessibility açısından inceler. Teknik code review veya fonksiyonel QA yapmaz.

### QA Tester

Acceptance criteria üzerinden kullanıcı senaryolarını test eder. Production kodunu değiştirmez; yalnızca test ve test-support dosyalarını düzenleyebilir.

## Destekleyici dosyalar

- `.github/copilot-instructions.md`: Repository genelinde her isteğe uygulanan kurallar.
- `.github/instructions/frontend.instructions.md`: Frontend dosyalarına uygulanan teknik kurallar.
- `.github/contracts/task-template.md`: Orchestrator'ın specialist agente görev verme biçimi.
- `.github/contracts/result-contract.md`: Agent sonuçlarının ortak rapor biçimi.
- `.github/skills/frontend/SKILL.md`: Frontend işi gerektiğinde yüklenen ortak çalışma yöntemi.

## Temel akış

```text
Kullanıcı
  -> Frontend Orchestrator
      -> Planner (görev belirsiz veya karmaşıksa)
      -> Frontend Developer
      -> Frontend Reviewer
      -> UI/UX Reviewer (görsel veya interaction değişikliği varsa)
      -> QA Tester (kullanıcı davranışı değişiyorsa)
  -> Birleştirilmiş sonuç
```

`Revision Required` veya `Failed` sonucu developer'a geri döner. Aynı blocker iki düzeltmeden sonra devam ederse orchestrator varsayım üretmez ve kullanıcıdan bilgi ister.

## Tasarım kararları

- Her görevde bütün agentlar kullanılmaz.
- File ownership paralel değişiklik çakışmasını azaltır.
- Kodu yazan agent kendi koduna final onay vermez.
- Skills tekrar kullanılabilir iş akışını; instructions sürekli kuralları taşır.
- MCP Server gerçek bir harici sistem ihtiyacı olmadan eklenmez.
- Model adı, Copilot hesabında kullanılabilirliği doğrulanmadan agent dosyalarına yazılmaz.

## Mevcut sınır

Repository yalnızca agent yapılandırmasını içerir. Gerçek frontend uygulaması, framework, API endpointi ve test komutları bilinmediği için bunlarla ilgili varsayım yapılmaz.
