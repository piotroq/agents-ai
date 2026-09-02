# Plan stworzenia strony internetowej

Plan zakłada dostarczenie działającej, publicznie dostępnej strony w ramach jednego 6-dniowego sprintu, zgodnie z filozofią studia. Każdy etap ma przypisanych agentów z tego repozytorium, którzy wykonują lub wspierają pracę.

## 1. Cel i założenia

Przed rozpoczęciem pracy należy odpowiedzieć na pięć pytań:

| Pytanie | Przykładowa odpowiedź |
|---|---|
| Po co powstaje strona? | Prezentacja produktu / firmy, zbieranie leadów, sprzedaż |
| Kto jest odbiorcą? | Konkretna persona: kim jest, z jakiego urządzenia korzysta, co chce osiągnąć |
| Jaka jest główna akcja (CTA)? | Zapis do newslettera, formularz kontaktowy, zakup, pobranie aplikacji |
| Jak zmierzymy sukces? | Konwersja CTA, czas na stronie, ruch organiczny, Core Web Vitals |
| Co jest poza zakresem MVP? | Panel klienta, blog z CMS, wielojęzyczność, płatności |

Agenci: `trend-researcher` (analiza rynku i konkurencji), `ux-researcher` (persony, ścieżki użytkownika), `sprint-prioritizer` (cięcie zakresu do MVP).

## 2. Zakres MVP

Typowa struktura strony firmowej / produktowej:

- **Strona główna** – hero z propozycją wartości i CTA, sekcja korzyści, dowód społeczny (opinie, logotypy), FAQ, stopka.
- **O nas / Produkt** – szczegółowy opis oferty.
- **Kontakt** – formularz (nazwa, e-mail, wiadomość) z walidacją i ochroną antyspamową.
- **Strony prawne** – polityka prywatności, regulamin, informacja o cookies (wymagane przez RODO).
- **Strona 404** i podstawowe SEO (meta tagi, Open Graph, `sitemap.xml`, `robots.txt`).

Wszystko, co nie mieści się w tej liście, trafia do backlogu na kolejny sprint.

## 3. Stack technologiczny

Rekomendacja domyślna (można zamienić na inny, jeśli zespół ma silniejsze kompetencje):

| Warstwa | Wybór | Uzasadnienie |
|---|---|---|
| Framework | Next.js (App Router) lub Astro | SSG/SSR, świetne SEO, duży ekosystem; Astro dla stron głównie statycznych |
| Język | TypeScript | Bezpieczeństwo typów, lepsza współpraca z agentami |
| Stylowanie | Tailwind CSS + shadcn/ui | Szybkie budowanie spójnego UI |
| Treść | MDX lub headless CMS (np. Sanity, Contentful) | MDX na start, CMS gdy treść ma edytować marketing |
| Formularze | Server Actions / Route Handler + Resend (e-mail) | Brak osobnego backendu |
| Hosting | Vercel lub Cloudflare Pages | Deploy z Gita, preview na PR, CDN, HTTPS |
| Analityka | Plausible / Umami lub GA4 | Pomiar konwersji i ruchu |
| Jakość | ESLint, Prettier, Playwright, Lighthouse CI | Automatyczna kontrola jakości |

Agenci: `backend-architect` (decyzje architektoniczne, integracje), `tool-evaluator` (porównanie narzędzi, jeśli stack jest sporny).

## 4. Harmonogram sprintu (6 dni)

### Dzień 1 – Discovery i fundament

- Warsztat z interesariuszami: cel, persona, CTA, metryki (sekcja 1).
- Audyt 3–5 stron konkurencji.
- Architektura informacji: mapa strony, lista sekcji, szkielet treści.
- Scaffold projektu: repozytorium, framework, TypeScript, lint, formatowanie, CI, pierwszy deploy „Hello world” na hosting.

Agenci: `trend-researcher`, `ux-researcher`, `sprint-prioritizer`, `rapid-prototyper`, `devops-automator`.

