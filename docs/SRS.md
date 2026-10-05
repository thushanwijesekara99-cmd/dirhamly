# Dirhamly – Software Requirements Specification v2.0

*28 September 2026 · Thushan Wijesekara*

Dirhamly helps anyone working in Dubai control their monthly salary, in English, Arabic, Hindi, Urdu, Tagalog, Bangla, Tamil or Malayalam. This version replaces SRS v1.0 and starts the product from zero.

---

## 1. Vision and users

Dirhamly answers one question every day: **how much can I safely spend today?**
Its message: *"It's not what you earn. It's how you manage it."*

**Target users:** anyone who works in Dubai and the UAE and gets a salary, from drivers, construction and shop staff to office employees and families. Most are expats, many send money home, and many are more comfortable in another language than in English.

**Problems it solves:**
- Salary arrives, rent, loans and money sent home go out, and there is no clear picture of what is really left.
- Money runs out before the next salary.
- Finance apps are in English only, complex, and ask for bank logins.

**Principles:**
1. **Simple first:** one clear number on Home. Every screen can be understood without reading long text.
2. **Your language:** eight languages from day one, with correct right-to-left layout.
3. **Private:** no account, no bank login. Data stays on the phone and works offline.
4. **Built for UAE life:** AED, rent, DEWA and Etisalat/du bills, loans, credit cards and money sent home are first-class.
5. **Free to use** for the first release.

## 2. Languages

The user picks a language on the very first screen and can change it any time in Settings; the change is instant and keeps all data.

| Language | Script | Direction | Font (Google Noto) |
|---|---|---|---|
| English | Latin | LTR | Noto Sans |
| Arabic | Arabic | RTL | Noto Sans Arabic |
| Hindi | Devanagari | LTR | Noto Sans Devanagari |
| Urdu | Arabic (Nastaliq) | RTL | Noto Nastaliq Urdu |
| Tagalog (Filipino) | Latin | LTR | Noto Sans |
| Bangla (Bengali) | Bengali | LTR | Noto Sans Bengali |
| Tamil | Tamil | LTR | Noto Sans Tamil |
| Malayalam | Malayalam | LTR | Noto Sans Malayalam |

**Rules**
- **L-1** Every word on screen comes from translation files (ARB), never hard-coded.
- **L-2** Arabic and Urdu flip the whole layout: back arrows, progress bars, lists and directional icons.
- **L-3** Amounts use Western digits in every language (e.g. `AED 1,250.00`), as UAE banks and receipts do. A single setting, changeable later.
- **L-4** Dates follow the language, using the Gregorian calendar.
- **L-5** User-typed names and notes are stored as typed; built-in names (Food, Rent) are translated.
- **L-6** The default language is the phone's language if supported, otherwise English.
- **L-7** A native speaker checks each language before release. Money words must be exact.

## 3. Money model

Everything is counted per **pay cycle** — from payday to the day before the next payday, not per calendar month.

| Input | Meaning | Source |
|---|---|---|
| Salary | Take-home salary per month | Onboarding, Settings |
| Commitments | Fixed payments this cycle: rent, bills, loan instalments, money sent home, goal savings | Onboarding, Payments, Goals |
| Extra income | Bonus, overtime, side job this cycle | Add Income |
| Spent | Day-to-day expenses this cycle | Add Expense |
| Days left | Today to the day before next payday, today included | Calendar |

**Formulas**

```
Money available     = Salary + Extra income − Commitments − Spent
Safe spending today = (Money available + Spent today) ÷ Days left − Spent today
```

**Worked example:** salary AED 5,000; commitments AED 2,550 (rent 1,200, utilities 200, phone 150, loan 500, money home 500); nothing spent; 30 days left.
Money available = **AED 2,450**. Safe spending today = 2,450 ÷ 30 = **AED 81.67**.

**Rules**
- **M-1** Weekly salary counts as × 52 ÷ 12 per month; bi-weekly as × 26 ÷ 12.
- **M-2** Marking a commitment as paid does not count again as spending.
- **M-3** If safe spending today is below zero, Home shows "No safe spending left today" and the amount over, in red.
- **M-4** If money available is below zero, Home shows "Over budget by AED …" instead of a negative balance.
- **M-5** Status: On track (spent today ≤ safe amount), Careful (over 80%), Over (above 100%).
- **M-6** A new cycle starts automatically on payday; the previous one stays in history.
- **M-7** All amounts are stored in AED with 2 decimals.

## 4. Screens

Bottom bar: **Home · Payments · (+) · Goals · More** — the centre (+) opens Add Expense.

