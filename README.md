# EyeCademy-Git-Files
This repository contains the VSQL required to ingest data from a Linux
machine to a  Vertica DB.

The use case of this example is to conceptualise the power of in database
machine learning and data processing possible using VSQL and Vertica.
This Problem Statement of this project is the following. We have previous
data points in which IOT Data is missing due to internet faults.
In an effort to produce the most accurate C02 Reporting required by the
national government, they have supplied a data consultant to create
an automated pipeline to resolve any missing IOT data concerns.
The data used within this project is C02 Emissions readers from Denmark which
can be found at the following link:
  http://iot.ee.surrey.ac.uk:8080/datasets.html#pollution

The following code located in this repository extracts current data extracted
to create a model that can effectively fill in any missing values as they are
streamed into the database. Alleviating the poor quality data problem.

In reality this methodology could be used to accurately numeric prediction
(regression).
A more tangible example would be how much energy was not produced via a
wind turbine during maintenance or unexpected outages.
This model and pipeline would be able to impute values into the dataset to
enable improved CBA analysis or Discounted Cash Flow investment analysis.

The SQL Code within this repository aimed to be flexible to allow for
unexpected data inputs without failing. Continuous table drops and creations
allow the pipeline to run over and over again with little required changes.



The Modules follow a linear path to enable an end to end project.
The Main Document located in the repository are the following:
1: Data Ingestion
2: Vertical Data Pre-processing
3:Machine learning sampling
4:predictive analytics
5:Final SQL Tables

1: Data Ingestion
Initially data is downloaded via web, and copied into the database using the
command line.

2: Vertical Data Pre-processing
Sensor_id are created based on unique longitude and latitude's.
Duplicate Observations are removed from the tables.
Features are created from the data to assist with later predictive analytics
and unnecessary columns are dropped from the table.
columns containing zero's (early in the data capture process) are removed as
they will skew any statistical model
Numerical Observations are normalised to assist with predictive analytics.

Data is then loaded unsegmented to allow for data table minor alterations.

3: Machine Learning sampling
A sample of the pre-processed data is taken and balanced to avoid sensor_id
biases.
A Random Forest model is trained and a model summary is produced.

4:A Pretend IOT Failure is simulated. Damaged data observations
are then predicted using the trained model.

5: Predicted Data points are joined and manipulated back into the dataset.
These Value would be to be exported for as normal data analytics or regulatory
reporting.

6:Tables Reset:
A list of drop tables to reset the database to end of stage 1.
