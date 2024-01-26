#MaintenanceUI

  - Prometheus is an open-source systems monitoring and alerting toolkit. Prometheus collects and stores its metrics as time series data, i.e. metrics information is stored with the timestamp at which it was recorded, alongside optional key-value pairs called labels.
      1. Install prometheus node exporter:
          - sudo apt-get install -y prometheus-node-exporter
          - sudo systemctl enable prometheus-node-exporter.service 
      2. install prometheus:
         - sudo apt-get install -y prometheus
      3. install
         - wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
         - echo "deb https://packages.grafana.com/oss/deb stable main" > grafana.list
         - sudo mv grafana.list /etc/apt/sources.list.d/grafana.list
         - sudo apt-get update && sudo apt-get install -y grafana
      4. enable services
         - Enable services so they start automatically:
         - sudo systemctl enable grafana-server.service
         - sudo systemctl enable prometheus.service
         - sudo systemctl enable prometheus-node-exporter.service
      5. change the yml configuration files as needed. see prometheus.yml in this branch
      6. restart services:
          - sudo systemctl restart grafana-server.service
          - sudo systemctl restart prometheus.service
          - sudo systemctl restart prometheus-node-exporter.service       
      8. verify the service is running:
        - sudo systemctl status grafana-server.service prometheus.service prometheus-node-exporter.service
      9. setting up grafana on http://localhost:3000
      10. 
