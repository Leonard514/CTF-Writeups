# Challenge Description

We made a lot of substitutions to encrypt this. Can you decrypt it? Connect with `nc jupiter.challenges.picoctf.org 13758`.
- Hint 1: **Flag is not in the usual flag format**

## Ciphertext (upon connecting via netcat):

```
-------------------------------------------------------------------------------
osjytilk cqtq nk mspt zaiy - ztqbpqjom_nk_o_suqt_aixewi_wjulztlimp
-------------------------------------------------------------------------------
gq gqtq jsl xpoc xstq lcij i bpitlqt sz ij cspt spl sz spt kcnr lnaa gq kig cqt knjv, ijw lcqj n pjwqtklssw zst lcq zntkl lnxq gcil gik xqijl em i kcnr zspjwqtnjy nj lcq kqi.  n xpkl iovjsgaqwyq n ciw citwam qmqk ls assv pr gcqj lcq kqixqj lsaw xq kcq gik knjvnjy; zst ztsx lcq xsxqjl lcil lcqm tilcqt rpl xq njls lcq esil lcij lcil n xnycl eq kinw ls ys nj, xm cqitl gik, ik nl gqtq, wqiw gnlcnj xq, ritlam gnlc ztnycl, ritlam gnlc csttst sz xnjw, ijw lcq lcspyclk sz gcil gik mql eqzstq xq.
```

## Challenge Approach

Initially, I wasn't going for this challenge. I had just completed asm2 and was looking for some information from the pico 2018 video solution playlist (on YouTube) that could dig up hints about what to do with an audio file for **m00nwalk** (since spectrograms, the go-to solution, didn't work). While searching, I stumbled upon [this video](https://www.youtube.com/watch?v=DhA8JBd0tcc&list=PLJ_vkrXdcgH8l7m6PDGxYQm3GHS_5zRmx&index=12) about the pico 2018 challenge **hertz**. I remembered dealing with this challenge, and it all but gave a solution.

The solution is quite simple: Plug the ciphertext into [quipqiup.com](https://quipqiup.com/) and go with it. So that's what I did, and that's all I had to do.
