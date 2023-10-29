# Challenge Description

I wrote you another song. Put the flag in the picoCTF{} flag format

Notice: The Rockstar language has changed since this problem was released! Use this Wayback Machine URL to use an older version of Rockstar, [here](https://web.archive.org/web/20190522020843/https://codewithrockstar.com/online).

## Rockstar code

```
Rocknroll is right              
Silence is wrong                
A guitar is a six-string        
Tommy's been down               
Music is a billboard-burning razzmatazz!
Listen to the music             
If the music is a guitar                  
Say "Keep on rocking!"                
Listen to the rhythm
If the rhythm without Music is nothing
Tommy is rockin guitar
Shout Tommy!                    
Music is amazing sensation 
Jamming is awesome presence
Scream Music!                   
Scream Jamming!                 
Tommy is playing rock           
Scream Tommy!       
They are dazzled audiences                  
Shout it!
Rock is electric heaven                     
Scream it!
Tommy is jukebox god            
Say it!                                     
Break it down
Shout "Bring on the rock!"
Else Whisper "That ain't it, Chief"                 
Break it down
```

## Challenge Approach

Upon going to the website to run the code, an input is demanded. Let's see what's happening...

<img width="960" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/16763f36-e0f4-48d6-a5ed-756a1b7c2a67">

Apparently, listening is input here. From the code, there are some variables that are being compared, and we theoretically could trace the code to see what our variables need to be. But let's cut the gordian knot! We will simply delete the lines that listen for input and that deliver an if-else condition. That will allow us to print what we need.

<img width="960" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/4ecdf3b1-d3e1-4dd0-92c7-0b33bff8d10b">


Then, we can use the same python program from the mus1c challenge to get the flag without a prefix.

```python
list = input().split()

for i in list:
    print(chr(int(i)), end='')
```
