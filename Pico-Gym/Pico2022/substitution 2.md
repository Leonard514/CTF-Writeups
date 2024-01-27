# Challenge Description

It seems that another encrypted message has been intercepted. The encryptor seems to have learned their lesson though and now there isn't any punctuation! Can you still crack the cipher?
- Hint 1: Try refining your frequency attack, maybe analyzing groups of letters would improve your results?

# Message Text

```
isnfnnpctitnznfmxhisnfwnxxntimjxctsnascdstushhxuhgqbinftnubfciruhgqnicichktckuxbackdurjnfqmifchimkabturjnfusmxxnkdnisntnuhgqnicichktehubtqfcgmfcxrhktrtingtmagckctifmichkebkamgnkimxtwscusmfnznfrbtnebxmkagmfonimjxntocxxtshwnznfwnjnxcnznisnqfhqnfqbfqhtnhemscdstushhxuhgqbinftnubfciruhgqnicichkctkhihkxrihinmuszmxbmjxntocxxtjbimxthihdnitibankitckinfntinackmkanpucinamjhbiuhgqbinftucnkunanenktcznuhgqnicichktmfnheinkxmjhfchbtmeemcftmkauhgnahwkihfbkkckdusnuoxctitmkanpnubickduhkecdtufcqitheenktnhkisnhisnfsmkactsnmzcxrehubtnahknpqxhfmichkmkacgqfhzctmichkmkaheinksmtnxngnkitheqxmrwnjnxcnznmuhgqnicichkihbusckdhkisnheenktcznnxngnkitheuhgqbinftnubfcirctisnfnehfnmjniinfznscuxnehfinusnzmkdnxctgihtibankitckmgnfcumkscdstushhxtebfisnfwnjnxcnznismimkbkanftimkackdheheenktczninuskcvbntctnttnkicmxehfghbkickdmkneenuicznanenktnmkaismiisnihhxtmkauhkecdbfmichkehubtnkuhbkinfnackanenktcznuhgqnicichktahntkhixnmatibankitihokhwisncfnkngrmtneenuicznxrmtinmusckdisngihmuicznxrisckoxconmkmiimuonfqcuhuiectmkheenktcznxrhfcnkinascdstushhxuhgqbinftnubfciruhgqnicichkismitnnotihdnknfminckinfntickuhgqbinftucnkunmghkdscdstushhxnftinmusckdisngnkhbdsmjhbiuhgqbinftnubfcirihqcvbnisncfubfchtcirghiczmickdisngihnpqxhfnhkisncfhwkmkankmjxckdisngihjniinfanenkaisncfgmusckntisnexmdctqcuhUIE{K6F4G_4K41R515_15_73A10B5_702E03EU}
```

# Challenge approach

I started out by going to [quipqiup.com](quipqiup.com) since this is how the previous two substitution challenges were solved. They are not documented here, because they consisted of one step: putting the challenge text into the repository. This time, however, it was not so simple because quipqiup apparently got confused by the presence of numbers and underscores in the flag (meaning salvaging the flag was required):

<img width="960" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/ddb9451d-cea3-43fa-aad4-47b3009fa85c">

I then took a look at the first two words: **there exist**. Initially I expected the space to be substituted by an alphanumeric character, but I found through the patterns of the letter **n** in **isnfnnpcti** (where n maps to e) that the message text simply doesn't account for spaces at all.


I then took a look at the previous challenge substitution1 (not documented here) and found that case-sentitivity was turned off, and that numbers and underscores were not touched.

<img width="769" alt="image" src="https://github.com/Leonard514/CTF-Writeups/assets/92343899/7a75fda9-6763-4f39-98f4-9c7185b727de">


Therefore, the task was relatively simple: use the encrypted flag, keep the numbers and underscores, and find the bindings for the alphabetic characters using parts of the decrypted ciphertext. I went about storing the relevant text mappings in a notepad text buffer (mostly since a challenge which calls for brains and a web-based tool doesn't call for a Linux VM). I went about this carefully, making sure that the translated flag made some sense. And that is the challenge!

```
qcuhUIE{K6F4G_4K41R515_15_73A10B5_702E03EU}


k --> n
g --> m
r --> y
a --> d

FLAG REDACTED
```
