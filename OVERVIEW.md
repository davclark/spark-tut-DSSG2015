So, you have "big" data?
========================

Really?
-------

[Where I'm from](http://dlab.berkeley.edu), when I say "data-intensive social science"
I mean:

 - You have some conventional approach, and
 - You have more data than works nicely with that approach. e.g.,
    - It takes so long that you:
       - start making scientific decisions based on computational concerns, or
       - forget what you were doing / start making mistakes (hopefully you
         notice).
    - Others will have trouble reproducing your workflow;
    - Others will have trouble *understanding* what you did at all.

When I say "big data," I am quite literal... I generally mean "it won't fit on
a thumb-drive." Probably you don't want to just keep it all on your tiny SSD.


Data Management
---------------

 - This is really important.
 - Make a plan, and make it clear to your team-mates.
 - Take the time to transform your raw data into a format that works nicely:
    - Databases (SQL, NoSQL) - [a nice
      comparison](http://matthewrocklin.com/blog/work/2014/09/01/Blaze-HMDA/)
      by Matt Rocklin
    - Binary formats like HDF5, Avro, Parquet, BCOLZ, NetCDF4
    - Or invent your own!
 - I use git annex, it's awesome.

Sadly, I don't know of well-structured resources for scientists on data
management. ICPSR maintains [some
resources](https://www.icpsr.umich.edu/icpsrweb/content/datamanagement/index.html),
but they won't provide answers - they just provide you with the tools to think
about your particular issue.


The focus for today
-------------------

What do you do when your data won't fit in memory? In approximate order of
easiness:

 - Get a bigger (shared memory) machine
    - For efficiency, you probably want to explore parallelization
 - Out-of-core or streaming approaches
    - We'll see an example with pandas
    - Databases provide another way to do this
    - UChicago's Matt Rocklin is [pushing the limits of this
      approach](http://matthewrocklin.com/blog/work/2015/02/17/Towards-OOC-Bag/)
 - Clusters / HPC
    - You can probably get free access to HPC (Argonne, OpenScienceGrid), and
    - you can sort-of pretend that HPC is a cluster (Though HPC often has some
      rough spots, Spark support is currently reasonable and being actively improved)


What if my analyses take forever?
---------------------------------

 - Use parallelization - you probably have hella cores in your machine.
    - Threads are problematic in Python, so use multiprocessing
    - Or, just run multiple programs at the same time.
    - Once again, Matt Rocklin is pushing the limits on this (with [the same
      tech as
      above](http://matthewrocklin.com/blog/work/2015/02/17/Towards-OOC-Bag/)).
    - Spark does this for you, even if you're on a single multi-core machine.
 - Use GPUs - you can get [~6 single-precision TFLOPS (YMMV) for
   ~$1k](https://developer.nvidia.com/devbox), and this is an active area in
   machine learning:
    - Caffe
    - BIDMach
    - Theano / PyLearn2
    - Torch
    - etc.
 - Also use clusters / HPC


Keeping it real
---------------

No one is going to have a complete, current list of appropriate methods for
your data challenges. Forks are encouraged! Send me pull requests!
