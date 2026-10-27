# Language notes

Patterns that make website text hard to read, with typical fixes. Read only the section for the language you're working on. The general principles in SKILL.md always apply; these notes add what is specific to each language.

One caution for every language: when you swap a formal verb for a simpler one, make sure it means the same thing. "Zrealizujemy zamówienie" might mean shipping it or delivering it, and "process your order" might mean confirming it or packing it. If the page doesn't say which, keep the original verb rather than guess.

## Contents

- [Polish](#polish)
- [English](#english)
- [German](#german)
- [Other languages](#other-languages)

## Polish

The Polish plain-language movement calls this "prosty język". Most of the difficulty comes from the officialese register (styl urzędowy) and from nominal style.

**Nominalizations → verbs**

- "dokonać zakupu" → "kupić"
- "przeprowadzić analizę" → "przeanalizować", "sprawdzić"
- "w celu uzyskania informacji" → "żeby się dowiedzieć"
- "dokonać zmiany" → "zmienić"

**Passive and impersonal → active, in the site's form of address**

- "Płatność może zostać dokonana kartą lub przelewem" → "Możesz zapłacić kartą lub przelewem" (site uses "ty") / "Mogą Państwo zapłacić kartą lub przelewem" (site uses "Państwo")
- "Istnieje możliwość odbioru osobistego" → "Możesz odebrać zamówienie osobiście" / "Mogą Państwo odebrać zamówienie osobiście"

**Officialese → everyday words**

| Instead of | Write |
| --- | --- |
| posiadać | mieć |
| w przypadku gdy, w sytuacji gdy | jeśli, gdy |
| celem, w celu | żeby, aby |
| niniejszy, przedmiotowy | ten |
| w chwili obecnej | teraz |
| w związku z powyższym | dlatego |
| stanowi | jest |
| w oparciu o | na podstawie, według |
| winien | powinien |
| uprzejmie informujemy, że | (usuń, podaj od razu informację) |

**Participles → clauses**

- "Wypełniając formularz, otrzymasz rabat" → "Wypełnij formularz, a dostaniesz rabat"
- "Osoby posiadające kartę stałego klienta" → "Osoby, które mają kartę stałego klienta"

**Genitive chains (dopełniaczówki).** "w celu poprawy jakości obsługi klientów firmy" has four genitives in a row. Break it up with a verb: "żeby lepiej obsługiwać naszych klientów".

**Marketing clichés.** "Kompleksowe rozwiązania", "szeroki wachlarz usług", "indywidualne podejście do klienta", "najwyższa jakość" and "wieloletnie doświadczenie" tell the reader almost nothing. Replace each with what the page actually says the company does. If the page gives a number ("15 lat"), use it. If it doesn't, say it plainly ("od wielu lat") and don't invent one.

**Form of address.** If the site writes "Państwo" (often capitalised in direct address), keep it, including its capitalisation, and use the matching forms: "mogą Państwo", "zapraszamy Państwa". Don't mix it with "ty" verb forms.

**Typography.** Many Polish sites put a non-breaking space after single-letter words (a, i, o, u, w, z, also capitalised) so they don't dangle at the end of a line. If the site does, do it in your text too, using whatever form the file uses (`&nbsp;`, `&#160;`, `\u00a0` in JSON and JS strings, or the literal character). Keep Polish quotes „…”, the en dash "–" for ranges and asides, and a space before currency: "99 zł".

## English

**Nominalizations → verbs**

- "make a payment" → "pay"
- "provide assistance" → "help"
- "carry out an assessment" → "check", "assess"
- "give consideration to" → "consider"

**Passive → active**

- "Payment can be made by card or bank transfer" → "You can pay by card or bank transfer"
- "Your enquiry will be answered within 24 hours" → "We'll answer your enquiry within 24 hours"

**Formal words → everyday words**

| Instead of | Write |
| --- | --- |
| utilise, leverage | use |
| commence | start |
| prior to | before |
| in order to | to |
| purchase | buy |
| assist, facilitate | help |
| approximately | about |
| additional | more, extra |
| in the event that | if |
| subsequently | then, later |
| obtain | get |
| require | need |
| sufficient | enough |
| numerous | many |
| endeavour | try |

**Buzzwords.** "End-to-end solutions", "best-in-class", "seamless", "cutting-edge", "empower" and "synergy" read as noise. Say what the product or service actually does, using only what the page states.

**Conventions.** Follow the site's choices on contractions ("we'll" vs "we will"), British vs American spelling, and the serial comma.

## German

The target here is *Einfache Sprache* (about B1), not *Leichte Sprache* (A1–A2). So don't add Leichte Sprache conventions such as hyphenated or mid-dot-split compounds ("Kunden·zufriedenheit").

**Nominal style → verbs**

- "zur Verfügung stellen" → "geben", "bieten"
- "in Anspruch nehmen" → "nutzen"
- "eine Entscheidung treffen" → "entscheiden"
- "Die Bearbeitung Ihrer Anfrage erfolgt innerhalb von 24 Stunden" → "Wir bearbeiten Ihre Anfrage innerhalb von 24 Stunden"

**Passive → active.** "Ihre Bestellung wird versendet" → "Wir versenden Ihre Bestellung".

**Nested clauses.** Because the verb comes last in subordinate clauses, nesting quickly gets hard to follow. Keep subordinate clauses short and one level deep, and split the rest into separate sentences.

**Long compounds.** Rephrase them instead of splitting them typographically: "Kundenzufriedenheitsumfrage" → "Umfrage zur Zufriedenheit unserer Kunden".

**Form of address.** Keep "Sie" or "du" as the site uses it.

**Typography.** Keep German quotes „…“ and the site's number format ("1.499 €" vs "1 499 €").

## Other languages

The general principles carry over. Most languages have an officialese register built on nominal phrases and formulaic connectors, and that's usually where the difficulty is. Examples: French "procéder à", "dans le cadre de", "afin de"; Spanish "llevar a cabo", "en el marco de", "con el fin de"; Italian "provvedere a", "al fine di".

Keep formality distinctions exactly as the site uses them: vous/tu, usted/tú, Lei/tu.

If you can't write natural B1-level text in a language, tell the user instead of producing stilted text. A clumsy simplification is worse than the original.
