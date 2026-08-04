# Corporate HR RAG Assistant — Project Journey

## 1. Постановка задачи

**Цель:** создать AI-ассистента, который отвечает сотрудникам на вопросы по внутренним регламентам компании.

<p align="center">
  <img src="docs/images/activity_diagram2.png" alt="HR RAG Flow" width="550">
</p>

---

## 2. Архитектурное решение

### Container Diagram (C4)

Диаграмма контейнеров (C4 Container Diagram) для проекта выглядит следующим образом:

<p align="center">
  <img src="docs/images/container.png" alt="HR RAG Flow" width="550">
</p>

### RAG-архитектура

Архитектура RAG представлена на горизонтальной блок-схеме (pipeline):

<p align="center">
  <img src="docs/images/pipeline.png" alt="HR RAG Flow" width="800">
</p>

---

## 3. Реализация Workflow

Скриншот интерфейса Dify:

<p align="center">
  <img src="docs/images/dify_sandbox.png" alt="HR RAG Flow" width="100%">
</p>

---

## 4. Подготовка базы знаний

При загрузке документов были опробованы различные методики сегментирования, и для каждого типа документа (PDF, TXT) выбрана оптимальная.

<p align="center">
  <img src="docs/images/chunk_settings_for_pdf.png" alt="HR RAG Flow" width="800">
</p>

Документы прошли через процессы chunking и embedding, после чего данные были помещены в векторную базу данных (Vector DB). Ниже — список загруженных и обработанных документов.

<p align="center">
  <img src="docs/images/docs_list.png" alt="HR RAG Flow" width="1000">
</p>

После загрузки и обработки работа с каждым документом была протестирована, а получаемые chunks — проанализированы. Процесс повторялся до тех пор, пока результат не стал удовлетворять начальным условиям проекта.

<p align="center">
  <img src="docs/images/found_testing.png" alt="HR RAG Flow" width="1100">
</p>

Для работы с различными сценариями и для будущего масштабирования системы были созданы и определены метаданные для каждого документа.

<p align="center">
  <img src="docs/images/create_meta.png" alt="HR RAG Flow" width="400">
</p>

<p align="center">
  <img src="docs/images/meta_for_fail.png" alt="HR RAG Flow" width="400">
</p>

В качестве LLM был выбран Gemini 3.6 Flash.

<p align="center">
  <img src="docs/images/LLM_model.png" alt="HR RAG Flow" width="400">
</p>

В LLM были прописаны системный промпт и определены основные переменные.

<p align="center">
  <img src="docs/images/create_promt_and_variables.png" alt="HR RAG Flow" width="400">
</p>

Для объяснения назначения чата было заполнено приветственное сообщение и добавлены примеры вопросов.

<p align="center">
  <img src="docs/images/start_chat.png" alt="HR RAG Flow" width="400">
</p>

---

## 5. Тестирование

Система была протестирована по основным сценариям:

| Вопрос | Результат |
|---|---|
| Лимит гостиницы за рубежом | ✅ |
| Кто согласует 100 000 рублей | ✅ |
| Класс авиабилетов | ✅ |
| Нет данных в базе | ✅ (переадресация в HR) |

Поведение системы при вопросе, информацию по которому можно найти в прилагаемых документах:

<p align="center">
  <img src="docs/images/work_chat.png" alt="HR RAG Flow" width="400">
</p>

Поведение системы при вопросе, выходящем за рамки её компетенции 

<p align="center">
  <img src="docs/images/chat_test_rules.png" alt="HR RAG Flow" width="400">
</p>

TODO например: «Какой лимит компенсации обучения сотрудника в университете?»

**Лимит сообщений.** Поскольку использовалась бесплатная версия API, она ограничена по количеству запросов в сутки. При достижении лимита в чате появляется соответствующее сообщение:

<p align="center">
  <img src="docs/images/quota_limit.png" alt="HR RAG Flow" width="400">
</p>

---

## 6. Итоговая версия

Опубликованное приложение в Dify.
