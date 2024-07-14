# Django Celery with Redis 
It is a basic example for implementing task queues with Celery & Redis 

## Virtual env setup
```bash
python3 -m venv path/to/venv
source path/to/venv/bin/activate
```

## You need to install packages in virtual environments 
```bash
pip install -r requirements.txt 
```

## Update deps 
```bash
pip freeze -r requirements.txt 
```

## Redis setup
Install Redis in your machine 
-> [Redis](https://redis.io/)
to check your redis server
```bash
redis-server
```

## Environment Variables

```
CELERY_BROKER_REDIS_URL="redis://localhost:6379"
DEBUG=True

```

## Check your broker server 


## to run your Django server
```bash
python manage.py runserver
``` 
## To run your scheduler 
```bash
celery -A project_name beat -l info

celery -A celeryapp beat -l info
```
In `celery.py` hardcoded scheduler config 👇

```python
app.conf.beat_schedule = {
    'multiply-task-crontab': {
        'task': 'multiply_two_numbers',
        'schedule': crontab(hour=7, minute=30, day_of_week=1),
        'args': (16, 16),
    },
    'multiply-every-5-seconds': {
        'task': 'multiply_two_numbers',
        'schedule': 5.0,
        'args': (16, 16)
    },
    'add-every-30-seconds': {
        'task': 'movies.tasks.add',
        'schedule': 30.0,
        'args': (16, 16)
    },
}
```
## To run your Celery worker 
```bash
celery -A project_name worker -l info

celery -A celearyapp worker -l info
```



