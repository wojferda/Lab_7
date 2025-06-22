
# Sprawozdanie nr 7  
**Autor:** Wojciech Ferda  

---

## 1. Stworzenie roboczego branch’a

Na początku pracy stworzyłem nową gałąź roboczą (`dev`), aby nie modyfikować bezpośrednio głównego branch’a (`main`). Dzięki temu mogę bezpiecznie pracować nad funkcjonalnościami, a ewentualne błędy nie wpłyną na główną wersję projektu.

```bash
git checkout -b dev
```

---

## 2. Skopiowanie zawartości folderu `env_0000`

Aby przygotować środowisko do zadania, skopiowałem folder bazowy `env_0000` do nowego folderu o nazwie `env_416796`, w którym mogłem wprowadzać zmiany niezależnie od oryginału.

```bash
cp -r env_0000 env_416796
```

---

## 3. Stworzenie własnego repozytorium

Za pomocą polecenia `git init` zainicjowałem nowe repozytorium w katalogu projektu, a następnie dodałem zdalne repozytorium hostowane na GitLabie:

```bash
git init
git remote add origin https://gitlab.com/użytkownik/moje-repo.git
```

---

## 4. Dodanie i spushowanie repozytorium

Następnie dodałem pliki do Gita, zatwierdziłem pierwszy commit i wypchnąłem repozytorium do zdalnego serwera:

```bash
git add .
git commit -m "Initial commit"
git push -u origin dev
```

---

## 5. Dodanie folderu `env_416796` do repozytorium

Upewniłem się, że katalog `env_416796` nie jest pomijany przez `.gitignore` i został prawidłowo dodany do systemu kontroli wersji. Jeśli folder był pusty, dodałem do niego plik `.gitkeep`, aby Git go nie zignorował:

```bash
touch env_416796/.gitkeep
git add env_416796
git commit -m "Dodano folder env_416796"
git push
```

---

## 6. Stworzenie i modyfikacja pliku `.gitlab-ci.yml`

W celu automatyzacji procesu testowania utworzyłem plik `.gitlab-ci.yml`, który definiuje pipeline CI/CD. Pipeline zawiera jedną fazę `test`, która uruchamia testy za pomocą `pytest`.

```yaml
stages:
  - test

test_job:
  stage: test
  script:
    - pip install -r requirements.txt
    - pytest
```

---

## 7. Edycja skryptu `calculator.py`

Do skryptu `calculator.py` dodałem dodatkowe funkcje matematyczne oraz obsługę wyjątków. Przykład jednej z dodanych funkcji:

```python
def divide(a, b):
    if b == 0:
        raise ValueError("Division by zero")
    return a / b
```

---

## 8. Dodanie testów w `calculator_test.py`

Dla każdej funkcji zdefiniowałem odpowiadające testy jednostkowe z użyciem `pytest`. Testy sprawdzają poprawność wyników oraz odpowiednie zachowanie w sytuacjach wyjątkowych:

```python
def test_divide():
    assert divide(6, 2) == 3

def test_divide_by_zero():
    with pytest.raises(ValueError):
        divide(5, 0)
```

---

## 9. Dodanie skryptów na repozytorium

Po zakończeniu prac nad kodem i testami, wszystkie zmiany zostały zatwierdzone i wypchnięte do zdalnego repozytorium:

```bash
git add .
git commit -m "Dodano funkcje i testy"
git push
```

---

## 10. Uruchomienie testów przez pipeline

Pipeline uruchomił się automatycznie po każdym wypchnięciu zmian do repozytorium. Wszystkie testy zostały wykonane poprawnie, co oznacza, że implementacja działa zgodnie z założeniami.



## Podsumowanie

W ramach zadania:
- stworzyłem i skonfigurowałem własne repozytorium Git,
- utworzyłem środowisko pracy,
- zdefiniowałem plik CI/CD uruchamiający testy automatyczne,
- zaimplementowałem funkcje matematyczne i testy jednostkowe,
- wypchnąłem projekt na zdalne repozytorium z przechodzącym pipeline’em.

Projekt został zrealizowany zgodnie z wymaganiami.
