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
For example if you had a singular connection pool for all your connections, one workload could overload the connection pool and then this would affect other workload
The solution would be to partition your connection pools based on either bussiness logic.
Bulkhead comes from a concept in the ships where the ship is partitioned such that if there is a hole in the ship hull the ship doesn't sink as there are many partitions so only one partition would be filled with water.

So partition your resources such that in case of a local failure it doesn't turn into a catastrophic failure

This can be for example at the level of a thread pool where you separate the user facing tasks from the background tasks
At a service level where you put your services into microservices where is service operates independently
It could be at a database level it could involve partitioning your database and connections to isolate different types of data and workload
At the network level it could involve separating network traffic based on the data of the services or some other business logic
And yea there are many other examples

#### Throttling
Throttling involves setting limits to how much an api can be used over a unit of time. This is usually to prevent impact performance impact over your api and it also serves as a safe guard against bugs that just call your api in a loop.
Ways to implement it could be a simple fixed size queue
A sliding window of max calls