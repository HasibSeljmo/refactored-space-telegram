# 💬 Review Feedback Template

Koristi ovaj template kada daješ review feedback na PR-u. Budi jasan, konstruktivan i precizan.

---

## 🔴 MUST FIX - Critical Issues

Koristi za sigurnost, logičke greške, performance problem-e:

```markdown
## 🔴 MUST FIX: [Naslov]

**Problem:** 
[Jasan opis problema]

**Zašto je ovo problem:**
[Objašnjenje uticaja]

**Preporuka:**
[Kako to ispraviti]

**Primjer:**
```[language]
[Kod primjer]
```
```

### Primjeri

```markdown
## 🔴 MUST FIX: SQL Injection Vulnerability

**Problem:**
Linija 42: User input se koristi direktno u SQL query bez validacije.

**Zašto je ovo problem:**
To omogućava SQL injection attack koji može izbrisati cijelu bazu podataka.

**Preporuka:**
Koristi parameterized queries ili ORM library.

**Primjer:**
```javascript
// ❌ LOŠE
const query = `SELECT * FROM users WHERE id = ${userId}`;

// ✅ DOBRO
const query = 'SELECT * FROM users WHERE id = ?';
db.query(query, [userId], callback);
```
```

---

## 🟡 SHOULD FIX - Important Issues

Koristi za code quality, best practices, maintainability:

```markdown
## 🟡 SHOULD FIX: [Naslov]

**Observacija:**
[Što vidiš]

**Zašto:**
[Objašnjenje]

**Sugestija:**
[Kako poboljšati]

**Primjer:**
```[language]
[Kod primjer]
```
```

### Primjeri

```markdown
## 🟡 SHOULD FIX: Function Too Long

**Observacija:**
`processUserData()` funkcija ima 120 linije i radi previše stvari.

**Zašto:**
Funkcije trebale bi biti male i fokusirane (single responsibility).
To čini kod teže razumjeti i testirati.

**Sugestija:**
Rastavi ovu funkciju u manje helper funkcije:
- `validateUser()`
- `transformUserData()`
- `saveUserToDatabase()`

**Primjer:**
```javascript
// ❌ LOŠE
function processUserData(data) {
  // 120 linije koda...
}

// ✅ DOBRO
function processUserData(data) {
  const validated = validateUser(data);
  const transformed = transformUserData(validated);
  return saveUserToDatabase(transformed);
}
```
```

---

## 🟢 NICE TO HAVE - Suggestions

Koristi za optimizacije, alternative, budućnosti:

```markdown
## 🟢 NICE TO HAVE: [Naslov]

**Prijedlog:**
[Tvoja ideja]

**Benefit:**
[Što se dobija]

**Primjer:**
```[language]
[Kod primjer]
```
```

### Primjeri

```markdown
## 🟢 NICE TO HAVE: Use Array.map() Instead of Loop

**Prijedlog:**
Ova for loop može biti elegantnije napisana sa `.map()`.

**Benefit:**
- Čitljivije
- Funkcionalni pristup
- Lakše za razumijevanje

**Primjer:**
```javascript
// ✅ Trenutno (OK)
const doubled = [];
for (let i = 0; i < numbers.length; i++) {
  doubled.push(numbers[i] * 2);
}

// ✨ Bolje
const doubled = numbers.map(n => n * 2);
```
```

---

## ✅ Kada APPROVE

```markdown
## ✅ APPROVED

[Kraći komentar zašto je dobro]

Primjeri:
- "Solid implementation. Logic je jasan, testovi su comprehensive, security je OK."
- "Great work! Performance je dobra, code je čitljiv, ready to merge."
```

---

## ⚠️ Kada REQUEST CHANGES

```markdown
## ⚠️ CHANGES REQUESTED

[Sažetak što trebaj ispraviti]

Trebaj ispraviti:
1. [MUST FIX #1]
2. [MUST FIX #2]

Opciono:
- [SHOULD FIX #1]

Primjer:
"Trebaj ispraviti SQL injection i performance issue prije merge-anja."
```

---

## 💬 Kada COMMENT ONLY

```markdown
## 💬 COMMENTED

[Informativni komentari bez blokiranje merge-a]

Primjer:
"FYI: Sličnu logiku ćeš trebati i drugdje. Možda za budući refactoring?"
```

---

## 🎯 Best Practices za Feedback

### ✅ Dobro

- "Ova logika mogla bi biti jednostavnija sa..."
- "Razmisli o edge case gdje je korisnik null"
- "Security concern: Input trebao bi biti validiran"

### ❌ Loše

- "Ovo je loš kod"
- "Zašto si to tako napisao?"
- "This is wrong" (bez objašnjenja)

---

## 📊 Primjer Kompletnog Review-a

```markdown
## 🔍 Code Review - PR #42: Add User Authentication

### 🔴 MUST FIX

## 🔴 MUST FIX: SQL Injection on Login

Linija 67: Password query nije parameterized.

[Ostalo kao gore...]

---

### 🟡 SHOULD FIX

## 🟡 SHOULD FIX: Extract Validation Logic

[Ostalo kao gore...]

---

### ✅ Dobro Rađeno

- Security checks su comprehensive
- Testovi su jasni i pokrivaju edge cases
- Documentation je izvrsna

---

### 🎯 DECISION: ⚠️ CHANGES REQUESTED

Trebaj ispraviti SQL injection na liniji 67. 
Nakon toga mogu approve. Ostalo je odličnog kvaliteta!
```

---

**Zadnja Ažuriranja:** 2026-06-08  
**Maintainer:** @HasibSeljmo
