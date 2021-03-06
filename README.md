lzpush - Litzscore Push Client
======

Litzscore Push Client lets you get live cricket score notification from Litzscore server. It uses Litzscore API v2 to authenticate and receive notification. Make sure you have rights for push notification, check https://www.cricketapi.com/docs/

Before you begin make sure you have registered your app in Litzscore Developers site https://www.cricketapi.com/get_started/.


Get started
=======


Step 1. Register call back functions

```
def on_match_update(card):
  print "Got match update for", card['key']

def on_past_ball_update(ball):
  print "Got a ball update", ball

def on_event(name, *args):
  print "Raised event %s with params %s" % (name, args)
```

Step 2. Initialise handler

```
from lzpush import LZPushHandler

lzhandler = LZPushHandler(
  access_key = 'YOUR_ACCESS_KEY',
  secret_key = 'YOUR_SECRET_KEY',
  app_id = 'YOUR_APP_ID',
  on_update = on_match_update,
  on_past_ball_update = on_past_ball_update,
  on_event = on_event
)
```

Step 3. Listen matches

```
lzhandler.listen_match('dev_season_2014_t20_02')
lzhandler.listen_match('dev_season_2014_test_01')
```

Step 4. Connect Litzscore push server

```
lzhandler.connect()
```


If you need, Change loggers level

```
logger = logging.getLogger('lzpush')
logger.setLevel(logging.INFO)

socket_logger = logging.getLogger('socketIO_client')
socket_logger.setLevel(logging.INFO)
```

Events
======

`on_update` - Raised whenever a match is saved


`on_past_ball_update` - Raised whenever a ball is saved, sometimes we may save the ball even if there was no change in public data. This will not be raised if the last ball is changed. But whenever last ball is changed, system will raise `on_update` event. 


Support
=====
If you any question, please contact litzscore support support@cricketapi.com