# Frontend Agent System

Frontend geliştirme görevlerini uzman rollere ayıran GitHub Copilot ve VS Code custom agent yapısıdır.

## Amaç

Planlama, implementasyon, teknik review, UI/UX review ve QA sorumluluklarını ayırarak daha kontrollü bir frontend çalışma akışı oluşturmak.

## Yapı

```text
.github/
  agents/                 Agent rolleri
  contracts/              Görev ve sonuç formatları
  instructions/           Frontend dosyalarına özel kurallar
  skills/frontend/        Tekrar kullanılabilir frontend çalışma yöntemi
  copilot-instructions.md Repository genel kuralları
.vscode/settings.json     Markdown editör görünümü
ARCHITECTURE.md            Sistem akışı ve sorumluluklar
```

## Agentlar

- `frontend-orchestrator`: Talebi analiz eder ve gerekli agentları yönlendirir.
- `frontend-planner`: Büyük veya belirsiz görevi küçük işlere böler.
- `frontend-developer`: Frontend implementasyonu yapar.
- `frontend-reviewer`: Teknik code review yapar.
- `ui-ux-reviewer`: Usability, responsive ve accessibility inceler.
- `frontend-qa-tester`: Kullanıcı davranışını test eder.

## Kullanım

1. Repository'yi VS Code ile aç.
2. GitHub Copilot ve Copilot Chat'i kurup GitHub hesabına bağlan.
3. `Chat: Open Customizations` ekranında altı agentın yüklendiğini doğrula.
4. `frontend-orchestrator` agentını seç ve frontend talebini yaz.
5. Orchestrator'ın yalnızca gerekli specialist agentları çağırdığını kontrol et.

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

## Doğrulama

Copilot bağlantısından sonra `.github/tests/orchestrator-smoke-test.md` içindeki senaryoyu çalıştır. Customizations Diagnostics ekranında agent, instruction ve skill yükleme hatası olmadığını kontrol et.

## Model ve MCP

Agent dosyalarında model sabitlenmemiştir; seçili Copilot modelini devralırlar. Model adı ancak hesapta kullanılabilirliği doğrulandıktan sonra eklenmelidir. Bu yapı için şu anda MCP Server gerekmez.

## GitHub'a aktarma

Değişiklikleri doğrudan `main` branch üzerinde geliştirme. GitHub repository erişimi açıldığında yeni bir feature branch oluştur, dosyaları commit et ve pull request ile gönder.

Örnek branch adı:

```text
feature/frontend-agent-system
```
