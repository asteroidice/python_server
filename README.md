[![Build Status](https://travis-ci.org/prestoncarman/python_server.svg?branch=develop)](https://travis-ci.org/prestoncarman/python_server)
[![Maintainability](https://api.codeclimate.com/v1/badges/836030dc57f2e2a4bd9b/maintainability)](https://codeclimate.com/github/prestoncarman/python_server/maintainability)
[![Test Coverage](https://api.codeclimate.com/v1/badges/836030dc57f2e2a4bd9b/test_coverage)](https://codeclimate.com/github/prestoncarman/python_server/test_coverage)
[![codebeat badge](https://codebeat.co/badges/dd21c596-ed9f-42b1-8101-edc120b333ec)](https://codebeat.co/projects/github-com-prestoncarman-python_server-develop)
[![Coverage Status](https://coveralls.io/repos/github/prestoncarman/python_server/badge.svg?branch=develop)](https://coveralls.io/github/prestoncarman/python_server?branch=develop)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/b01a02d4eb0c40e6974db21676ee1604)](https://www.codacy.com/app/prestonc/python_server?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=prestoncarman/python_server&amp;utm_campaign=Badge_Grade)

# REST API for ASWWU
This is a python based REST api that ASWWU web uses for EVERYTHING.

## Installation

**Note:** This uses python 2 so if you don't have that installed, install it [here](https://www.python.org/downloads/).

The following python packages
(pattern, requests, SQLAlchemy, tornado, bleach, etc.) need to be
installed and they can be installed with the following command.

Linux:
```
pip install -r requirements.txt
```
Mac:
```
sudo -H pip install -r requirements.txt --ignore-installed six
```
You should be ready to run the server now.
```
python server.py
```

## Check Installation
You can test the connection by opening [`http://localhost:8888/search/all`](http://localhost:8888/search/all).

If you see a json array of profiles you're all set. Congrats! You now have a clone of the ASWWU backend server running locally!

## Further usage
If you want get a list of other endpoints(urls) that you can query on the server checkout the `server.py` file in the root of this project.

```python
handlers = [
    (r"/login", base.BaseLoginHandler),
    (r"/profile/(.*)/(.*)", mask.ProfileHandler),
    (r"/profile_photo/(.*)/(.*)", mask.ProfilePhotoHandler),
    (r"/search/all", mask.SearchAllHandler),
    ...
    ]
```
From this array you can see that the function that handles the `/search/all` url is part of the mask module. In `./src/aswwu/route_handlers/mask.py` you can see the function that handles this.
```python
# get all of the profiles in our database
class SearchAllHandler(BaseHandler):
    def get(self):
        profiles = alchemy.query_all(mask_model.Profile)
        self.write({'results': [p.base_info() for p in profiles]})
```

## Testing
We have continuous integration working on this project however it doesn't actually use any of the actual python server code. :( You can run a dummy test by running the following command.
```
pytest
```


## Miscellaneous

If you need it the live server is available at [`https://aswwu.com/server/`](https://aswwu.com/server/).

**Note:** If you having trouble with this process please email [ryan.rabello@wallawalla.edu](mailto:ryan.rabello@wallawalla.edu).
