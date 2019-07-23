# faasflow-redis-statestore
A **[faas-flow](https://github.com/s8sg/faas-flow)** statestore implementation that uses redis to store state

## Getting Stated

### Deploy redis

#### Deploy in Swarm

TODO:

#### Deploy in k8s

```bash
kubectl apply -f resource/redis-k8s-standalone.yml
```

or you can install redis service by your self



### Use redis StateStore in `faasflow`
* Set the `stack.yml` with the necessary environments
```yaml
    redis_url: "redis.default.svc.cluster.local:6379"
```
* Use the `RedisStateStore` as a DataStore on `handler.go`
```go
redisStateStore "github.com/chennqqi/faas-flow-redis-statestore"

func DefineStateStore() (faasflow.StateStore, error) {
        ss, err := redisStateStore.GetConsulStateStore(os.Getenv("redis_url"), os.Getenv("redis_master"))
        if err != nil {
                return nil, err
        }
        return ss, nil
}
```
