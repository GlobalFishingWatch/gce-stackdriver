# gce-stackdriver
Python client for reading and writing custom metrics with google cloud monitoring (stackdriver)

# Design Concept

Provide a pip installable module that genericaly supports creating, writing and reading custom metrics in the same way that this sample code does.

https://cloud.google.com/monitoring/custom-metrics/using-custom-metrics
https://cloud.google.com/monitoring/demos/wrap_write_labeled_metric

- Accumulate metrics and write in a batch to stay within google API rate limits
- Write asynchronously so that Google API latency does not block a running task
- Provide a context manager interface 
- read custom metric definitions from a config file

## Usage Example

```python
import stackdriver

# define a metric
labels = {'color': 'descrition of the color label', 
          'size': 'description of the size label'}
          
metric = stackdriver.Metric.create(name='task_counter', labels=labels, data_type='int64', 
                            description='Count of tasks completed')


def doSomethings():
  with stackdriver.Counter('task_counter', color='red', size='large') as counter:
    # do a thing
    counter.increment()   # count one thing done
    # do 4 more things
    counter.increment(4)
```
