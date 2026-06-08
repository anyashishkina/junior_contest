# Оценка пешеходной доступности и коммерческой привлекательности городских территорий в Санкт-Петербурге

Рассматриваемые типы бизнеса: кафе, рестораны, фитнес-студии, салоны красоты, стоматологии.
Система предназначена для автоматизированной оценки привлекательности городских локаций для размещения бизнеса. Модель использует открытые данные OpenStreetMap (OSM): точки интереса (POI), пешеходную сеть, здания и транспортную инфраструктуру.

Основные задачи:
1) расчёт пространственных признаков для любой точки в городе;
2) вычисление интегрального коммерческого скора (0–100) для заданного типа бизнеса;
3) кластеризация локаций по типу городской среды;
4) моделирование почасового пешеходного трафика (будни / выходные);
5) генерация бизнес-рекомендаций (ассортимент, позиционирование, риски).

## Запуск проекта 
1) Заупск всех ячеек
2) Оценка произвольного адреса
```
result = evaluate_new_location_unsupervised(
    address="Невский проспект, 28", #впишите свой адрес
    business_type="coffee_shop", #тип бизнеса
    context=fast_context,
    scaler_unsup=scaler_unsup,
    pca_model=pca_model,
    kmeans_model=kmeans_model,
    feature_ranges=feature_ranges,
    cluster_labels=CLUSTER_LABELS,
    with_traffic=True
)

print(f"Оценка привлекательности: {result['commercial_score']} ({result['commercial_class']})")
print(f"Кластер: {result['cluster_label']}")
print(f"Рекомендации: {result['recommendations']['assortment']}")
```
3) Сравнение нескольких локаций
```
addresses = ["Невский проспект, 28", "Лиговский проспект, 50"] #впишите адреса
comparison_df = compare_locations_unsupervised(
    addresses=addresses,
    business_type="coffee_shop",
    context=fast_context,
    scaler_unsup=scaler_unsup,
    pca_model=pca_model,
    kmeans_model=kmeans_model,
    feature_ranges=feature_ranges,
    cluster_labels=CLUSTER_LABELS,
    show_plots=True
)
```
4) Визуализация трафика
```
plot_traffic_profile(
    result['traffic_weekday'],
    result['traffic_weekend'],
    title=f"Профиль трафика - {address}"
)
```
