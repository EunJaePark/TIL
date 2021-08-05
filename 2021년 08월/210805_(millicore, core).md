1000m = 1core

https://discuss.kubernetes.io/t/metric-server-cpu-and-memory-units/7497/2

kubernetes의 `podSpec.resource.requests.cpu`, `podSpec.resource.limits.cpu`의 최소단위는 `millicore(m)`이다.
