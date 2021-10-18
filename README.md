
# To reproduce bug, two solutions

## with pyenv

```
$ pyenv install 3.10.0
$ pyenv shell 3.10.0

$ python3.10 -m venv venv
$ source venv/bin/activate

# Install same version as current heroku buildpack
$ pip install -U pip==20.2.4 setuptools==47.1.1 wheel==0.36.2 

$ pip install -r requirements.txt

$ # It failed:
$ import-check
Traceback (most recent call last):
  File "/home/sileht/workspace/mergify/py10-bug/venv/bin/import-check", line 6, in <module>
    from pkg_resources import load_entry_point
  File "/home/sileht/workspace/mergify/py10-bug/venv/lib/python3.10/site-packages/pkg_resources/__init__.py", line 3262, in <module>
    def _initialize_master_working_set():
  File "/home/sileht/workspace/mergify/py10-bug/venv/lib/python3.10/site-packages/pkg_resources/__init__.py", line 3245, in _call_aside
    f(*args, **kwargs)
  File "/home/sileht/workspace/mergify/py10-bug/venv/lib/python3.10/site-packages/pkg_resources/__init__.py", line 3274, in _initialize_master_working_set
    working_set = WorkingSet._build_master()
  File "/home/sileht/workspace/mergify/py10-bug/venv/lib/python3.10/site-packages/pkg_resources/__init__.py", line 584, in _build_master
    ws.require(__requires__)
  File "/home/sileht/workspace/mergify/py10-bug/venv/lib/python3.10/site-packages/pkg_resources/__init__.py", line 901, in require
    needed = self.resolve(parse_requirements(requirements))
  File "/home/sileht/workspace/mergify/py10-bug/venv/lib/python3.10/site-packages/pkg_resources/__init__.py", line 787, in resolve
    raise DistributionNotFound(req, requirers)
pkg_resources.DistributionNotFound: The 'enum34; python_version < "3.4"' distribution was not found and is required by ddtrace

$ # upgrade setuptools
$ pip install -U setuptools
$  import-check
it works
```

## with heroku

Just use this repo as-is in heroku
