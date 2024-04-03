# Challenge Overview

We are greeted with a page that tells us that similar code is used but that the session IDs are no longer sequential. We are then called to log in with admin credentials again. If there's anything expected from the previous challenge, it's that the log in boxes are once again useless.

## Challenge Approach

I tried logging in with random credentials and observed (via Firefox) that the PHP cookies seemed to be hexadecimal values. I deleted a few cookies (not before saving their values first) in order to get a few values to understand their patterning. This is what they looked like:

```
126-a
338-a
260-a
```

At this point, I realized that burpsuite wasn't going to hold its own because I needed something that would quickly convert values to hex. It was time to take out Python! Now,
