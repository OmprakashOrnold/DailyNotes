# Linux OS

* It is community based OS
* Linux is free & open source
* Linux is Multi User based OS
* Security features are very good in linux
	(Anti-virus not required)
* Linux is CLI based OS (Command Line Interface)
* It is highly recommended to run servers

	Ex : database, web server, docker, jenkins, k8s, sonar, nexus
## Linux History  

* Linux OS developed by '**Linus Torvalds**'
* Unix OS
* Minux
* (Li) nus Torvals + Mi(nux) = Linux

### Linus Torvalds released linux os into market with source code...

* Many s/w companies downloaded linux source code and modified according to their requirement and released into market with their brand names those are called as 'Linux Distributions'


                      - Amazon Linux
				- Ubuntu
				- Red Hat (community & enterprise)
				- Fedora
				- CentOS
				- SUSE
				- Kali
				- Debian ..... 200+


## Environment setup	

1) Create Account in AWS 

2) Create Linux Virtual Machine using AWS EC2

3) Connect with Linux Virtual machine using MobaXterm/Putty		

## Linux CommandS

1) **whoami** : To display logged in username

2) **date** : display current date

3) **cal** : display calendar with current month

4) **pwd** : display present working directory

5) **ls** : list files and directories of pwd

				 ls
				 ls -l
				 ls -lr
				 ls -lt
				 ls -ltr

6) **cd** : change directory

			 cd <dirname>

			 cd ..

7) **mkdir** : To create directory

		 mkdir java

8) **rmdir** : To delete empty directory

9) **touch** : To create empty files

			  touch f1.txt

			  touch f2.txt f3.txt f4.txt		

10) **cat** : To create files + append data + display data

			 cat > java.txt

			 cat >> java.txt

			 cat java.txt	

			 cat -n java.txt

11) **cp** : To copy file data

			cp <src-file> <target-file>

12) **mv** : To rename files/directories + To move files/directories

			mv f1.txt f11.txt

		    mv f1.txt mydata			

13) **rm** : To remove files and non-empty directories	

			rm <file-name>

			rm -r <dir-name>

14) **head** : Print top 10 lines of file data

		      head a1.txt
			  head -n 15 a1.txt

15) **tail** : Print last 10 lines of file data

			tail a1.txt
			tail -n 30 a1.txt

16) **grep** : Print file data based on pattern match

			grep "AWS" a1.txt

		    grep -i "aws" a1.txt

### Note: To see exception messages in log file we will use 'grep' command.

			$ grep -i "exception"	app.log

17) **vi** : Visual Editor (text editor)

			$ vi <file-name>

			command mode : only read + delete

			insert mode : press 'i' (modifications allowed)

			esc mode : press 'esc'

					:wq => write and quit

					:q! => close without 

18) **ifconfig** : To get ip address

19) **ping** : To check connectivity

20) **wget** : To download files using url

21) **curl** : To send HTTP request

## Package Managers in Linux

- Package managers are used to install softwares in Linux machine

	        amazon linux / red hat : yum
	
			ubuntu / debian : apt

		 install git client
 
		 sudo yum install git
 
		 git --version

		 install maven
	 
		 sudo yum install maven
 
		 mvn --version
	 
		 java --version
	
## How to deploy Spring Boot application in Linux VM

1) Clone Git Repo

		$ git clone https://github.com/ashokitschool/sb_log_app.git

2) Build app using maven

		$ cd sb_log_app
		$ mvn clean package

3) Run the jar file

		$ java -jar target/sb-log-app.jar

4) Enable Embedded Server port num in security group inbound rule

5) Access application in browser.

			URL : http://public-ip:port/welcome


