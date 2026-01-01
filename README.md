# Feature Store and Data Versioning with Delta Lake

This project demonstrates a simple feature store using Delta Lake for data versioning with PySpark.

## Requirements

- Python 3.x
- PySpark
- Delta Lake (delta-spark package)

Install dependencies:
```
pip install pyspark delta-spark
```

## Project Structure

- `data/`: Contains sample raw data CSV files.
- `notebooks/`: Jupyter notebook for the feature store implementation.
- `delta/`: Directory where Delta tables are stored.

## Running the Notebook

1. Ensure Spark and Delta are configured.
2. Open `notebooks/feature_store.ipynb` in Jupyter.
3. Run the cells in order.

The notebook performs:
- Ingests raw CSV data into a Delta table.
- Computes derived features (aggregations).
- Writes features to a versioned Delta table.
- Demonstrates time travel queries.

## Querying Different Versions

After running the notebook, you can query historical versions using:

```python
# For version 0
spark.read.format("delta").option("versionAsOf", 0).load("../delta/features").show()

# For version 1
spark.read.format("delta").option("versionAsOf", 1).load("../delta/features").show()
```

To see the history:
```python
from delta.tables import DeltaTable
delta_table = DeltaTable.forPath(spark, "../delta/features")
delta_table.history().show()
```

## Pushing to GitHub

Initialize git repository:
```
git init
git add .
git commit -m "Initial commit"
```

Create a repository on GitHub and push:
```
git remote add origin <your-repo-url>
git push -u origin main
```