# Email Templates Skill

## Cel umiejętności
Skill wspiera projektowanie, implementację i testowanie szablonów email w aplikacji Mailer. Obejmuje zarówno szablony HTML, jak i tekstowe, zmienne, dziedziczenie oraz przypadki użycia.

## Kontekst
- Projekt: Mailer
- Funkcjonalność: Email Templates
- Wymagania: szablony powiadomień, newsletterów, potwierdzeń
- Środowisko: Flask, Jinja2, Python

## Tematy do pokrycia
- Template inheritance
- Variable substitution
- HTML/Plain text templates
- Template testing
- Przykłady: Welcome, Confirmation, Newsletter

## Wzorzec użytkowania
Szablony powinny być podzielone na bazowy layout i konkretne wiadomości. Przykład:

```jinja
{# templates/base_email.html #}
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>{{ subject }}</title>
</head>
<body>
  <header>
    <h1>{{ header_text }}</h1>
  </header>
  <main>
    {% block content %}{% endblock %}
  </main>
  <footer>
    <p>{{ footer_text }}</p>
  </footer>
</body>
</html>
```

```jinja
{# templates/welcome_email.html #}
{% extends "base_email.html" %}

{% block content %}
<p>Witaj {{ user_name }},</p>
<p>Dziękujemy za rejestrację.</p>
{% endblock %}
```

## Pattern: Variable substitution
- Używaj bezpiecznego renderowania Jinja2
- Unikaj wstrzykiwania HTML bez sanitizacji
- Zmienna `{{ variable }}` powinna mieć fallback lub walidację

## Pattern: HTML i Plain text
- Dla HTML: `templates/*.html`
- Dla plain text: `templates/*.txt`
- Zawsze dostarczaj alternatywę tekstową do wiadomości email

## Pattern: Template inheritance
- Centralny plik `base_email.html`
- Nagłówek, stopka i blok `content`
- Specyficzne szablony rozszerzają bazę

## Pattern: Template testing
- Testy powinny weryfikować:
  - poprawne renderowanie zmiennych
  - obecność wymaganych fragmentów
  - brak niebezpiecznych elementów
  - czy HTML i tekst są spójne

### Przykład testu
```python
from jinja2 import Environment, FileSystemLoader

class TestEmailTemplates:
    @pytest.fixture
    def env(self):
        return Environment(loader=FileSystemLoader("templates"))

    def test_welcome_template_renders(self, env):
        template = env.get_template("welcome_email.html")
        content = template.render(user_name="Jan", subject="Witaj", header_text="Cześć", footer_text="Dziękujemy")

        assert "Witaj Jan" in content
        assert "Dziękujemy za rejestrację" in content
```

## Przykłady szablonów
- Welcome email: powitanie nowego użytkownika
- Confirmation email: potwierdzenie subskrypcji
- Newsletter: dynamiczna treść i zmienne

## Reguły
- Używaj jednoznacznych nazw zmiennych
- Unikaj logiki biznesowej w szablonach
- Testuj renderowanie z danymi edge case
- Dokumentuj dostępne zmienne template
