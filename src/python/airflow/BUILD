python_binary(
  name='airflow',
  dependencies=[
    '3rdparty/python:apache-airflow',
    '3rdparty/python:prometheus-client',
    'src/python/libs',
  ],

  # The airflow script has some logic that cannot be called as a module,
  # so we copy the script into this repo. Ideally this would be fixed upstream.
  source='airflow.py',
)
