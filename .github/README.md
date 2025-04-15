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

## Крок 5: Ручний запуск Workflow

### Додано можливість ручного запуску:

```yaml
on:
  push:
    branches: [ "main" ]
  workflow_dispatch:
```

## Крок 6: Cron запуск за розкладом

```yaml
on:
  schedule:
    - cron: '30 12 * * 1'  # кожен понеділок о 12:30
```

## Крок 7: Декілька Workflow

Створено два окремі Workflow з іменами:

- `python-app.yml`
- `manual-workflow.yml`

Кожен з них відображається у вкладці **Actions** на GitHub.

## Крок 8: Декілька Jobs

```yaml
jobs:
  name_one:
    name: Run first Job
    runs-on: ubuntu-latest
    steps:
      - name: First
        run: echo "First"
  name_two:
    name: Run Second Job
    runs-on: ubuntu-latest
    steps:
      - name: Second
        run: echo "Second"
```

## Крок 9: Умовне виконання

```yaml
- name: Send greeting
  run: echo "Hello ${{ github.event.inputs.name }}"
  if: github.event.inputs.name != 'Executer'
```

## Крок 10: Бейджі у README.md

```md
![Python application](https://github.com/Kaena0/actions/actions/workflows/python-app.yml/badge.svg)
```

##

