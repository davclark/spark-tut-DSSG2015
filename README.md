Spark Tutorial for DSSG 2015
============================

You definitely want to refer to [the official docs from Apache
Spark](https://spark.apache.org/docs/latest/).

Installation
------------

### Anaconda is *le shiz*

    conda install -c blaze spark

This is apparently not public, but Matt Rocklin (former U Chicago alum) and the
Blaze team are very interested in supporting spark.

### On Linux

CDH 5 is probably the best way to go for Linux, it includes Spark 1.3.0 (which
includes Spark SQL), and also Hadoop, etc. Strangely, it doesn't appear to
support postgres 9.4, and Spark SQL is "unsupported" (but it's installed). I
don't know if this is just a judgement call, or if there are CDH-specific
problems with Spark SQL. Cloudera develops Impala, a "competitor" to Spark.

### On OS X

Spark 1.3 still targets Scala 2.10. This is non-standard at this point on
homebrew, so I did:

    brew install scala210
    brew link --force scala210

Homebrew complains, but I won't be installing scala 2.11 anytime soon.

### Virtual Machines

HortonWorks and Cloudera both provide VMs. For now, it looks like Cloudera is
more up-to-date (HortonWorks does Spark 1.2). Cloudera also supports more Linux
flavors (provides debs and rpms).

### Setting up IPython

At a minimum, You'll need something like this in your `~/.bash_profile`:

    # Setup for Spark / PySpark (sadly, that IPYTHON variable is a bit generally named...)
    export IPYTHON=1
    export SPARK_HOME=/opt/anaconda/share/spark
    # Or wherever you put the local spark install
    # export SPARK_HOME=~/Code/spark-1.3.1-bin-hadoop2.6
    # export PATH=$SPARK_HOME/bin:$PATH
    export PYSPARK_SUBMIT_ARGS='--master local[*] --executor-memory 12g'

This is from a [Cloudera Blog
Post](http://blog.cloudera.com/blog/2014/08/how-to-use-ipython-notebook-with-apache-spark/).
It includes setting things up for remote, secure execution. I won't worry about
that today, so here's the essentials:

    ipython profile create pyspark

Copy the `00-pyspark-setup.py` file to your new profile directory, which will
be something like `~/.ipython/profile_pyspark/startup`.

You'll need to modify the paths to reflect your installation root (under
share/spark in the anaconda root, or wherever you unzipped the tarball).
