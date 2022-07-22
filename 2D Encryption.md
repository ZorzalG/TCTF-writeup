## Question
> A one time pad is mathematically IMPOSSIBLE to break! Just make sure you only use the key once. (answer should be wrapped in the format T{flag})

gen.py
```
from PIL import Image

img1 = Image.open("plaintext.png")
px1 = img1.load()

img2 = Image.open("2ndmsg.png")
px2 = img2.load()

key = Image.open("key.png")
keypx = key.load()

enc1 = Image.new("RGB",img1.size)
encpx1 = enc1.load()

for y in range(img1.size[1]):
    for x in range(img1.size[0]):
        encpx1[x,y]=(px1[x,y][0]^keypx[x,y][0],
                     px1[x,y][1]^keypx[x,y][1],
                     px1[x,y][2]^keypx[x,y][2])

enc1.save("enc1.png")

enc2 = Image.new("RGB",img2.size)
encpx2 = enc2.load()

for y in range(img2.size[1]):
    for x in range(img2.size[0]):
        encpx2[x,y]=(px2[x,y][0]^keypx[x,y][0],
                     px2[x,y][1]^keypx[x,y][1],
                     px2[x,y][2]^keypx[x,y][2])

enc2.save("enc2.png")
```
[enc1.png](https://cdn.discordapp.com/attachments/999851646983090226/999855385357852723/enc1.png?size=4096)

[enc2.png](https://cdn.discordapp.com/attachments/999851646983090226/999855385685012600/enc2.png?size=4096)

## Solution
Yes, it is true that one time pads are impossible to break, but only when you use them correctly. Here, we've used the key twice, making OTP insecure. The generator 
program takes two images, and XORs them with the same randomly generated key image. If we simply XOR each of these encrypted images, by the properties of XOR, we will find just the 
two unencrypted images XORed with each other, which may reveal the flag. Let's write a script to do exactly that.

Code:
```
from PIL import Image

img1 = Image.open("enc1.png")
px1 = img1.load()

img2 = Image.open("enc2.png")
px2 = img2.load()

flag = Image.new("RGB",img1.size)
fpx = flag.load()


for y in range(img1.size[1]):
    for x in range(img1.size[0]):
        fpx[x,y]=(px1[x,y][0]^px2[x,y][0],
                     px1[x,y][1]^px2[x,y][1],
                     px1[x,y][2]^px2[x,y][2])

flag.save("flag.png")
```
When we open up ```flag.png```, we see:

![](https://cdn.discordapp.com/attachments/999847989952647209/1000114592963375125/unknown.png?size=4096)

The flag is ```T{OopS!MSr5}```

Note: this vulnerability is one of the first examples you can find if you search up "one time pad key used twice."
