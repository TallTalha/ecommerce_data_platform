# ecommerce_data_platform

```plaintext
                                      +---------------------------------+
                               +----->|   Spark Streaming Job           |-----> [ MongoDB ]
                               |      | (frontend-events işleme)        |      (Kullanıcı Etkileşim Profilleri)
                               |      +---------------------------------+
[Owl Shop Aracı] -> [Apache Kafka Konuları]
(Veri Üretimi)     (Merkezi Sinir Sistemi)
                               |      +---------------------------------+
                               +----->|   Spark Batch Job               |-----> [ Data Lake (Parquet) ]
                                      | (orders, customers işleme)      |      (Tarihsel Analiz Deposu)
                                      |   (Orchestrated by Airflow)     |
                                      +---------------------------------+

```
/div
```plaintext
ecommerce_data_platform/
├── dags/ # Airflow DAG dosyalarımız burada yaşayacak
│ └── process_daily_data.py
├── data/ # Lokal Veri Gölümüz. Spark işlerinin sonuçları (Parquet) buraya yazılacak.
│ └── processed/
│ ├── customer_profiles/
│ └── sales_reports/
├── docker-compose.yml # Tek komutla tüm altyapıyı (Kafka, Mongo, Airflow vb.) başlatan dosya
├── notebooks/ # Keşifsel veri analizi ve denemeler için Jupyter Notebook'lar
│ └── initial_data_exploration.ipynb
├── spark_jobs/ # Spark ile yazacağımız veri işleme betiklerimiz
│ ├── streaming_frontend_events.py
│ └── batch_process_orders.py
├── configs/ # Konfigürasyon dosyaları
│ └── owl_shop_config.yaml
└── README.md # Projenin ne yaptığını ve nasıl çalıştırılacağını anlatan ana dosya
```