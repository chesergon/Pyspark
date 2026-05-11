#  PySpark Basics Demo

A beginner-friendly introduction to **Apache Spark with Python (PySpark)**, covering the core building blocks of Spark — `SparkConf`, `SparkContext`, and RDDs (Resilient Distributed Datasets).

---

## 📌 Overview

This notebook walks through the foundational concepts of PySpark, demonstrating how to configure and initialize a Spark application, inspect its settings, manage logging, and perform basic distributed data operations using RDDs.

---

## 🎯 Learning Objectives

By the end of this notebook, you will be able to:

- Create and configure a `SparkConf` object
- Initialize a `SparkContext` to connect to a Spark cluster
- Inspect Spark application properties (app name, master URL, parallelism)
- Control Spark's log verbosity using `setLogLevel()`
- Create an RDD using `sc.parallelize()`
- Perform basic RDD actions such as `.sum()`
- Properly shut down a Spark session with `sc.stop()`

---

## 📓 Notebook Contents

### 1. Setup & Imports
```python
from pyspark import SparkConf, SparkContext
```
Imports the two core PySpark classes needed to start a Spark application.

---

### 2. Creating SparkConf and SparkContext
```python
conf = SparkConf().setAppName("PysparkBasicsDemo").setMaster("local[*]")
sc = SparkContext(conf=conf)
```
- **`SparkConf`** — holds configuration settings for the Spark application
- **`setAppName()`** — gives the application a human-readable name
- **`setMaster("local[*]")`** — runs Spark locally using **all available CPU cores**
- **`SparkContext`** — the entry point to any Spark functionality

---

### 3. Inspecting Spark Properties
```python
print("Application Name:", sc.appName)
print("Master URL:", sc.master)
print("SparkConf Settings:", sc.getConf().getAll())
print("Default Parallelism:", sc.defaultParallelism)
```
Useful for verifying your Spark setup and understanding how the session is configured.

| Property | Description |
|---|---|
| `sc.appName` | Name of the Spark application |
| `sc.master` | The master URL (e.g. `local[*]`) |
| `sc.getConf().getAll()` | All active Spark configuration key-value pairs |
| `sc.defaultParallelism` | Number of partitions used by default (equals number of CPU cores in local mode) |

---

### 4. Log Level Management
```python
sc.setLogLevel("WARN")
```
Reduces Spark's verbose console output to only show warnings and errors — recommended when running in notebooks to keep output clean.

| Log Level | What it shows |
|---|---|
| `ALL` | Everything |
| `INFO` | General information (default, very verbose) |
| `WARN` | Warnings and errors only ✅ recommended |
| `ERROR` | Errors only |
| `OFF` | Nothing |

---

### 5. Creating and Using an RDD
```python
rdd = sc.parallelize(range(10))
sum_result = rdd.sum()
print("Sum of RDD Elements:", sum_result)  # → 45
```
- **`sc.parallelize()`** — distributes a local Python collection across Spark partitions, creating an RDD
- **`.sum()`** — an **action** that triggers computation and returns the total

---

### 6. Stopping the SparkContext
```python
sc.stop()
```
Always stop the SparkContext when done to free up memory and system resources. Only one SparkContext can be active at a time.

---

## ⚙️ Setup & Installation

### Prerequisites
- Python 3.8+
- Java 8 or 11 (required by Spark)
- Jupyter Notebook or JupyterLab

### Install PySpark
```bash
pip install pyspark
```

### Verify Java
```bash
java -version
```

### Launch Jupyter
```bash
jupyter notebook
```

---

##  Notes

- The warnings about `numexpr` and `bottleneck` versions are from Pandas and do **not** affect PySpark functionality. You can optionally upgrade them:
```bash
pip install --upgrade numexpr bottleneck
```
- `"local[*]"` is for local development only. In a real cluster environment, the master URL would point to a Spark cluster (e.g. `spark://host:7077`)
- Always call `sc.stop()` at the end of your notebook to avoid `SparkContext already exists` errors on re-runs

---

##  Key Concepts Summary

| Concept | Description |
|---|---|
| `SparkConf` | Configuration object for the Spark application |
| `SparkContext` | Entry point to Spark — manages the connection to the cluster |
| `RDD` | Resilient Distributed Dataset — Spark's core data structure |
| `parallelize()` | Creates an RDD from a local Python collection |
| `Action` | An operation that triggers computation (e.g. `.sum()`, `.collect()`) |
| `Transformation` | A lazy operation that defines a new RDD (e.g. `.map()`, `.filter()`) |

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
