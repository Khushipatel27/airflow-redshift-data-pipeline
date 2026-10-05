# Setting up Airflow Connections

The DAG uses two Airflow connections. Create them in the Airflow UI under **Admin → Connections → Create**.

## 1. `aws_credentials` (used by the S3 → Redshift COPY)

| Field     | Value                                   |
|-----------|-----------------------------------------|
| Conn Id   | `aws_credentials`                       |
| Conn Type | `Amazon Web Services`                   |
| Login     | your IAM user's **Access key ID**       |
| Password  | your IAM user's **Secret access key**  |

The IAM user needs `AmazonS3ReadOnlyAccess` (or read access to your bucket).

## 2. `redshift` (used by every operator that runs SQL)

| Field     | Value                                                                         |
|-----------|-------------------------------------------------------------------------------|
| Conn Id   | `redshift`                                                                    |
| Conn Type | `Postgres`                                                                    |
| Host      | Redshift endpoint **without** port/db, e.g. `default-workgroup.123456789012.us-west-2.redshift-serverless.amazonaws.com` |
| Schema    | `dev`                                                                         |
| Login     | Redshift admin username                                                       |
| Password  | Redshift admin password                                                       |
| Port      | `5439`                                                                        |

> Never commit these values. They live only in Airflow's metadata DB.
