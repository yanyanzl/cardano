#MaintenanceUI

  - Prometheus is an open-source systems monitoring and alerting toolkit. Prometheus collects and stores its metrics as time series data, i.e. metrics information is stored with the timestamp at which it was recorded, alongside optional key-value pairs called labels.
      1. Install prometheus node exporter:
          - sudo apt-get install -y prometheus-node-exporter
          - sudo systemctl enable prometheus-node-exporter.service 
      2. install prometheus:
         - sudo apt-get install -y prometheus
      3. install grafana
         - wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
         - echo "deb https://packages.grafana.com/oss/deb stable main" > grafana.list
         - sudo mv grafana.list /etc/apt/sources.list.d/grafana.list
         - sudo apt-get update && sudo apt-get install -y grafana
      4. enable services
         - Enable services so they start automatically:
         - sudo systemctl enable grafana-server.service
         - sudo systemctl enable prometheus.service
         - sudo systemctl enable prometheus-node-exporter.service
      5. change the yml configuration files as needed. located in /etc/prometheus/prometheus.yml see prometheus.yml in this branch
      6. restart services:
          - sudo systemctl restart grafana-server.service
          - sudo systemctl restart prometheus.service
          - sudo systemctl restart prometheus-node-exporter.service       
      8. verify the service is running:
        - sudo systemctl status grafana-server.service prometheus.service prometheus-node-exporter.service
      9. setting up grafana on http://localhost:3000
      10. in Grafana, Click Create + icon (in left Menu) > Import Add dashboard by Upload JSON file Click the Import button.
            - https://github.com/sanskys/SNSKY/blob/main/SNSKY_Dashboard_v2.json
  
  - Add Data from Cexplorer to the Dashboard
      cd /$NODE_HOME
      
      mkdir -p poolStat
      
      cd poolStat
      
      echo "curl https://js.cexplorer.io/api-static/pool/3fa5bb77e911054c37eeaecc22acb3387f83065e667ddf57767d39b6.json 2>/dev/null \\
      | jq '.data' | jq 'del(.stats, .url , .img, .updated, .handles, .pool_id, .name, .pool_id_hash)' \\
      | tr -d \\\"{},: \\
      | awk NF \\
      | sed -e 's/^[ \t]*/cexplorer_/' > poolStat.prom" > getstats.sh
      
      chmod +x getstats.sh
      
      ./getstats.sh

  - on producing node:
      sudo ufw allow proto tcp from 192.168.1.53 to any port 9100
      sudo ufw allow proto tcp from <Monitoring Node IP address> to any port 12798
      sudo ufw reload 
