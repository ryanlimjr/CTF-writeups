# Enumerating the Cloud

## Challenge type 

Cloud - 125 pts

This challenge is a 4-part challenge with each flag worth 25 pts.

## Challenge Description

The spaceship that you will use in SPACE RACE is almost ready. One of the last steps is to verify that all of the systems are operational. Unfortunately, the AI controlling the system information decided to take a personal time off for a few days, leaving you without an easy access to the spaceship systems. This is not a problem because, as the cyber security specialist in the ship, you know the spaceship cloud infrastructure like the back of your hand.

Flag 1 - Your spaceship is located [here](http://planet-bucket-43b2a07.s3-website-eu-west-1.amazonaws.com/), can you find the external information panel?

Flag 2 - You have gained access to the external infromation endpoint. Can you access the spaceship logs to obtain the access keys?

Flag 3 - You have managed to access the spaceship. You see a cleaning bucket, the Lambda Thrusters information panel tag and the E-space Computing Cloud system tags. What does the tag in the cleaning bucket says?

Flag 4 - What is the tag in the Lambda Thrusters information panel?

Flag 5 - What is the tag in the E-space Cloud Computing System?

## write up

From the challenge description we are given the following link.

```
http://planet-bucket-43b2a07.s3-website-eu-west-1.amazonaws.com/
```

From the link it is obvious that we are dealing with another challenge involving Amazon Web services.

Clicking on the link would lead us to the following landing page.

![landing page](res/landingpage.png)

Doesn't seem like much, lets explore the source code of the page.

![source code of page](res/sourcecode.png)

aha! it seems like we have found another S3 bucket of interest to us. accessing the bucket we get to the XML file stored in the bucket and we see several things of interest.

![Objects in bucket](res/objectsinbuckets.png)

Downloading the flag.txt file and we have obtained our first flag 

```
CTF{0841862f273fd2ca20ea3b94a645781071ab19d7}
```

Downloading the `external-information-panel.txt` we can find the following link

```
https://g0341x75tb.execute-api.eu-west-1.amazonaws.com/logs
```

However it seems like accessing this link is not going to be easy as we get a 405 error stating GET method is not allowed. Doing some trial and error we are able to obtain the logs file by using `curl` with the PUT option : 

```
curl -X PUT https://g0341x75tb.execute-api.eu-west-1.amazonaws.com/logs
```

Redirecting the output into a text file and opening it we can find our second flag -

```
CTF{9177a9c8bb1cd5c85934}
```

Scrolling through the logs we find another area of interest, Access key ID and Secret access key!

![secret](res/secret.png)

Log in to the account associated with the keys using the command `aws configure`.

For the third flag, the challenge description seems to give us a hint that we should be looking into an S3 bucket 'What does the tag in the cleaning _bucket_ says?'.

Doing the following command `aws s3 ls` would indeed reveal another S3 bucket.

![cleaning bucket](res/cleaningbucket.png)

To find the tag we simply issue the following command 

```
aws s3api get-bucket-tagging --bucket cleaningbucket-cf2be35
```

And we can obtain the third flag from the output that is displayed

```
CTF_855cc724fd34896c8875
```

![ec2 tags](res/s3tag.jpg)

For the fourth flag, we are given a hint to look into the tags of the Lambda services associated with this AWS ID, 'tag in the _Lambda_ Thrusters information panel.'.

Lets list the functions that are available using the following command 

```
aws lambda list-functions
```

![List of lambda functions](res/lambdafunctions.jpg)

We can observe that there is function named `lamdaThrusters` which is of interest to us, taking note of the FunctionARN. we can get the tag of the function by using using the following command 

```
aws lambda list-tags --resource <FunctionARN>
```

And we can obtain the fourth flag from the output that is displayed

```
CTF_20324408a4e3f5c1d54d
```
![ec2 tags](res/lambdatag.jpg)

For the final flag, doing some quick googling about Amazon's "E-space Cloud Computing System" we deduce that we should be looking into the tags of the EC2 services associated with the AWS Id.

Doing a quick look up of the AWS CLI documentation we can try to issue the following command 

```
aws ec2 describe-tags
```

And we can see the flag that is displayed to us in the output 

```
CTF_98f960b4d86bbcfe3fe1
```

![ec2 tags](res/ec2tag.jpg)


## Flags

1. `CTF{0841862f273fd2ca20ea3b94a645781071ab19d7}` - 25 pts

2. `CTF{9177a9c8bb1cd5c85934}` - 25pts
 
3. `CTF_855cc724fd34896c8875` - 25 pts

4. `CTF_20324408a4e3f5c1d54d` - 25 pts

5. `CTF_98f960b4d86bbcfe3fe1` - 25 pts
