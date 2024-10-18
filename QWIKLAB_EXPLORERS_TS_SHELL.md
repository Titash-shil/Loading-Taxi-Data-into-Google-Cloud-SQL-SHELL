# [Loading Taxi Data into Google Cloud SQL](https://www.cloudskillsboost.google/games/5521/labs/35625)

## Solution [here](https://youtu.be/it72NG_h_XY)

### Run the following Commands in CloudShell

```
export PROJECT_ID=$(gcloud info --format='value(config.project)')
export BUCKET=${PROJECT_ID}-ml

gcloud sql instances create taxi \
    --tier=db-n1-standard-1 --activation-policy=ALWAYS

sleep 15

gcloud sql users set-password root --host % --instance taxi \
 --password Passw0rd

export ADDRESS=$(wget -qO - http://ipecho.net/plain)/32

gcloud sql instances patch taxi --authorized-networks $ADDRESS

MYSQLIP=$(gcloud sql instances describe \
taxi --format="value(ipAddresses.ipAddress)")

echo $MYSQLIP

mysql --host=$MYSQLIP --user=root \
      --password --verbose
```

- type or paste the followinG password and press Enter.

```
Passw0rd
```

- Now paste the following content into the command line to create the schema for the trips table:

```
create database if not exists bts;
use bts;

drop table if exists trips;

create table trips (
  vendor_id VARCHAR(16),    
  pickup_datetime DATETIME,
  dropoff_datetime DATETIME,
  passenger_count INT,
  trip_distance FLOAT,
  rate_code VARCHAR(16),
  store_and_fwd_flag VARCHAR(16),
  payment_type VARCHAR(16),
  fare_amount FLOAT,
  extra FLOAT,
  mta_tax FLOAT,
  tip_amount FLOAT,
  tolls_amount FLOAT,
  imp_surcharge FLOAT,
  total_amount FLOAT,
  pickup_location_id VARCHAR(16),
  dropoff_location_id VARCHAR(16)
);
```

### Congratulations 🎉 for completing the Lab !

##### *You Have Successfully Demonstrated Your Skills And Determination.*

#### *Well done!*

#### Don't Forget to Join the [Telegram Channel](https://t.me/quickgcplab) & [Discussion group](https://t.me/quickgcplabchats)

# [QUICK GCP LAB](https://www.youtube.com/@quickgcplab)
