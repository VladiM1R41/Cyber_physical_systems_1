# Лабораторная работа 1: классификация видов бабочек

> Студент: **Ляхов Владимир**  
> Группа: **М8О-403Б-22**  
> Вариант: **на 5**

## О работе

В репозитории находится решение лабораторной работы по исследованию моделей классификации изображений.  
Задача работы — распознавание видов бабочек по изображению в постановке многоклассовой классификации.

Работа включает:

- выбор и анализ датасета;
- обучение baseline-моделей из `torchvision`;
- улучшение baseline с помощью гипотез;
- самостоятельную реализацию CNN- и transformer-моделей;
- сравнение всех результатов по единым метрикам.

Основной результат оформлен в ноутбуке:

- `lab1_butterfly_classification.ipynb`

## Датасет

Используется датасет **Butterfly Classification Dataset**:

- Kaggle: https://www.kaggle.com/datasets/pnkjgpt/butterfly-classification-dataset

Почему он выбран:

- задача имеет практический смысл для биомониторинга и анализа биоразнообразия;
- датасет подходит для многоклассовой классификации;
- в нём много визуально похожих классов, что делает задачу нетривиальной.

В работе используется локальная папка `Train/`, сформированная из изображений датасета.

Характеристики используемой выборки:

- `50` классов;
- `4479` изображений;
- стратифицированное разбиение `train / val / test = 70 / 15 / 15`.

## Метрики качества

В работе используются:

- `accuracy`
- `precision_macro`
- `recall_macro`
- `f1_macro`
- `top-3 accuracy`

Основной метрикой сравнения выступает `f1_macro`, так как она лучше отражает качество многоклассовой классификации по всем классам сразу.

## Какие модели использовались

### Модели из `torchvision`

- `ResNet18` — baseline сверточная модель
- `Swin_T` — baseline трансформерная модель

### Самостоятельно реализованные модели

- `CustomResNet` — собственная residual-CNN
- `SimpleViT` — собственная упрощённая vision transformer модель

## Итоговые результаты

### Baseline-модели

| Модель | Accuracy | Precision Macro | Recall Macro | F1 Macro | Top-3 Accuracy |
|---|---:|---:|---:|---:|---:|
| `swin_t` | 0.894345 | 0.901206 | 0.894192 | 0.892888 | 0.968750 |
| `resnet18` | 0.812500 | 0.834966 | 0.814340 | 0.809934 | 0.918155 |

### Улучшенные baseline-модели

| Модель | Accuracy | Precision Macro | Recall Macro | F1 Macro | Top-3 Accuracy |
|---|---:|---:|---:|---:|---:|
| `swin_t_improved` | 0.936012 | 0.941218 | 0.937160 | 0.935731 | 0.980655 |
| `resnet18_improved` | 0.921131 | 0.926501 | 0.923186 | 0.922602 | 0.965774 |

### Самостоятельно реализованные модели

| Модель | Accuracy | Precision Macro | Recall Macro | F1 Macro | Top-3 Accuracy |
|---|---:|---:|---:|---:|---:|
| `custom_resnet` | 0.550595 | 0.591259 | 0.553477 | 0.531000 | 0.800595 |
| `simple_vit` | 0.497024 | 0.522066 | 0.494284 | 0.479405 | 0.735119 |

### Улучшенные самостоятельно реализованные модели

| Модель | Accuracy | Precision Macro | Recall Macro | F1 Macro | Top-3 Accuracy |
|---|---:|---:|---:|---:|---:|
| `custom_resnet_improved` | 0.708333 | 0.734736 | 0.703668 | 0.699325 | 0.901786 |
| `simple_vit_improved` | 0.569940 | 0.600517 | 0.567202 | 0.556263 | 0.827381 |

### Сводная таблица

| Группа моделей | Лучшая модель | F1 Macro |
|---|---|---:|
| Baseline `torchvision` | `swin_t` | 0.892888 |
| Improved baseline | `swin_t_improved` | 0.935731 |
| Собственные модели | `custom_resnet` | 0.531000 |
| Improved собственные модели | `custom_resnet_improved` | 0.699325 |

## Краткие выводы по работе

- Среди baseline-моделей лучшей оказалась `Swin_T`.
- Улучшение baseline дало заметный прирост для обеих `torchvision`-моделей.
- Наилучший итоговый результат показала модель `swin_t_improved` с `f1_macro = 0.935731`.
- Самостоятельно реализованные модели оказались слабее готовых моделей из `torchvision`, что ожидаемо из-за более простой архитектуры и обучения с нуля.
- Перенос техник improved baseline помог и для собственных моделей:
  - `CustomResNet`: `f1_macro` вырос с `0.5310` до `0.6993`
  - `SimpleViT`: `f1_macro` вырос с `0.4794` до `0.5563`

## Структура репозитория

- `lab1_butterfly_classification.ipynb` — основной ноутбук с полным решением
- `Train/` — локальная папка с изображениями датасета
- `requirements.txt` — зависимости проекта
- `Lab_tasks.pdf` — формулировка задания

## Требования

- Python `3.10+`
- GPU не обязателен, но ускоряет обучение

## Инструкция по установке и запуску

### 1. Клонирование репозитория

```powershell
git clone https://github.com/VladiM1R41/Cyber_physical_systems_1.git
cd Cyber_physical_systems_1
```

### 2. Создание виртуального окружения

PowerShell:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

CMD:

```bat
python -m venv .venv
.venv\Scripts\activate.bat
```

### 3. Установка зависимостей

```powershell
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Подготовка датасета

Если папка `Train/` уже есть в репозитории, этот шаг можно пропустить.

Если папки `Train/` нет:

1. скачать датасет по ссылке Kaggle;
2. распаковать архив;
3. поместить папку с обучающими изображениями в корень проекта;
4. при необходимости переименовать папку `TRAIN` в `Train`, чтобы структура совпадала с ноутбуком.

Ожидаемая структура:

```text
Cyber_physical_systems_1/
  Train/
    adonis/
    american snoot/
    ...
  lab1_butterfly_classification.ipynb
  requirements.txt
  README.md
```

### 5. Опционально: запуск на GPU

Если на компьютере есть NVIDIA GPU и установлен совместимый драйвер, можно поставить CUDA-сборку PyTorch:

```powershell
pip uninstall -y torch torchvision
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu128
```

Проверка:

```powershell
python -c "import torch; print(torch.__version__); print(torch.cuda.is_available())"
```

Если выводит `True`, ноутбук будет использовать GPU автоматически.

### 6. Запуск ноутбука

```powershell
jupyter notebook
```

После запуска нужно открыть файл:

- `lab1_butterfly_classification.ipynb`

И выполнять ячейки сверху вниз.
