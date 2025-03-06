### Поддержка языков и производительность

- **Llama 3 8B**: Модель от Meta AI, 8 миллиардов параметров, ориентирована на английский язык с умеренной поддержкой русского. Исследования показывают, что она хорошо справляется с английскими задачами (MMLU: 60.4%), но для русского может потребоваться доработка.
- **ruGPT-3.5 13B**: От Sberbank, 13 миллиардов параметров, оптимизирована для русского, с некоторой поддержкой английского, особенно в коде и юридических текстах. Обучена на 300 ГБ текстов на русском, что делает её отличным выбором для русского общения.
- **Vikhr**: Независимая разработка, основана на Mistral 7B, 7 миллиардов параметров, фокусируется на русском и английском, считается передовой для русского по бенчмаркам ([Paper](https://arxiv.org/abs/2405.13929)).
- **Mistral 7B**: От Mistral AI, 7 миллиардов параметров, ориентирована на английский, с ограниченной поддержкой русского. Исследования показывают, что она не является многоязычной моделью ([Medium](https://medium.com/@incle/mistral-7b-is-not-a-multilingual-model-5df3a38b3cc3)).
- **Qwen 7B**: От Alibaba Cloud, 7 миллиардов параметров, многоязычная, с акцентом на китайский и английский, умеренная поддержка русского ([Qwen GitHub](https://github.com/QwenLM/Qwen)).
- **YandexGPT-5-Lite-8B-pretrain**: От Yandex, 8 миллиардов параметров, фокусируется на русском и английском, с контекстом до 32 000 токенов, обучена на 15 триллионах токенов, преимущественно на русском ([Hugging Face](https://huggingface.co/yandex/YandexGPT-5-Lite-8B-pretrain)).

### Актуальность на 2025 год

Все модели актуальны на 2025 год, с регулярными обновлениями от разработчиков. Llama 3 8B и Mistral 7B имеют сильную поддержку в глобальном сообществе, тогда как ruGPT-3.5 13B, Vikhr и YandexGPT-5-Lite-8B-pretrain популярны в российском контексте. Qwen 7B активно развивается, но её фокус на китайский может ограничивать интерес в России.

### Производительность в оздоровительном комплексе

Для оздоровительного комплекса, где гости общаются преимущественно на русском, но также на английском, модели с сильной поддержкой русского, такие как ruGPT-3.5 13B, Vikhr и YandexGPT-5-Lite-8B-pretrain, наиболее подходящи. Они могут обрабатывать запросы, связанные с услугами, расписанием и рекомендациями, с акцентом на русский язык. Llama 3 8B и Mistral 7B могут быть полезны для английских гостей, но потребуют доработки для русского. Qwen 7B подходит для многоязычных сценариев, но может быть менее точной для русского.

### Требования к оборудованию

- **Llama 3 8B**: ~16 ГБ VRAM, эффективна благодаря GQA.
- **ruGPT-3.5 13B**: ~25 ГБ VRAM, больше ресурсов из-за большего размера.
- **Vikhr**: ~16 ГБ VRAM, эффективна, как и Mistral 7B.
- **Mistral 7B**: ~16 ГБ VRAM, известна своей эффективностью.
- **Qwen 7B**: ~16 ГБ VRAM, поддерживает длинные контексты (8K).
- **YandexGPT-5-Lite-8B-pretrain**: ~16 ГБ VRAM, поддерживает контекст до 32K.

### Сложность обучения и обновления

- **Llama 3 8B**: Легко дообучить благодаря популярности и ресурсам, регулярные обновления от Meta AI.
- **ruGPT-3.5 13B**: Требует больше ресурсов для дообучения из-за размера, активная поддержка от Sberbank.
- **Vikhr**: Новая модель, дообучение возможно, но сообщество ещё развивается.
- **Mistral 7B**: Легко дообучить, активная поддержка от Mistral AI.
- **Qwen 7B**: Поддерживает дообучение, активная поддержка от Alibaba Cloud.
- **YandexGPT-5-Lite-8B-pretrain**: Дообучение возможно, инструктированная версия в разработке, поддержка от Yandex.

### Внедрение

Все модели доступны через Hugging Face Transformers и vLLM, что упрощает интеграцию. Llama 3 8B, Mistral 7B и Qwen 7B имеют обширную документацию на английском, тогда как ruGPT-3.5 13B, Vikhr и YandexGPT-5-Lite-8B-pretrain имеют сильную поддержку на русском, что подходит для пользователя.

### Пользовательские отзывы и сообщество

- **Llama 3 8B**: Положительные отзывы в глобальном сообществе, но ограниченные для русского.
- **ruGPT-3.5 13B**: Высоко ценится в российском сообществе за русскую поддержку.
- **Vikhr**: Новая модель, но уже получает положительные отзывы за передовые результаты.
- **Mistral 7B**: Положительные отзывы для английских задач, ограниченные для русского.
- **Qwen 7B**: Популярна в Китае, менее известна в России.
- **YandexGPT-5-Lite-8B-pretrain**: Положительные отзывы в российском сообществе, активное обсуждение на Reddit ([Reddit](https://www.reddit.com/r/LocalLLaMA/comments/1iyk53b/yandexgpt5lite8bpretrain_russia_model/)).

### Дополнительные параметры

- **Контекст длины**: YandexGPT-5-Lite-8B-pretrain (32k) и Llama 3 8B (128k) имеют самые длинные контексты, что полезно для длинных взаимодействий.
- **Лицензия**: Все модели открыты, но ==Llama 3 8B имеет кастомную лицензию, что может ограничивать использование.==

---

**Model Comparison Table for AI Models**

|Model Name|Parameters|Language Support|Russian Performance|English Performance|Context Length|VRAM Requirement (approx.)|Special Features|License|Community Support|
|---|---|---|---|---|---|---|---|---|---|
|Llama 3 8B|8B|Multilingal (English primary)|Moderate|Excellent|128K tokens|16 GB|GQA, long context|Custom commercial|Active from Meta AI|
|ruGPT-3.5 13B|13B|Russian (primary), some English|High|Moderate (specific domains)|Standard|25 GB|Trained on Russian data|Open-source|Active in Russian community|
|Vikhr|7B|Russian and English (bilateral)|High (state-of-the-art)|Good|8192 tokens|16 GB|Adapted tokenizer for Russian|Open-source|Active on Hugging Face|
|Mistral 7B|7B|English (primary), some code generation|Low|Excellent|8192 tokens|16 GB|Efficient, GQA|Apache 2.0|Active from Mistral AI|
|Qwen 7B|7B|Multilingal (Chinese, English, etc.)|Moderate|Excellent|8192 tokens|16 GB|Multilingal support|Apache 2.0|Active from Alibaba Cloud|
|YandexGPT-5-Lite-8B-pretrain|8B|Russian and English, focused on Russian|High|Good|32k tokens|16 GB|Trained on Russian data|Open-source|Active from Yandex|