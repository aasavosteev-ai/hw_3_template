На 4 балла

КОД
sudo docker build -t programm ./app

sudo docker run -d --name counter \
  -p 8080:8000 \
  -e PORT=8000 \
  -e GREETING="Hello from Compose!" \
  -e STORAGE=sqlite \
  -e DATA_FILE=/data/counter.db \
  programm

ПРОВЕРКИ
curl -fsS http://127.0.0.1:8080/
{"greeting": "Hello from Compose!", "count": 0, "hostname": ..., "storage": "sqlite"}
curl -fsS -X POST http://127.0.0.1:8080/increment
{"greeting": "Hello from Compose!", "count": 1, "hostname": ..., "storage": "sqlite"}
Увеличение счётчика произошло. Приветствие передано.

На 6 баллов

Отдельно есть файл compose.yaml, в котором представлена compose
КОД
cp .env.example .env
docker compose up -d --build

curl -fsS -X POST http://127.0.0.1:8080/increment
{"greeting": "Hello from Compose!", "count": 1, "hostname": ..., "storage": "sqlite"}
curl -fsS -X POST http://127.0.0.1:8080/increment
{"greeting": "Hello from Compose!", "count": 2, "hostname": ..., "storage": "sqlite"}

docker compose down
docker compose up -d

curl -fsS http://127.0.0.1:8080/
{"greeting": "Hello from Compose!", "count": 2, "hostname": ..., "storage": "sqlite"}
Счётчик сохранился после удаления и повторного создания контейнера.
