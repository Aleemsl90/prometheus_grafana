# Prometheus + Grafana Monitoring Stack  
Server performance monitoring with Prometheus + Grafana

A production-ready setup for monitoring infrastructure/apps with:  
- **Prometheus** (metrics collection)  
- **Grafana** (visualization + alertrules + notification) 

📂 Repository Structure
``` bash
prometheus-grafana-manual/  
├── prometheus/  
│   ├── prometheus.yml       # Main Prometheus config  
│   ├── alerts.yml           # Alert rules  
│   └── prometheus.service   # Systemd service file  
├── grafana/  
│   ├── dashboards/          # Exported JSON dashboards  
│   └── datasources.yml      # Auto-configured datasource  
└── README.md                # Documentation
```



🔧 Configuration Steps


🔔 Alerting