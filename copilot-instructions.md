# GitHub Copilot Instructions - Mailer Project

## 1. Python i Zależności
- Python 3.9+
- Używaj `venv` lub innego virtual environment
- Linting: `flake8`, `black`
- Type hints obowiązkowe dla nowych funkcji i metod
- `requirements.txt` musi być aktualny
- Unikaj używania zewnętrznych pakietów bez uzasadnienia

## 2. Struktura kodu
- Moduły: max 500 linii
- Funkcje: max 50 linii
- Klasy: pojedyncza odpowiedzialność
- Separacja logiki biznesowej od warstwy web
- MVC dla warstwy Flask
- Pliki HTML/CSS/JS w `templates/` i `static/`

## 3. Code Style
- Przestrzegaj PEP 8
- Formatowanie za pomocą `black`
- Dokumentuj klasy i funkcje w formacie Google Docstring
- Waliduj wszystkie dane wejściowe
- Unikaj hardcodowanych sekretów i danych wrażliwych

## 4. Testy
- Minimum 80% coverage
- Używaj `pytest` i `pytest-cov`
- Wszystkie funkcje muszą mieć testy
- Mockuj zewnętrzne usługi, np. SMTP
- Testuj edge case'y i obsługę błędów
- Testy umieszczaj w katalogu `tests/`

## 5. Bezpieczeństwo
- Brak credentials w kodzie i repozytorium
- Secrets w environment variables
- Waliduj użytkownika i dane wejściowe
- Waliduj format emaili przed użyciem
- Zabezpiecz formularze Flask przed XSS
- Nie używaj zapytań do bazy bez odpowiedniej walidacji

## 6. Git i PR
- Commity: conventional commits
- Nazwy branchy: `feature/*`, `bugfix/*`, `docs/*`
- PR: opisane, z testami, związek z taskiem
- Nie commituj kodu niedziałającego
- Przed merge uruchom testy i lint

## 7. Komponenty projektu
- `mailer/` – logika biznesowa i usługi email
- `templates/` – pliki HTML Flask
- `static/` – CSS, JavaScript, zasoby frontendu
- `tests/` – testy jednostkowe i integracyjne

## 8. Testing Strategy
- Use `Mailer Complete Testing Skill` dla szczegółów
- Każda funkcja: min. 2 testy
- Edge cases i error handling
- Mock external services
- Coverage: min. 80%
- Preferuj testy parametryzowane i izolowane
