# System Architecture

## Data Flow

1. **B1 (Edge)** captures video from cameras, runs YOLO detection, extracts vehicle metadata
2. **B1** publishes detection events to Kafka topic `traffic.events.raw`
3. **B2 (Stream Processor)** consumes events, aggregates in 5-second windows, computes traffic metrics, classifies congestion
4. **B2** writes aggregated metrics to PostgreSQL
5. **B2 (API)** serves metrics via REST endpoints and WebSocket live updates
6. **B3 (Dashboard)** displays real-time traffic heatmaps and congestion visualizations
7. **B4 (Platform)** orchestrates all services, provides API gateway (Kong), and monitors health (Prometheus/Grafana)

## Service Map

| Service | Port | Protocol | Owner |
|---------|------|----------|-------|
| Kafka | 9092 | TCP | B4 (shared infra) |
| PostgreSQL | 5432 | TCP | B4 (shared infra) |
| b2-stream-processor | — | Internal | B2 |
| b2-api | 8000 | HTTP/WS | B2 |
| b3-dashboard | 3000 | HTTP | B3 |
| Kong API Gateway | 8080 | HTTP | B4 |
| Prometheus | 9090 | HTTP | B4 |
| Grafana | 3001 | HTTP | B4 |

## Integration Points

- **B1 → B2:** Kafka topic `traffic.events.raw` (JSON, partitioned by camera_id)
- **B2 → B3:** REST API (`/metrics/*`, `/congestion/*`) + WebSocket (`/ws/metrics`)
- **B2 → B4:** Health endpoint (`/health`) + Prometheus metrics (`/metrics`)
- **B4 → All:** Docker orchestration, Kong routing, monitoring
