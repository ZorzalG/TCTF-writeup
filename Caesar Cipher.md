## Question
> I learned that Caesar used a cipher to keep his messages secret. Instead of 13, I'll use my favorite number instead.
Decrypt this message: A{jfwoly_sprl_opa_nhtl_chsvyhua!?!?_z5JGbQQWj6}
## Solution
A Caesar Cipher is an encryption method that takes every letter, and shifts it a certain amount of letters left or right. If the letter is shifted past A or Z, it "wraps around."
For example: the string "abcxyz" shifted by 3 to the right would be encrypted as "defabc"
To decrypt the flag, we can just try multiple shifts on the encrypted flag.

Searching up "caesar cipher solver" gives us a tool (dcode.fr) that we can plug the encrypted message into, and solve.

![](https://cdn.discordapp.com/attachments/999847989952647209/1000103034002616360/unknown.png?size=4096)

![](https://cdn.discordapp.com/attachments/999847989952647209/1000104720129597470/unknown.png?size=4096)

The flag is ```T{cypher_like_hit_game_valorant!?!?_s5CZuJJPc6}```
