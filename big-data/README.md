# Big Data workshop tech requirements
It is worth prefacing the below list with the caveat: Spark is a non-trivial installation -- i.e. it's a not a simple 'pip install' unfortunately.

Also, as mentioned in the workshop, you are not required to know any Spark, let alone implement it in code, for any part of the end-point assessment. *This section is above and beyond the Apprenticeship requirements*.

If however, you still want to install and experiment with Spark, then here are a list of packages and software you will need:

* Java 8.
  - Note, this isn't the latest version of Java. This means you will have to sign up for an Oracle account and agree to Terms & Conditions.
  - You can use [this link](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) and choose the appropriate development kit at the bottom of the page.

* Spark.
  - You can install this package directly from the [Apache website](http://spark.apache.org/downloads.html).
  - Note: as of December 2019, there's been an update to the package and Spark 3.0.0 has been released. The workshop content however has *only* been tested on the stable 2.4.4 release. Feel free to test out either version!
  -  The file you download should look something like: `spark-3.0.0-preview2-bin-hadoop2.7.tgz` or `spark-2.4.4-preview2-bin-hadoop2.7.tgz`.
  - Save this file in your home directory.

### Spark API/Library in Python
* PySpark
  - This is the Python package that allows you to use Spark functionality in Python.
  - Simply run `pip install pyspark` to install PySpark.
  - For more information, the [PyPi documentation](https://pypi.org/project/pyspark/) may prove useful.

### Spark API/Library in R
  * SparklyR
    - This is a user-friendly package that allows you to use Spark functionality in R. Note that there are others, but this is the one we've used in the workshop.
    - To start off simply run `install.packages('sparklyr')`.
    - There are a few more minor steps you can follow directly from the package's [excellent documentation website](https://spark.rstudio.com/).
