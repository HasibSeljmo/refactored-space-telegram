# 🐛 GitHub Issues Skill

**Verzija:** 1.0  
**Zadnja ažuriranja:** 2026-06-08  
**Autor:** HasibSeljmo  

---

## 📖 Opis

Ova vještina definiše kako AI agenti i automacija trebaju upravljati GitHub issue-ima u ovom repozitoriju. Obuhvata sve aspekte životnog ciklusa issue-a: od kreiranja do rješavanja.

---

## 🎯 Dostupne Operacije

### 1. **Kreiranje Issue-a**

#### Preduslov
- Reproduktibilan problem ili jasan zahtjev za feature
- Jasno definirani koraci za reprodukciju (za bugove)
- Kontekst i očekivani rezultat

#### Template za Bug Report
```markdown
## Opis Problema
[Kratko objašnjenje što se javlja]

## Koraci za Reprodukciju
1. [Korak 1]
2. [Korak 2]
3. [Korak 3]

## Očekivani Rezultat
[Što bi trebalo biti]

## Stvarni Rezultat
[Što se zaista javlja]

## Okruženje
- OS: [npr. Windows 10, macOS, Linux]
- Browser/Runtime: [npr. Chrome 120, Node.js 20]
- Verzija: [verzija projekta ili commitSHA]

## Screenshots/Logs
[Priloži relevantne slike ili log output]

## Prioritet
- [ ] Critical (blokira sve)
- [ ] High (može se raditi, ali blokira neke)
- [ ] Medium (trebalo bi riješiti, ali nije hitno)
- [ ] Low (nice-to-have)
```

#### CLI Primjer
```bash
# Kreiraj bug report issue
gh issue create \
  --title "Bug: HTTP server pada na zahtjevu s velikom payloadi" \
  --body "$(cat .github/skills/github-issues/templates/bug-report.md)" \
  --label "bug" \
  --label "needs-investigation"

# Kreiraj feature request
gh issue create \
  --title "Feature: Dodaj support za HTTPS" \
  --body "Trebamo HTTPS support za produkciju" \
  --label "enhancement" \
  --label "backlog"
```

---

### 2. **Kategorizacija Issue-a**

#### Dostupne Labels (Označavanja)

| Label | Opis | Boja |
|-------|------|------|
| `bug` | Nešto ne funkcioniše kako treba | 🔴 Red |
| `enhancement` | Novi feature ili poboljšanje | 💚 Green |
| `documentation` | Nedostaje ili loša dokumentacija | 📘 Blue |
| `good-first-issue` | Dobar početak za nove contributor-e | 💜 Purple |
| `needs-investigation` | Trebam bolje razumijevanje | 🟡 Yellow |
| `blocked` | Čeka na nešto vanjsko | 🔒 Gray |
| `help-wanted` | Tražimo pomoć od community-ja | ❓ Cyan |
| `duplicate` | Duplikat već postojećeg issue-a | 🚫 Black |
| `wontfix` | Neće biti ispravljen | 🛑 Stop |

#### Proces Kategorizacije

```
1. Čitaj Title i Body
   ├─ Je li opisano što trebam?
   └─ Mogu li reproduciram problem?

2. Dodaj Labels
   ├─ Tip (bug, enhancement, documentation)
   ├─ Prioritet (high, medium, low) - opcionalno
   └─ Status (needs-investigation, blocked, help-wanted)

3. Dodaj Milestone (ako postoji)
   └─ v1.0, v2.0, Backlog

4. Dodaj Assignee
   └─ Tko će raditi na tome?
```

#### Primjer Kategorizacije

```bash
# Bug s visokim prioritetom
gh issue create \
  --title "Critical: HTTP server se ruši na startup" \
  --label "bug" \
  --label "critical" \
  --assignee HasibSeljmo

# Feature zahtjev za community
gh issue create \
  --title "Add dark mode support" \
  --label "enhancement" \
  --label "help-wanted"
```

---

### 3. **Analiza i Triage**

#### Što Trebam Znati?

Za svaki issue postavi se sljedeća pitanja:

- ✅ **Validnost**: Je li ovo stvaran problem ili korisničku grešku?
- 🔍 **Reproduktibilnost**: Mogu li to reproducirati?
- 📊 **Uticaj**: Koliko je to važno? Koliko korisnika je pogođeno?
- 🔗 **Zavisnosti**: Postoji li drugi issue koji to blokira?
- ⏰ **Prioritet**: Kada trebam raditi na tome?

#### Primjer Triage Prozesa

```markdown
## Triage Checklist

- [ ] Issue je jasan i reproducibilan
- [ ] Labels su postavljeni pravilno
- [ ] Nema duplikata
- [ ] Prioritet je postavljen
- [ ] Assignee je dodijeljen (ako je moguće)
- [ ] Milestone je postavljeno (ako je primjenjivo)

## Analiza

**Tip**: Bug  
**Prioritet**: High  
**Složenost**: Medium (1-2 dana rada)  
**Zavisnosti**: Issue #2, Issue #5  

**Plan Rješavanja**:
1. Korak 1
2. Korak 2
3. Korak 3
```

