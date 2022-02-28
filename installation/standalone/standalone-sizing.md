# Standalone Sizing

## Small Tier - 16 Core, 128G RAM (r5.4xlarge / E16s v3) <a href="#small-tier-16-core-128g-ram-r5.4xlarge-e16s-v3" id="small-tier-16-core-128g-ram-r5.4xlarge-e16s-v3"></a>

| Component | RAM  | Cores |
| --------- | ---- | ----- |
| Web       | 2g   | 2     |
| Postgres  | 2g   | 2     |
| Spark     | 100g | 10    |
| Overhead  | 10g  | 2     |

## Medium Tier - 32 Core, 256G RAM (r5.8xlarge / E32s v3) <a href="#medium-tier-32-core-256g-ram-r5.8xlarge-e32s-v3" id="medium-tier-32-core-256g-ram-r5.8xlarge-e32s-v3"></a>

| Component | RAM  | Cores |
| --------- | ---- | ----- |
| Web       | 2g   | 2     |
| Postgres  | 2g   | 2     |
| Spark     | 250g | 26    |
| Overhead  | 10g  | 2     |

## Large Tier - 64 Core, 512G RAM (r5.16xlarge / E64s v3) <a href="#large-tier-64-core-512g-ram-r5.16xlarge-e64s-v3" id="large-tier-64-core-512g-ram-r5.16xlarge-e64s-v3"></a>

| Component | RAM  | Cores |
| --------- | ---- | ----- |
| Web       | 4g   | 3     |
| Postgres  | 4g   | 3     |
| Spark     | 486g | 54    |
| Overhead  | 18g  | 4     |

## Estimates

Sizing should allow headroom and based on peak concurrency and peak volume requirements.  If concurrency is not a requirement, you just need to size for peak volume (largest tables). Best practice to efficiently scan is to scope the job by selecting critical columns. See [performance tuning](../../benchmarks/performance-tuning/) for more information.

| Bytes per Cell | Rows             | Columns | Gigabytes | Gigabytes for Spark (3x) |
| -------------- | ---------------- | ------- | --------- | ------------------------ |
| 16             | 1,000,000.00     | 25      | 0.4       | 1.2                      |
| 16             | 10,000,000.00    | 25      | 4         | 12                       |
| 16             | 100,000,000.00   | 25      | 40        | 120                      |
| 16             | 1,000,000.00     | 50      | 0.8       | 2.4                      |
| 16             | 10,000,000.00    | 50      | 8         | 24                       |
| 16             | 100,000,000.00   | 50      | 80        | 240                      |
| 16             | 1,000,000.00     | 100     | 1.6       | 4.8                      |
| 16             | 10,000,000.00    | 100     | 16        | 48                       |
| 16             | 1,000,000,000.00 | 100     | 1600      | 4800                     |
| 16             | 100,000,000.00   | 100     | 160       | 480                      |
| 16             | 1,000,000.00     | 200     | 3.2       | 9.6                      |
| 16             | 10,000,000.00    | 200     | 32        | 96                       |
| 16             | 100,000,000.00   | 200     | 320       | 960                      |
| 16             | 1,000,000,000.00 | 200     | 3200      | 9600                     |

## Cluster <a href="#cluster" id="cluster"></a>

If your program requires more horsepower or (spark) workers than the example tiers above which is fairly common in Fortune 500 companies than you should consider the horizontal and ephemeral scale of a cluster. Common examples are Amazon EMR, Cloudera CDP etc... OwlDQ is built to scale up horizontally and can scale to hundreds of nodes.
