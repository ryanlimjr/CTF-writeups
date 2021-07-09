# Space Snacks

## Challenge Type

Misc - 200 pts

This challenge is a 7-part challenge with flags varying between 20 - 50 points

## Challenge Description

Find the answers to the treasure hunt to gain access to the cake in the space cafe.

- specific challenge description for each flag is in the write up

## Write up

### Flag 1

You find a roten apple next to a piece of paper with 13 circles on and some text. What's the message?

```
Vg nccrnef lbh unq jung vg gnxrf gb fbyir gur svefg pyhr
Jryy Qbar fcnpr pnqrg
pgs{Lbh_sbhaq_gur_ebg}
Npprff pbqr cneg 1: QO
```

The first challenge is simple, from the description we can deduce that ROT13 encryption is used, we can simply decrypt it using tools online and we can obtain the flag.

```
It appears you had what it takes to solve the first clue
Well Done space cadet
ctf{You_found_the_rot}
Access code part 1: DB
```

### Flag 2

You find a page with a roman insignia at the top with some text what could it mean?

```
Jhlzhy ulcly dhz clyf nvvk ha opkpun tlzzhnlz.
jam{Aol_vul_aybl_zhshk}
jvkl whya: NW
```

The second challenge is also rather simple, from the description we can deduce that Ceaser Cipher was used, analyzing the cipher text we can guess that the shift is 7 alphabets , `c -> shift 7 -> j`, using tools online we can decrypt the cipher text and obtain the flag

```
Caesar never was very good at hiding messages.
ctf{The_one_true_salad}
code part: GP
```

### Flag 3

You hear the heavy base line of 64 speakers from the next compartment. you walk in and the song changes to writing's on the wall, there is some strange code painted on the wall what could it mean?

```
RXZlbiAgaW4gc3BhY2Ugd2UgbGlrZSB0aGUgYnV0dGVyeSBiaXNjdXQgYmFzZS4gY3Rme0lfbGlrZV90aGVfYnV0dGVyeV9iaXNjdWl0X2Jhc2V9IC4gQWNjZXNzIHBhcnQgMzogWEQ=
```

The third challenge is also simple, from the description and looking at the 'strange code' we can deduce that the message is encoded using base64 encoding. simply decoding the message will reveal the flag to us

```
Even  in space we like the buttery biscut base. ctf{I_like_the_buttery_biscuit_base} . Access part 3: XD
```

### Flag 4

You hear beeps on the radio, maybe someone is trying to communicate? Flag format: CTF:XXXXXX

```
.. -. ... .--. . -.-. - --- .-. / -- --- .-. ... . / .-- --- ..- .-.. -.. / -... . / .--. .-. --- ..- -.. / --- ..-. / -.-- --- ..- .-. / . ..-. ..-. --- .-. - ... .-.-.- / -.-. - ..-. ---... ... .--. .- -.-. . -.. .- ... .... ..--- ----- ..--- .---- / .- -.-. -.-. . ... ... / -.-. --- -.. . ---... / .--- --...
```

The fourth challenge require us to decode morse code which can be done with online tools. Hence we can obtain the flag rather easily

```
INSPECTOR MORSE WOULD BE PROUD OF YOUR EFFORTS. CTF:SPACEDASH2021 ACCESS CODE: J7
```

### Flag 5

You are now in the space cafe, the cake is in the container that should not be here. You can see random names on all the containers. What will Docker never name a container? Note: Please enter it as ctf{full_name}

This challenge is a little tricky, it requires some googling but from this [article](https://medium.com/peptr/why-boring-wozniak-will-never-be-generated-as-a-container-name-in-docker-763b755f9e2a) we find out that the answer (hence flag) is simply `boring_wozniak`

### Flag 6

They ate then cake and left a note with a secret algorithm to unlock the cake treasury. We saw it happening at exactly January 1, 2030 11:23:45 AM... are you the visionary that can figure out the PIN code? PIN code generation algorithm:

```
int generatePin() {
  srand(time(0));
  return rand();
}
```

This challenge requires a good understanding that `time(0)` returns the amount of time (in seconds) since `1 Jan 1970 00:00:00` at that particular instance. hence by calculating the time in seconds from `1 Jan 1970 00:00:00` to `1 Jan 2030 11:23:45` we are able to determine the seed that was used ,1893540225.

Using an online compiler we can modify the code to generate us the pin that was used at that exact moment as the description.

```
int generatePin() {
  srand(1893540225);
  return rand();
}
```

We get the pin as `311084940` which is also the flag.

### Flag 7

The treasury consists of cake hidden on stars in space.

```
* ****  * * * *** ***  **    *  *  * ****  * ** *  ** ***  ** ***  ** * *  *   ** *     *  * ** *  *   ** *     *   **  *   *****  **** *  ***  *  ** * *     *
```

This challenge is rather interesting as we are greated with an message encoded in astericks and spaces. However, after some careful thinking we can deduce that this is another form of a binary string as there is only 2 types of information astericks (0) or spaces (1) converting the above to binary we get.

```
0100001101010100010001100110100001111011011010010110010001100100011001010110111001011111011010010110111001011111011100110111000001100001011000110110010101111101
```

Converting the above binary to ASCII text would reveal the flag.

```
CTF{hidden_in_space}
```

## Flags

1. `ctf{You_found_the_rot}` - 20pts

2. `ctf{The_one_true_salad}` - 25 pts

3. `ctf{I_like_the_buttery_biscuit_base}` - 25pts

4. `CTF:SPACEDASH2021` - 25 pts

5. `ctf{boring_wozniak}` - 25 pts

6. `311084940` - 50pts

7. `CTF{hidden_in_space}` - 30 pts
