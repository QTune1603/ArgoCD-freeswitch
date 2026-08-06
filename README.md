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

FreeSWITCH + ArgoCD + Prometheus & Grafana Monitoring

Triển khai FreeSWITCH và FreeSWITCH Exporter lên Kubernetes Cluster.
Thiết lập GitOps với ArgoCD: Quản lý K8s Manifests / ConfigMap trên Git để ArgoCD tự động Sync.
Thiết lập Monitoring với Prometheus & Grafana: Thu thập metrics real-time từ FreeSWITCH (active calls, channels, CPS, CPU/RAM) và vẽ Dashboard trên Grafana.


Phase 1: Chuẩn bị môi trường Kubernetes local

Phase 2: Soạn thảo Kubernetes Manifests cho FreeSWITCH & Exporter
Tạo cấu trúc thư mục Kubernetes manifests trong dự án 

Phase 3: Triển khai qua ArgoCD (GitOps Workflow)
Đẩy các file K8s Manifests lên Git Repository.
Tạo file argocd/application.yaml định nghĩa ArgoCD Application.
Apply application.yaml để ArgoCD tự động kéo manifests và deploy FreeSWITCH + Exporter lên K8s.

Phase 4: Cấu hình Prometheus & Dựng Grafana Dashboard
Cấu hình Prometheus Scrape Config / ServiceMonitor tới freeswitch-exporter:9282.
Import hoặc tạo Grafana Dashboard gồm các panel:
Active Calls & Channels Count (Số cuộc gọi đang diễn ra).
Calls Per Second (CPS) (Số cuộc gọi khởi tạo mỗi giây).
FreeSWITCH Uptime & System Metrics (CPU, RAM).
SIP Registration Count (Số thiết bị SIP đã đăng ký).

Phase 5: Test & Kiểm chứng (Simulate Calls)
Dùng công cụ test cuộc gọi (như sipp hoặc softphone) tạo cuộc gọi thử nghiệm tới FreeSWITCH.

