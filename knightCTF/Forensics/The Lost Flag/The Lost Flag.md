# The Lost Flag

## Challenge type

### Forensics - 25pts

## Challenge Description

We recovered a image file from an incident. There might be something interesting in the file. Give it a try.

Flag Format: KCTF{pla1n_t3xt_here}

## Write up

We were given a PNG file as shown.

![Challenge image](res/Lost%20Flag%20.png)

This could be a case of hidden bits within the image so by putting the image through Stegsolve and cycling through the filters, we indeed found 
the flag as shown below.

![hidden flag](res/Hidden_flag.jpg)

And the flag is `KCTF{Y0U_F0uNd_M3}`.