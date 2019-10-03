# Airflow PEX

This repo is highly inspired by another similar work done [here](https://github.com/traviscrawford/airflow-pex-example). 
The only reason I re-attempted it, so that I can get the first hand experience and also resolve some difficulties I 
faced while using the above solution. 

Build an Airflow pex by running:

```$xslt
./pants binary src/python/ariflow:airflow
``` 

This produces `airflow.pex`, a single file that is analogous to a statically-lined binary. It's a self-contained, 
runnable Airflow you can `scp` to another machine and run. However, ideally you would zip this whole folder and `scp` 
to remote machine. 

You can then run Airflow commands, using `airflow_cli` wrapper, which internally calls the `airflow.pex` file. You can 
also use this wrapper file to modify the Airflow config variables. 

```$xslt
./airflow_cli version
[2019-09-16 22:52:23,399] {__init__.py:51} INFO - Using executor SequentialExecutor
  ____________       _____________
 ____    |__( )_________  __/__  /________      __
____  /| |_  /__  ___/_  /_ __  /_  __ \_ | /| / /
___  ___ |  / _  /   _  __/ _  / / /_/ /_ |/ |/ /
 _/_/  |_/_/  /_/    /_/    /_/  \____/____/|__/  v1.10.5
```

To start the webserver
```$xslt
./airflow_cli webserver
```

To start the Scheduler
```$xslt
./airflow_cli scheduler
```

## Working Environment

If you've noticed the dags and plugins folder are part of `airflow_home` folder, but ideally they should be part of 
the `airflow.pex` itself. We can easily bundle dags and plugins as well in the `airflow.pex` like we've bundled `libs` 
folder, but unfortunately Airflow can't read them from `airflow.pex/dags` or `airflow.pex/plugins` directly, so  you can 
unzip the final PEX at the server and move them inside `airflow_home` folder. 
