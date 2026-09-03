# Примеры структуры Knowledge Base

[English version](README.md)

В этой папке находятся синтетические примеры записей, аналогичных тем, которые использовались в Knowledge Base проекта **beFruitbe AI Content Pipeline**.

## Важно

Эти файлы:

- не содержат реальных закрытых данных beFruitbe;
- не раскрывают фактический состав продуктов;
- не содержат внутренние claims компании;
- не содержат реальные SKU;
- не содержат конфиденциальные материалы или интервью.

Цель этих примеров — показать **структуру данных и принципы проектирования Knowledge Base**, не публикуя внутреннюю информацию компании.

---

## Что здесь показано

### SKU Example

[`sample-sku-ru.md`](sample-sku-ru.md)

Показывает, как могла быть структурирована информация о конкретном продукте:

- идентификация;
- факты;
- состав;
- статус данных;
- claims;
- связанные assets;
- права на использование.

### Claim Example

[`sample-claim-ru.md`](sample-claim-ru.md)

Показывает, как продуктовые утверждения отделялись от обычного текста и получали статус:

- APPROVED;
- DRAFT;
- CONFIRMATION REQUIRED;
- NOT ALLOWED.

### Document Metadata Example

[`sample-document-metadata-ru.md`](sample-document-metadata-ru.md)

Показывает, как можно управлять:

- версиями документов;
- владельцами информации;
- статусами;
- scope;
- разрешениями на AI-использование;
- публичностью;
- архивными версиями.

---

## Основной принцип

Knowledge Base проектировалась так, чтобы AI работал не с набором случайных файлов, а со структурированным контекстом.

Упрощённо:

```text
User Request
       ↓
Identify Relevant Product / Context
       ↓
Retrieve Verified Facts
       ↓
Check Claims & Restrictions
       ↓
Retrieve Approved Assets
       ↓
Generate AI Output
       ↓
Human Verification where required
