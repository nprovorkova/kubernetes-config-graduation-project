### Подготовка cистемы мониторинга и деплой приложения
#### Подготовить конфигурационные файлы для настройки нашего Kubernetes кластера
* Воспользовать пакетом kube-prometheus, который уже включает в себя Kubernetes оператор для grafana, prometheus, alertmanager и node_exporter. При желании можете собрать все эти приложения отдельно.
* Для организации конфигурации использовать qbec, основанный на jsonnet. Обратите внимание на имеющиеся функции для интеграции helm конфигов и helm charts
* Если на первом этапе вы не воспользовались Terraform Cloud, то задеплойте в кластер atlantis для отслеживания изменений инфраструктуры.

#### Ожидаемые результаты:
* Git репозиторий с конфигурационными файлами для настройки Kubernetes.
* Http доступ к web интерфейсу grafana.
* Дашборды в grafana отображающие состояние Kubernetes кластера.
* Http доступ к тестовому приложению.

#### Команды:
mkdir kube-prometheus; cd my-kube-prometheus
<br>jb init
<br>jb install github.com/prometheus-operator/kube-prometheus/jsonnet/kube-prometheus@main
<br>wget https://raw.githubusercontent.com/prometheus-operator/kube-prometheus/main/example.jsonnet -O example.jsonnet
<br>wget https://raw.githubusercontent.com/prometheus-operator/kube-prometheus/main/build.sh -O build.sh
<br>chmod +x build.sh
<br>./build.sh prometheus.jsonnet
<br>kubectl apply --server-side -f manifests/setup
<br>kubectl apply -f manifests/
<br>kubectl get pods -n monitoring
