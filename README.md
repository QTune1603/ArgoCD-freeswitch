# ArgoCD-freeswitch
ArgoCD-freeswitch/
├── k8s/
│   ├── freeswitch/
│   │   ├── configmap.yaml    # Cấu hình event_socket & acl
│   │   ├── deployment.yaml   # Chạy FreeSWITCH Container
│   │   └── service.yaml      # Expose port ESL 8021 & SIP 5060
│   └── exporter/
│       ├── deployment.yaml   # Chạy FreeSWITCH Exporter kết nối vào port 8021
│       └── service.yaml      # Expose port metrics 9282 cho Prometheus
└── argocd/
    └── application.yaml      # File ứng dụng cho ArgoCD Sync
