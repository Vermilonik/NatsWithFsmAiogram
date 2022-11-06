создай .env с внутренностями: `BOT_TOKEN = token`

потом нужно скачать графану и прометеус. после этого нужно запустить всё:
```
prometheus-nats-exporter -varz -jsz=all http://localhost:8222
systemctl start prometheus
sudo -u postgres DATA_SOURCE_NAME="user=postgres host=/var/run/postgresql/ sslmode=disable" ./postgres_exporter
sudo -u grafana grafana-server --config=/etc/grafana/grafana.ini --homepath /usr/share/grafana
nats-server -c server.conf
```
после запуска всех сервисов, нужно создать стрим(mass_bullshit) и консьюмера(aiogram), потом бакет(`nats kv add fsm_states_aiogram —history=5 —storage=file`) и еще один бакет(`nats kv add fsm_data_aiogram —history=5 —storage=file`)

и наконец написать эти 2 команды:
```
pip install -r requirements.txt
python bot.py
```