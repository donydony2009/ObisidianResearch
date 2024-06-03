- Experience with implementing resiliency patterns like Circuit Breaker, Retry, Fallback, Bulkhead Isolation, Throttling, Stale Cache and so on.
#### Circuit breaker
It's a design pattern used to detect failures and encapsulates logic of preventing a failure from constantly recurring.
For example if you see a 400 Bad Request there is probably no point in retrying since it's gonna fail anyways
It's essentially detecting failures that will not recover and putting a halt to operations
#### Retry + Fallback
Retry is the mechanism of retrying requests that are likely to succeed if retried. Usually it's good to implement some exponential backoff so if it keeps failing to retry less and less. Or just a fixed number of retries.
Fallback would be a separate endpoint that could be the same thing through a different network path, or even a more limited version of the same api
#### Bulkhead isolation
Refers to partitioning resources based on workload such that if something fails not everything fails
For example if you had a singular connection pool for all your connections, one workload could overload the connection pool and then this would affe