Rezultat: zatwierdzony zakres MVP i pusty projekt działający na publicznym URL.

### Dzień 2 – Design

- Design system: kolory, typografia, spacing, komponenty bazowe (przycisk, karta, formularz, nawigacja).
- Makiety low-fi wszystkich stron, potem hi-fi strony głównej.
- Weryfikacja zgodności z identyfikacją marki.
- Przygotowanie grafik (hero, ilustracje, OG image).

Agenci: `ui-designer`, `brand-guardian`, `visual-storyteller`, `whimsy-injector` (mikrointerakcje, stany puste, 404).

Rezultat: zaakceptowane makiety i biblioteka komponentów w kodzie (Storybook opcjonalnie).

### Dzień 3 – Implementacja: layout i strona główna

- Layout globalny: nagłówek, nawigacja (w tym mobilna), stopka.
- Implementacja strony głównej sekcja po sekcji na podstawie makiet.
- Responsywność (mobile-first), tryb ciemny jeśli w zakresie.
- Podpięcie treści (MDX/CMS).

Agenci: `frontend-developer`, `rapid-prototyper`, `content-creator` (docelowe teksty zamiast lorem ipsum).

Rezultat: strona główna gotowa do przeglądu na preview URL.

### Dzień 4 – Implementacja: pozostałe strony i integracje

- Podstrony: O nas / Produkt, Kontakt, strony prawne, 404.
- Formularz kontaktowy: walidacja, wysyłka e-mail, ochrona antyspamowa (honeypot / Turnstile), komunikaty sukcesu i błędu.
- Baner cookies i zgody na analitykę.
- SEO: metadane per strona, Open Graph, dane strukturalne (JSON-LD), `sitemap.xml`, `robots.txt`.
- Analityka z eventami dla CTA.

Agenci: `frontend-developer`, `backend-architect`, `legal-compliance-checker` (RODO, cookies, treść polityki prywatności), `ai-engineer` (jeśli w zakresie jest np. chatbot lub generowanie treści).

Rezultat: wszystkie strony MVP działają na preview.

### Dzień 5 – Jakość, wydajność, dostępność

- Testy E2E krytycznych ścieżek (Playwright): nawigacja, wysyłka formularza, 404.
- Audyt Lighthouse: cel ≥ 90 w każdej kategorii; Core Web Vitals w zieleni (LCP < 2,5 s, INP < 200 ms, CLS < 0,1).
- Optymalizacja obrazów (`next/image` / formaty AVIF/WebP), fontów (self-hosting, `font-display: swap`), bundle size.
- Dostępność (WCAG 2.1 AA): kontrast, nawigacja klawiaturą, etykiety formularzy, alt-teksty, semantyczny HTML.
- Testy cross-browser i na realnych urządzeniach mobilnych.
- Naprawa wszystkich znalezionych błędów.

Agenci: `test-writer-fixer`, `performance-benchmarker`, `api-tester` (endpoint formularza), `test-results-analyzer`.

Rezultat: raport jakości bez blokerów, zielony pipeline CI.

### Dzień 6 – Wdrożenie i start

- Konfiguracja domeny produkcyjnej, DNS, HTTPS, przekierowania (www ↔ bez www, http → https).
- Zmienne środowiskowe produkcyjne, monitoring uptime i błędów (np. Sentry), alerty.
- Ostatnia korekta treści, weryfikacja linków i formularza na produkcji.
- Zgłoszenie do Google Search Console i Bing Webmaster Tools, przesłanie sitemap.
- Publikacja i komunikacja startu (social media, newsletter).
- Retrospektywa sprintu i backlog na kolejną iterację.

Agenci: `devops-automator`, `project-shipper`, `infrastructure-maintainer`, `content-creator`, `twitter-engager` / `instagram-curator` (komunikacja startu), `studio-producer` (retrospektywa).

