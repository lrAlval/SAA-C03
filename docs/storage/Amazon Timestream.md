# Timestream
- time series database
- fully managed
- scalable
- store and analyze **trillions** of events per day
- full SQL compatibility.
- Recent and historical data different storage tiers
- support encrypt in transit and at rest

![[Pasted image 20230605204644.png]]

## Use cases 
- IoT
- **operational** apps
- real time analytics.

## Architecture
### Sources
- Lambda.
- AWS IoT.
- Kinesis data analytics for Apache Flink.
- **Prometheus** (3rd party) (monitoring metrics).
- **telegraph** (3rd party) (metrics).

### Targets
- quick sight.
- sage maker.
- Grafana (Monitoring Dashboard).
- any JDBC connection.