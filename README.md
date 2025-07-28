# 🔐 Zero Trust Security Framework

> "Never trust, always verify – with code, not assumptions."

## 📌 Opis

Ten projekt to szkielet wdrożenia architektury **Zero Trust Security** (ZTNA), skoncentrowany na:
- Kontroli dostępu opartej o tożsamość i kontekst
- Analizie urządzeń i ich integralności
- Walidacji sesji i kryptograficznych tokenów
- Politykach dostępu dynamicznie reagujących na zagrożenia

Możesz używać tego frameworka jako podstawy do:
- budowy infrastruktury militarnej/off-grid,
- systemów śledzenia/autoryzacji,
- bezpiecznego CI/CD lub backendu wrażliwego środowiska.

---

## ⚙️ Komponenty

### 🔍 `device_fingerprint.py`
Zbiera identyfikatory urządzeń:
- hash CPU + MAC
- fingerprint przeglądarki lub klienta
- geo-IP i czas reakcji

### 🔐 `access_controller.py`
Decyzje o dostępie oparte o:
- poświadczenia + fingerprint
- lokalizację
- poziom zaufania (`TrustScore`)

### 🧠 `session_validator.py`
Waliduje każdą sesję przez:
- token JWT + timestamp + podpis HMAC
- analizę zgodności z polityką `ztna_policy.yml`

### 🔧 `utils/crypto_ops.py`
Szyfrowanie komunikacji, generatory tokenów, losowe klucze.

---

## 📁 Przykładowa polityka (`config/ztna_policy.yml`)
```yaml
ztna_policy:
  allowed_geo: ['PL', 'DE']
  trust_threshold: 70
  device_integrity_required: true
  session_expiry_minutes: 30
  token_algorithm: 'HS512'
```

---

## 🚀 Uruchomienie

1. Zainstaluj zależności:
```bash
pip install -r requirements.txt
```

2. Uruchom lokalny test:
```bash
python3 src/access_controller.py
```

---

## 🔐 Przykład decyzji o dostępie
```json
{
  "user": "alpha007",
  "device_trust": 83,
  "geo": "PL",
  "access_granted": true,
  "reason": "All conditions satisfied"
}
```

---

## 🧱 Architektura

📁 [`architecture/zero-trust-model.md`](architecture/zero-trust-model.md) zawiera pełny opis koncepcji:
- Model warstwowy
- Autonomiczny kontroler
- Połączenie z SIEM / monitorowaniem
- Scenariusze militarne / off-grid

---

## 📜 Licencja

MIT – używaj swobodnie, ale nie ufaj nawet swojemu kodowi 😉

---

## 📡 Autor

🛰️ Jakub / Ghost Dev  
🌐 ZeroTrust Engineering | Military Systems  
📫 globalsign@mail.com
