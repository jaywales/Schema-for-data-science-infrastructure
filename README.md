# Schema-for-data-science-infrastructure

Dear Future Self,

You need to remember the following steps required to configure your own Jupyter Data Science Notebook Server on Amazon Web Services. This will hopefully become routine part of setting up new projects so these instructions are a safegaurd in case you loose you mind in a some unanticipated deep thought analytical mind-eraser.

First as a refresh- you are a aspiring Data Scientist

Why? to meet the need for the emerging market:


![image](https://user-images.githubusercontent.com/40584489/43021330-20731280-8c18-11e8-97c4-3fe2a5e84acc.png)

![image](https://user-images.githubusercontent.com/40584489/43021258-dab50e42-8c17-11e8-9f85-b5fbb7daf826.png)


So, now you will need to set up a set of SSH keys, as you recall  this will allow you to access your notebook from anywhere through you own URL located on the Amazon Web Services.

## 1. set up a set of SSH keys

Open GitBash, I loaded it on your computer last time, at a command line you create a key pair using ssh, first check if they are already created... 
![image](https://user-images.githubusercontent.com/40584489/43021515-b700f30c-8c18-11e8-9136-4da6d3bce208.png)
If you don't see id_rsa, Id.rsa.pub you need to create them in step 1.5, if they are there skip to step 2

### 1.5 generating new key pair
Mkdir -p .ssh and then ssh-keygen
![image](https://user-images.githubusercontent.com/40584489/43021712-884e696c-8c19-11e8-97d3-bdab5417023f.png)

Next it asks twice for a passphrase, which you should leave empty so you don’t have to type a password when you use the key.

Type in at the prompt:

$ cat~.ssh/id_rsa.pub 

and you will see:

$ cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAklOUpkDHrfHY17SbrmTIpNLTGK9Tjom/BWDSU
GPl+nafzlHDTYW7hdI4yZ5ew18JH4JW9jbhUFrviQzM7xlELEVf4h9lFX5QVkbPppSwg0cda3
Pbv7kOdJ/MTyBlWXFCR+HAo3FXRitBqxiX1nKhXpHAZsMciLq8V6RjsNAQwdsdMFvSlVK/7XA
t3FaoJoAsncM1Q9x5+3V0Ww68/eIFmb1zuUFljQJKprrX88XypNDvjYNby6vw/Pb0rwert/En
mZ+AW4OZPnTPI89ZPmVMLuayrD2cE86Z/il8b+gw3r3+1nKatmIkjn2so1d01QraTlMqVSsbx
NrRFi9wrf+M7Q==  Jay Wales@LAPTOP-JCU35373

PASTE THIS INTO Github from your clipboard:

![image](https://user-images.githubusercontent.com/40584489/43025632-5e3c2c82-8c27-11e8-81d0-cba083914f5c.png)


call this key "Lenovo personal" or if Josh has finally brainwashed you that Macs are better then "Personal MacBook Pro".

Paste your key into the "Key" field.
find the Add key button...go ahead and Click Add SSH key!

now back to the command line and:


$cp ~/.ssh/id_rsa.pub ~/Desktop/

$ ssh git@github.com

$Less ~/.ssh/known_host

$Q to quit

Finally, in the next step you take that long string that was added to Github and you will also paste at AWS to link to your notebook...Don't forget EC2 where we make servers; S3 is where we store them
****If you know how to make a server don’t need EFS!!!!

## 2. set up an Amazon EC 2

Once you are logged into to Amazon Web Services (AWS) find the EC2 dashboard as shown here:
![image](https://user-images.githubusercontent.com/40584489/43027061-53428398-8c2d-11e8-89da-74ad93f27a2d.png)

if needed Goto EC2 to import key pair and name as above for simplicty


You can check for running instances as you see here, make sure you are checking the regions (last time it defaluted to Ohio and that is where you created your first instance....awh.

![image](https://user-images.githubusercontent.com/40584489/43027223-0ab3e382-8c2e-11e8-9639-edb82ebf6783.png)

next you are offered your choice of operating system and virtual hard drive, Ububtu 16.04 is a good choice and is free tier eligible:

![image](https://user-images.githubusercontent.com/40584489/43027347-a04e0bfc-8c2e-11e8-8700-bc3c4845f0d6.png)

next Choose an Instance Type: T2 Micro is the free tier eligible and works for most projects
If needed Add Storage, Add Tags...otherwise defaults are fine

next Configure Security Group

### 3. Security Groups: set up the ports like this

![image](https://user-images.githubusercontent.com/40584489/43027794-0ef48a52-8c31-11e8-840e-6f0495533869.png)

##### Wait Don’t use 27017 for Mongo Servers that is where the KGB/hackers always look!

![image](https://user-images.githubusercontent.com/40584489/43027893-7bdc3c28-8c31-11e8-85e1-c77c65b7c94c.png)

That's better...

### 4. AWS Operating System
Come on now you remember, the AWS operating system that you chose was Ubuntu 16.04, I/you just said that! 

now before we leave the AWS site we need to grab the public IP address, take a look at the instance, everything looks good :

![image](https://user-images.githubusercontent.com/40584489/43029943-cf61a9f6-8c3f-11e8-8585-33f499746ffc.png)

copy the Public IP address to the clipboard to be used in the next step

Alright go back to Bash or Tmux (if you can handle it?)

 $ ssh ubuntu
 
 ![image](https://user-images.githubusercontent.com/40584489/43031763-222dbbc6-8c5d-11e8-9e9c-2494008dbf8a.png)

  ![image](https://user-images.githubusercontent.com/40584489/43032205-7184277e-8c66-11e8-9140-c36439c1ed34.png)
  
  now proceed to the next step, time to install Docker!

### 5. Docker Installation- these steps should seem familiar, 

 Now that you have Launch a new EC2
	1. we will Provision new instance w/Docker
	2. Pull the ds-nb  image ...ds-nb (datascience notebook)
	3. Run a ds-nb container
  4. Get the token & use Jupyter
  
$ curl -sSL httosL//get.docker.com | sh

$ #!/bin/sh ….shbang bin /shell

$ curl -sSL https://get.docker.com | sh

$ Sudo usermod -aG docker ubuntu

Ctrl D

#### Now pay attention, don't forget to Ctrl-D to exit the system, this allows “the pending input to get the application” when you reenter:

![image](https://user-images.githubusercontent.com/40584489/43032102-bf3eef2e-8c63-11e8-87c0-52d6547c3dff.png)

Up arrow to reconnect with a $ ssh ubuntu@18.222.193.161

The IP address that we copied goes here at the end of $ssh ubuntu@IPaddress:

$ ssh ubuntu@18.222.193.161

### 6. Obtaining the correct Docker image

$ Docker system prune

$ docker pull jupyter/datascience-notebook

### 7. Running the correct Docker image as a container

$ Docker run: 
docker run -p 443:8888 -v /home/ubuntu:/home/jovyan jupyter/datascience-notebook

$ Docker -Vi .profile  (note $ :wq exit or :q! or :!)

echo 'alias j="docker run -d -p 443:8888 -v /home/ubuntu:/home/jovyan jupyter/datascience-notebook"' >> .profile

$source .profile

$ Docker pull hello-world
$ Docker run hello-world

![image](https://user-images.githubusercontent.com/40584489/43032305-8a0ff082-8c68-11e8-8995-1a0c629d1cea.png)

### 8. Jupyter notebook security concerns

http://localhost:8889/?token=7c59b9c87d7d5bd289766f3fc379401e747e5d631aeb9a39 :: /home/jovyan
Check your the token:
7c59b9c87d7d5bd289766f3fc379401e747e5d631aeb9a39

you can check from Bash if you have any more concerns:

$ docker exec -it 12 jupyter notebook list

### 9. Anything else I may have forgotten ...

Get started and open a notebook:

open the URL you created: 18.222.193.161:443

### 10. Create at least one diagram of your overall system.

![image](https://user-images.githubusercontent.com/40584489/43032256-780ec94a-8c67-11e8-8556-f56e70a6fd8d.png)

### 11. A detailed budget of the costs of running a Jupyter Data Science Notebook Server for three months using at least three different kinds of EC 2 instances.

Compute: Amazon EC2 Instances:
 AWS Comparison 			
 
 ![image](https://user-images.githubusercontent.com/40584489/43033077-5e683952-8c78-11e8-9ea9-66958932507f.png)
 
 
 
 
 
Type	   vCPU	ECU	Memory (GiB)	Instance  Storage (GB)	    Linux/UNIX Usage	per Month	3 Months
t2.nano	  1	   Variable	0.5 GiB	EBS Only	$0.0058 per Hour	                    $4.25	$12.75
t2.micro	1	   Variable	1 GiB	  EBS Only	$0.0116 per Hour	                    $8.50	$25.50
t2.large	2	   Variable	8 GiB	  EBS Only	$0.0928 per Hour	                    $67.93	$203.79
m4.large	2	    6.5	    8 GiB	  EBS Only	$0.10 per Hour	                      $73.20	$219.60

