# Rationally

## Supported Use Case

### Sliding window log - X quantity over Y time period

| One can purchase 5 boxes of mask over the last 1 week

Sliding window log is the default configuration of the API endpoint. With this algorithm it allows one to collect/purchase X units of the goods over Y period.

### Static quota

| One can purchase up to 3 boxes of mask

one week later, we can update X to a different number to reflect the policy:

| One can purchase up to 5 boxes of mask (since the start of the ration)

Using the same algorithm, we can change the sliding window log to support a static quota (which can be updated). By changing Y to a sufficiently large period, we exercise a fixed quota to everyone up to X.

## Upgrades

Below are some of the possible upgrades to Rationally:

### Variable endpoints to allow any org to use the app for their rationing effort

This upgrade will allow Rationally to be used for any kind of rationing activities around the world. Independent organisations/cities/states/nations will be able to deploy their own backend where Rationally will connect to.

To do this, Rationally will have to get the host address from the authentication QR code at the login screen.

An example of such QR code will be:

```json
{
  "key": "3306a3d5-498f-42c5-a0a0-3a22af3f1121",
  "host:": "hosted-api.com"
}
```

### Sliding window log token bucket

This upgrade allows for Rationally to cumulate unused quota from previous periods. An example use case will be:

> One can purchase 1 box of mask each week, but they may carry forward the balance up to a maximum of 5

To do this, we will redefine X and Y and introduce new variables Z & t<sub>0</sub>.

- X - quota per period
- Y - period
- Z - maximum quota
- t<sub>0</sub> - starting time period

To calculate one's quota:

> floor((current_time - max(t<sub>0</sub>, Z*Y/X))/Y) * X

To calculate one's available balance:

> above_result - sum(total quantity purchase from current_time - Z\*Y/X to current_time)

To simplify the above calculation, we can force X = 1 and adjust Y so that one's quota updates at a shorter interval.

In terms of use case it will look like:

> One can purchase 1 box of mask every 2 weeks, but they may carry forward the balance up to a maximum of 6

instead of:

> One can purchase 2 box of mask every month, but they may carry forward the balance up to a maximum of 6

#### References

- https://hechao.li/2018/06/25/Rate-Limiter-Part1/
- https://konghq.com/blog/how-to-design-a-scalable-rate-limiting-algorithm/
