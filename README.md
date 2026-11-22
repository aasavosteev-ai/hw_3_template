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
curl -s http://127.0.0.1:8080
curl -s -X POST http://127.0.0.1:8080/increment