Rezultat: strona dostępna pod docelową domeną z działającym monitoringiem.

## 5. Po starcie (kolejne sprinty)

- **Tydzień 1–2**: analiza danych z analityki i nagrań sesji, zbieranie opinii użytkowników, szybkie poprawki.
- **Eksperymenty**: testy A/B nagłówka i CTA za pomocą feature flag.
- **Treść i SEO**: blog / baza wiedzy, strategia słów kluczowych, link building.
- **Rozszerzenia**: wielojęzyczność, CMS dla marketingu, integracja z CRM, panel klienta.

Agenci: `analytics-reporter`, `feedback-synthesizer`, `experiment-tracker`, `growth-hacker`, `support-responder`, `finance-tracker` (koszty hostingu i narzędzi).

## 6. Definicja ukończenia (Definition of Done)

Strona jest gotowa do publikacji, gdy:

- [ ] Wszystkie strony z zakresu MVP są wdrożone i zatwierdzone przez interesariuszy
- [ ] Treść jest finalna (brak placeholderów), sprawdzona językowo
- [ ] Formularz kontaktowy dostarcza wiadomości i ma ochronę antyspamową
- [ ] Lighthouse ≥ 90 w kategoriach Performance, Accessibility, Best Practices, SEO
- [ ] Testy E2E przechodzą w CI
- [ ] Strona działa poprawnie w Chrome, Safari, Firefox, Edge oraz na iOS i Androidzie
- [ ] Polityka prywatności, regulamin i baner cookies są wdrożone i zgodne z RODO
- [ ] Domena, HTTPS, przekierowania i monitoring są skonfigurowane
- [ ] Sitemap przesłana do Google Search Console
- [ ] Analityka rejestruje odsłony i zdarzenia CTA

## 7. Ryzyka i sposoby ich ograniczenia

| Ryzyko | Skutek | Mitygacja |
|---|---|---|
| Brak finalnych treści od klienta | Blokada implementacji | `content-creator` przygotowuje wersję roboczą w dniu 1–2; treść klienta podmieniana później |
| Rozrost zakresu w trakcie sprintu | Brak wdrożenia w dniu 6 | `sprint-prioritizer` zarządza backlogiem; nowe pomysły trafiają do kolejnego sprintu |
| Opóźnienie akceptacji makiet | Przesunięcie implementacji | Akceptacja etapowa (low-fi w dniu 1, hi-fi w dniu 2), implementacja komponentów równolegle |
| Problemy z wydajnością na końcu | Poprawki w ostatniej chwili | Lighthouse CI od pierwszego deployu, budżet wydajności zdefiniowany w dniu 1 |
| Braki zgodności z RODO | Ryzyko prawne | `legal-compliance-checker` weryfikuje w dniu 4, nie po starcie |
| Brak dostępu do domeny/DNS | Brak startu na docelowym adresie | Weryfikacja dostępów w dniu 1 |

## 8. Przykładowe polecenia dla agentów

- „Przeanalizuj 5 stron konkurencji w branży X i wskaż, co robią dobrze” → `trend-researcher`
- „Zaprojektuj design system dla strony marki Y w oparciu o brand book” → `ui-designer`, `brand-guardian`
- „Postaw projekt Next.js z Tailwind, TypeScript i deployem na Vercel” → `rapid-prototyper`
- „Zaimplementuj sekcję hero według makiety, mobile-first” → `frontend-developer`
- „Dodaj formularz kontaktowy z wysyłką e-mail i ochroną antyspamową” → `backend-architect`, `frontend-developer`
- „Sprawdź stronę pod kątem RODO i przygotuj politykę prywatności” → `legal-compliance-checker`
- „Napisz testy E2E dla formularza i nawigacji” → `test-writer-fixer`
- „Zoptymalizuj LCP na stronie głównej” → `performance-benchmarker`
- „Skonfiguruj domenę, monitoring i ogłoś start” → `devops-automator`, `project-shipper`
