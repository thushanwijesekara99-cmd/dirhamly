# Dirhamly 💰

**A simple, private salary-planning app for people working in Dubai and the UAE — in 8 languages.**

> *"It's not what you earn. It's how you manage it."*

Dirhamly answers one question every day: **how much can I safely spend today?**

![Status](https://img.shields.io/badge/status-in%20development-orange)
![Flutter](https://img.shields.io/badge/Flutter-Dart-02569B?logo=flutter)
![Platform](https://img.shields.io/badge/platform-Android%208%2B-3DDC84?logo=android)
![Offline](https://img.shields.io/badge/works-offline-success)

<!-- Add 3–4 screenshots here: Home, Add Expense, Payments, Arabic RTL screen -->
<!-- ![Home](docs/screenshots/home.png) ![Arabic](docs/screenshots/home-ar.png) -->

---

## The problem

Most salaried workers in the UAE are expats. Salary arrives, then rent, DEWA, phone bills, loan instalments and money sent home go out — and there's no clear picture of what is really left. Money runs out before the next payday.

Existing finance apps don't fit them: they're English-only, complicated, and ask for bank logins.

## The solution

Dirhamly is built for drivers, construction and shop staff, office employees and families:

- **One clear number on Home** — safe spending for today, with an *On track / Careful / Over* status
- **Your language from day one** — English, Arabic, Hindi, Urdu, Tagalog, Bangla, Tamil and Malayalam, with full right-to-left layout for Arabic and Urdu
- **Private by design** — no account, no bank login, no server. All data stays on the phone and works fully offline
- **Built for UAE life** — AED, rent, DEWA and Etisalat/du bills, loans, credit cards and money sent home are first-class
- **Pay-cycle based** — budgets run from payday to payday, not calendar month

## How the money model works

Everything is counted per **pay cycle** (e.g. 28th → 27th).

```
Money available     = Salary + Extra income − Commitments − Spent
Safe spending today = (Money available + Spent today) ÷ Days left − Spent today
```

**Example:** salary AED 5,000, commitments AED 2,550, 30 days left
→ Money available **AED 2,450.00** → Safe today **AED 81.67**

Rules handle weekly/bi-weekly salaries, loan balances that drop as instalments are paid, automatic cycle rollover on payday, and clear messages instead of negative numbers when over budget.

## Features

| Release | Features |
|---|---|
| **1** | Language picker · 2-minute onboarding (salary, commitments, everyday budgets, goal) · Home dashboard · Add expense / income · Activity history · Payments (Bills, Loans, Money Home) · Savings goals · Reports ("Where did my money go?") · Settings |
| **2** | Category budgets · Payment reminders |
| **3** | Backup & restore · CSV export · App lock (PIN / fingerprint) |

## Tech stack

| Layer | Choice |
|---|---|
| App | Flutter (Dart), Android first |
| Storage | Local on-device database (Hive / SQLite) |
| Localisation | Flutter ARB files, 8 locales, RTL support |
| Fonts | Google Noto family (Sans, Arabic, Devanagari, Nastaliq Urdu, Bengali, Tamil, Malayalam) |
| Testing | Unit tests for the money calculations; Pixel 7 emulator + small real device |

## Design principles

- One main number per screen, large and bold
- Icons on every category and action, so the app works with little reading
- 48 × 48 pt touch targets, full-width main buttons
- Colour is never the only signal (minus signs, status words)
- Works on 360 pt-wide phones, Android 8+, and up to 130% system font size

## Documentation

- [Software Requirements Specification v2.0](docs/SRS.md)

## Getting started

> The Flutter source code is being prepared for upload. Once it's here:

```bash
git clone https://github.com/thushanwijesekara99-cmd/dirhamly.git
cd dirhamly
flutter pub get
flutter run
```

```bash
flutter test   # runs the money-calculation tests
```

## Author

**Thushan Wijesekara** — product design, requirements and development
📧 thushanwijesekara99@gmail.com

## License

MIT — see [LICENSE](LICENSE).
