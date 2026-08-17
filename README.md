# Frontend Agent System

Frontend geliştirme görevlerini uzman rollere ayıran VS Code custom agent yapısıdır.

## Yapı

```text
.github/
  agents/         Agent rolleri
  skills/         Tekrar kullanılabilir frontend çalışma yöntemi
  instructions/   Ortak teknik kurallar
  contracts/      Agentlar arası görev ve sonuç formatları
```

## Agentlar

- `frontend-orchestrator`: Talebi analiz eder ve gerekli agentları yönlendirir.
- `frontend-planner`: Büyük veya belirsiz görevi küçük işlere böler.
- `frontend-developer`: Frontend implementasyonu yapar.
- `frontend-reviewer`: Teknik code review yapar.
- `ui-ux-reviewer`: Usability, responsive ve accessibility inceler.
- `frontend-qa-tester`: Kullanıcı davranışını test eder.

## Kullanım

VS Code'da `frontend-orchestrator` agentını seç ve frontend talebini yaz. Orchestrator görevin kapsamına göre yalnızca gerekli agentları çalıştırır.

```text
Küçük değişiklik: Developer -> Reviewer
Davranış değişikliği: Developer -> Reviewer -> QA
Görsel değişiklik: Developer -> Reviewer -> UI/UX Reviewer -> QA
Karmaşık görev: Planner -> Developer -> gerekli kontroller
```

## Dosyaların farkı

- Agent: Belirli bir rolü tanımlar.
- Skill: Frontend işinin hangi sırayla yürütüleceğini öğretir.
- Instructions: Her frontend değişikliğinde uygulanacak kuralları belirtir.
- Contract: Agentların görev ve sonuç bilgilerini aynı formatta aktarmasını sağlar.
