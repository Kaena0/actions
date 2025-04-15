# Автоматизація тестування з GitHub Actions

## Крок 1: Створення репозиторію
Створено GitHub-репозиторій `actions`, що містить три файли:
- `app.py`
- `test_app.py`
- `.github/workflows/python-app.yml`

## Крок 2: Створення файлів

### `app.py`
```python
class Figure:
    def __init__(self, type, length) -> None:
        assert length > 0, "Довжина має бути більшою за 0!"
        assert type in ["квадрат", "прямокутник", "трикутник"], "Дозволені фігури: квадрат, прямокутник, трикутник"
        self.type = type
        self.length = length

    def get_angles(self):
        if self.type == "трикутник":
            return 3
        return 4
```

### `test_app.py`
```python
from app import Figure

def test_get_angles():
    fig = "трикутник"
    triangle = Figure(fig, 1)
    assert triangle.get_angles() == 3, f"У {fig} має бути 3 кути!"
```

### `.github/workflows/python-app.yml`
```yaml
name: Python application

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.11'
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install pytest
    - name: Run tests
      run: |
        pytest
```

## Крок 3: Перевірка роботи

1. Заробили commit і push
2. Перейшли у вкладку **Actions**
3. Вибрали "Python application" і перевірили статус **build: passing**

## Крок 4: README.md

Створили файл `README.md` з коротким описом проєкту.

---

## Готово!
Проєкт автоматично проганяє тести при кожному push/pull request до `main`.