| # | Screen | What it does | Release |
|---|---|---|---|
| 1 | Splash | Logo and tagline | 1 |
| 2 | Choose language | Eight big buttons, each in its own script | 1 |
| 3 | Welcome | "Your salary. Your dirhams. Your plan." | 1 |
| 4 | Salary setup | Name, salary, frequency, payday | 1 |
| 5 | Monthly commitments | Rent, utilities, phone, loan, money home | 1 |
| 6 | Goal setup | One optional savings goal | 1 |
| 7 | Home | Money available, safe spending today, cycle progress, upcoming payments, recent activity | 1 |
| 8 | Add Expense | Big number pad, category icons, optional note | 1 |
| 9 | Add Income | Amount, source, optional note | 1 |
| 10 | Activity | All transactions by day; filter, edit, delete | 1 |
| 11 | Payments | Bills, Loans, Money Home tabs; mark as paid | 1 |
| 12 | Savings Goals | Progress; add money to a goal | 1 |
| 13 | More / Settings | Language, profile, categories, clear data | 1 |
| 14 | Monthly Budget | Per-category limits (basic version in Release 1) | 2 |
| 15 | Reports | "Where did my money go?" donut, last 3 cycles (moved into Release 1) | 1 |
| 16 | Reminders | Notification before each payment | 2 |
| 17 | Backup and export | Save to file, restore, CSV | 3 |
| 18 | App lock | PIN or fingerprint | 3 |

## 5. Functional requirements

**Onboarding**
- **F-1** First launch shows Choose language; later launches go straight to Home.
- **F-2** Salary must be above 0; payday 1–31 (31 in a short month = last day).
- **F-3** Commitments offers ready rows (Rent, Electricity & water, Phone & Internet, Transport pass, Food/mess fee, Gym, Subscriptions, Loan/Credit card, Money sent home) where the user only types an amount. A following Everyday spending step sets category budgets — not commitments — so nothing is counted twice.
- **F-4** Every step after salary can be skipped.
- **F-5** No sign-up in Release 1.

**Home**
- **F-6** Shows greeting, money available, safe spending with status, cycle progress, next 3 payments, last 5 transactions.
- **F-7** Tapping an upcoming payment offers "Mark as paid".

**Transactions**
- **F-8** Amounts: numbers only, up to 2 decimals, above 0, up to AED 9,999,999.
- **F-9** Expense categories: Food, Transport, Shopping, Bills, Health, Family, Entertainment, Other. Income sources: Overtime, Bonus, Side job, Transfer received, Other (salary is excluded to avoid double counting).
- **F-10** Save works once per tap.
- **F-11** Date defaults to now and can be set earlier.
- **F-12** Any transaction can be edited or deleted (with confirmation).

**Payments**
- **F-13** A payment has name, amount, type (Bill, Loan, Money home, Other), due day and, for loans, total remaining.
- **F-14** Paying a loan instalment lowers its remaining total.
- **F-15** Money-home entries can hold a country and monthly target.
- **F-16** Payments reset to unpaid each new cycle.

**Goals**
- **F-17** A goal has name, target, optional date and optional monthly amount (counted as a commitment).
- **F-18** "Add money" updates saved, remaining and percent.

**Settings**
- **F-19** Language changes instantly with no data loss.
- **F-20** Salary, frequency and payday changes apply to the current cycle.
- **F-21** Clear all data asks twice, then returns to Choose language.

## 6. Data, privacy and storage

All data stays on the phone. No server, no account, no bank connection.

- **D-1** Local on-device database (Hive or SQLite), saved after every change.
- **D-2** Stores profile, transactions, payments, goals and pay-cycle history.
- **D-3** No financial data or names are written to logs or sent anywhere.
- **D-4** Uninstalling deletes the data; Settings says so until Backup exists.
- **D-5** A damaged record is skipped on load; the rest still opens.
- **D-6** No ads and no tracking in Release 1.

## 7. Design and usability

Navy buttons, green accents, white cards, rounded corners.

- **U-1** One main number per screen, large and bold.
- **U-2** Every category and action has an icon.
- **U-3** Touch targets at least 48 × 48 pt; main buttons full width.
- **U-4** Short words: "Money available", not "Net disposable income".
- **U-5** Respects system font size up to 130%.
- **U-6** Colour is never the only signal.
- **U-7** Every list has a helpful empty state.
- **U-8** Works on 360 pt-wide phones, Android 8+.

## 8. Build phases

A fresh Flutter project, built in small steps, each tested on the Pixel 7 emulator.

1. **Foundation:** project structure, theme, fonts, all languages with RTL, local storage, data models, money calculations with tests.
2. **Onboarding:** Splash → Goal setup.
3. **Home and transactions:** Home, Add Expense, Add Income, Activity, bottom bar.
4. **Payments and Goals.**
5. **Settings and polish:** empty states, native-speaker checks, small-phone testing.
6. **Release 1:** app icon, store screenshots, privacy policy, Play Store internal test.
7. **Release 2:** Budget, Reminders. **Release 3:** Backup, export, app lock.

## 9. Acceptance criteria – Release 1

- [ ] A new user picks a language and finishes setup in under 2 minutes.
- [ ] Every screen is fully translated, with no English left in the other seven languages.
- [ ] Arabic and Urdu screens are fully right-to-left, nothing cut off.
- [ ] Salary 5,000 and commitments 2,550 on day 1 of a 30-day cycle → AED 2,450.00 available, AED 81.67 safe today.
- [ ] Adding an expense updates Home, Activity and safe spending at once.
- [ ] Data survives closing the app and restarting the phone.
- [ ] Changing language keeps all data.
- [ ] Invalid amounts (empty, 0, letters, 3 decimals) cannot be saved.
- [ ] A new cycle starts on payday and payments reset to unpaid.
- [ ] The app works with no internet connection.
- [ ] No crash in a full test pass on emulator and a small real phone.
