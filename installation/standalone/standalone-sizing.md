# Standalone Sizing

## Small Tier - 16 Core, 128G RAM (r5.4xlarge / E16s v3) <a href="small-tier-16-core-128g-ram-r5.4xlarge-e16s-v3" id="small-tier-16-core-128g-ram-r5.4xlarge-e16s-v3"></a>

| Component | RAM  | Cores |
| --------- | ---- | ----- |
| Web       | 2g   | 2     |
| Postgres  | 2g   | 2     |
| Spark     | 100g | 10    |
| Overhead  | 10g  | 2     |

## Medium Tier - 32 Core, 256G RAM (r5.8xlarge / E32s v3) <a href="medium-tier-32-core-256g-ram-r5.8xlarge-e32s-v3" id="medium-tier-32-core-256g-ram-r5.8xlarge-e32s-v3"></a>

| Component | RAM  | Cores |
| --------- | ---- | ----- |
| Web       | 2g   | 2     |
| Postgres  | 2g   | 2     |
| Spark     | 250g | 26    |
| Overhead  | 10g  | 2     |

## Large Tier - 64 Core, 512G RAM (r5.16xlarge / E64s v3) <a href="large-tier-64-core-512g-ram-r5.16xlarge-e64s-v3" id="large-tier-64-core-512g-ram-r5.16xlarge-e64s-v3"></a>

| Component | RAM  | Cores |
| --------- | ---- | ----- |
| Web       | 4g   | 3     |
| Postgres  | 4g   | 3     |
| Spark     | 486g | 54    |
| Overhead  | 18g  | 4     |

## Cluster <a href="cluster" id="cluster"></a>

If your program requires more horsepower or (spark) workers than the example tiers above which is fairly common in Fortune 500 companies than you should consider the horizontal and ephemeral scale of a cluster. Common examples are Amazon EMR, Cloudera CDP etc... OwlDQ is built to scale up horizontally and can scale to hundreds of nodes.
