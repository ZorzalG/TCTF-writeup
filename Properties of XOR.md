## Question
> The XOR operator has several mathematical properties that make it useful in cryptography. I'd advise you look into them.

gen.py
```
from Crypto.Util.number import *
import random

def generateKey(n):
    st=""
    bits=[0,1]
    for i in range(n*8):
        st = st + str(bits[random.randint(0,1)])
    return int(st , 2)

flag = open('flag.txt','rb').read()
plaintext = bytes_to_long(flag)

fakeflag = b'S{lmaoooo_what_if_this_was_the_real_one_and_you_spend_hours_trying_to_get_the_real_but_actually_fake_flag}'

fakept = bytes_to_long(fakeflag)

key=generateKey(106)

result1 = (fakept^key)

result2 = (plaintext^key)

print("r1",result1)
print("r2",result2)
```
output.txt
```
r1 1287700650464624372641928860853029159130135871642599871106140424838355508958751131459880932702163566392747280125007986341932270670931585052562381648065523684221407726587836869816717495851103579837525168622593905064847357366509864857038850353962197275763400
r2 1236377358734755488487361957766125148520385293459893017715387958141845987737057965300979571491603015854886455859446169260120512690138578591661168033297749906307105490242905235922818327757280448824493516020662650905863639424052924895679314785145237462426824
```
## Solution
We know that ```a XOR (^) a = 0```, and also that ```a^b^c = a^c^b``` and ```a^0=a```, so we can take ```r1```, which is ```fakept^key```, and XOR it with ```fakept``` again to get the key itself. Then, we can XOR the key with ```r2``` to get the plaintext.

Code:
```
from Crypto.Util.number import *
fakeflag = b'S{lmaoooo_what_if_this_was_the_real_one_and_you_spend_hours_trying_to_get_the_real_but_actually_fake_flag}'
fakept = bytes_to_long(fakeflag)

r1=1287700650464624372641928860853029159130135871642599871106140424838355508958751131459880932702163566392747280125007986341932270670931585052562381648065523684221407726587836869816717495851103579837525168622593905064847357366509864857038850353962197275763400
r2=1236377358734755488487361957766125148520385293459893017715387958141845987737057965300979571491603015854886455859446169260120512690138578591661168033297749906307105490242905235922818327757280448824493516020662650905863639424052924895679314785145237462426824
print(long_to_bytes(r1^fakept^r2))
```
The flag is ```T{y0u_didnt_actually_think_the_fake_flag_was_the_real_one_right?_id_have_to_be_really_dumb_to_do_that!!!!}```
