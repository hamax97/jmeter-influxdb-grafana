# JMeter / InfluxDB / Grafana
Example setup for visualizing JMeter metrics in Grafana using InfluxDB as storage.

Follow the steps in each of the following sections.

# Requirements

- Install Docker and Docker Compose.
- Install JMeter.

# Deploy

Run the following command with this repository as working directory:
```bash
docker compose up -d
```

# InfluxDB

## Setup InfluxDB
Visit in your browser:

```
localhost:8086
```

Set username/password to **admin/admin123**.

Initial bucket name: **jmeter**.

Other fields can be filled with anything you want, you'll use them when setting up grafana.

## Generate Token
In the next screen go to:

1. Load Data
2. API TOKENS
3. GENERATE API TOKEN
4. Custom API Token:

   - Description: jmeterToken
   - Buckets: mark read and write in the jmeter bucket.
   - Click Generate, copy the token and store it.

# Grafana

## Setup Data Source
To login use the default usename/password: **admin/admin**.

Go to:

1. Configuration.
2. Data soruces.
3. Add data source.
4. InfluxDB:

   - Query Language: Flux.
   - URL: `http://influxdb:8086`
   - In Auth enable the checkmarck: **Basic auth**
   - User: **admin**.
   - Password: **admin123**.
   - Organization: whatever you used when setting up InfluxDB.
   - Token: copy and paste the token generated previously in InfluxDB.
   - Default Bucket: **jmeter**.

## Setup Dashborad

Download a dashboard from the community. You have to make sure it maches the InfluxDB version,
in our case 2.6.
A good option [here](https://grafana.com/grafana/dashboards/13644-jmeter-load-test-org-md-jmeter-influxdb2-visualizer-influxdb-v2-0-flux/).
Click on **Download JSON**.

Go back to Grafana UI:

1. Click on Dashboards.
2. Click on New.
3. Click on Import.
4. Click on Upload JSON file.
5. Pick the file previously downloaded.
6. Under InfluxDB2.0_Jmeter, pick InfluxDB.
7. Click Import.

# JMeter

TODO:
- Create a script recording two transactions from https://www.demoblaze.com/
- Add the backend listener as explained here: https://jmeter.apache.org/usermanual/realtime-results.html#influxdb_v2
- Run the script and check out the dashboard.