---

### 4. **Rješavanje Issue-a (Development)**

#### Best Practices

```bash
# 1. Kreiraj branch sa brojem issue-a
git checkout -b fix/issue-123-http-server-crash

# 2. Radi na problemu
# ... kod promjena ...

# 3. Commit sa referencom na issue
git commit -m "Fix #123: HTTP server stabilizacija"

# 4. Kreiraj Pull Request koji linkuje issue
# PR će biti automatski linkovan ako koristiš:
# - "Closes #123"
# - "Fixes #123"
# - "Resolves #123"

gh pr create --title "Fix #123: HTTP server crash" \
  --body "Closes #123

## Što je Promijenjeno
- Dodao sam error handling
- Validacija payload-a
"
```

#### Commit Message Konvencija

```
<type>(<scope>): <subject>

<body>

Closes #123
```

**Tipovi:**
- `fix:` - Bug ispravka
- `feat:` - Novi feature
- `docs:` - Dokumentacija
- `refactor:` - Refaktoring koda
- `test:` - Testiranje

**Primjer:**
```
fix(http-server): prevent crash on large payload

Added validation for incoming request size to prevent
out-of-memory crashes. Maximum payload is now 10MB.

Closes #123
```

---

### 5. **Zatvoren Issue-a**

#### Automatsko Zatvaranje

GitHub će automatski zatvoriti issue kada PR bude merged ako koristiš:

```markdown
Closes #123
Fixes #123
Resolves #123
```

#### Ručno Zatvaranje

```bash
# Zatvori issue bez PR-a
gh issue close 123 --reason "completed"

# Sa komentar om
gh issue comment 123 --body "Problem je riješen u commit-u XYZ"
```

#### Status Issue-a

- 🟢 **Open** - U procesu ili čeka na atenciju
- 🔴 **Closed** - Riješeno ili odbijeno
- 🟠 **In Progress** - Neko radi na tome (labelom se označava)

---

## 📋 Workflow Primjer: Kompletan Životni Ciklus

### Scenario: Bug sa HTTP serverom

```
1️⃣  REPORT
   └─ User prijavljuje: "Server pada kad pošaljem 100MB datoteku"

2️⃣  TRIAGE
   └─ Dodijaljivam: @HasibSeljmo, label "bug", prioritet "high"

3️⃣  INVESTIGATION
   └─ Komentari: "Reproduciram na macOS 14.5 sa 50MB+ payload"

4️⃣  DEVELOPMENT
   ├─ Branch: fix/issue-42-large-payload
   ├─ Kod: Dodaj size validation
   └─ Commit: "fix(http-server): limit payload size to 10MB"

5️⃣  REVIEW
   └─ PR #15 approved ✅

6️⃣  MERGE & CLOSE
   └─ Issue #42 automatski zatvoren
```

---

## 🔧 Alati i Komande

```bash
# CLI Komande (GitHub CLI)

# Lista svih open issue-a
gh issue list

# Prikazi specifičan issue
gh issue view 123

# Kreiraj issue
gh issue create --title "..." --body "..."

# Dodaj label
gh issue edit 123 --add-label "bug"

# Dodaj comment
gh issue comment 123 --body "..."

# Zatvori issue
gh issue close 123

# Otvori issue
gh issue reopen 123
```

---

## ⚠️ Edge Cases i Limitacije

### Što NIJE Dozvoljeno

- ❌ **Spam Issues** - Bessmisleni ili promidžbeni issue-i
- ❌ **Duplikati** - Isti problem već postoji
- ❌ **Nejasni Izveštaji** - Bez reproducible koraka
- ❌ **Off-Topic** - Nije dio ovog projekta

### Kako Upravljati

```markdown
# Odgovor na Spam/Duplikat

"Hvala što ste prijavio, ali ovaj issue je [duplikat #XYZ / nije relevantan].

Zatvaram ga, ali slobodno se vratite s dodatnim informacijama ako je potrebno."
```

---

## 📚 Dodatni Resursi

- [GitHub Issues Dokumentacija](https://docs.github.com/en/issues)
- [GitHub CLI Upustva](https://cli.github.com/)
- [Semantic Commit Messages](https://www.conventionalcommits.org/)

---

## ✅ Checklist za Skill Mastery

Kada ovladaš ovim skill-om, trebaj biti u stanju da:

- [ ] Napraviš detaljan bug report sa reproducible koracima
- [ ] Pravilno kategoriziram issue-e sa labelama
- [ ] Svedam prioritete i činim triage
- [ ] Povežeš commit-e sa issue-ima
- [ ] Automatski zatvoriš issue-e kroz PR merge
- [ ] Upravljaš duplikatima i spam issue-ima

---

**Zadnja Ažuriranja:** 2026-06-08  
**Maintainer:** @HasibSeljmo