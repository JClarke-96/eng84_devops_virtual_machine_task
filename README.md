# Commands
## Vagrant commands
- `vagrant init` to initialise virtual machine
- `vagrant up` to start virtual machine
- `vagrant destroy` to destroy
- `vagrant reload` to reload
- `vagrant status` to check the status
- `vagrant ssh` to enter virtual machine
- `vagrant halt` to end virtual machine

## Linux Commands
- `uname` for username
- `ls` list directory, ls -a list all directories
- `mkdir` make a new directory
- `nano file_name` create file
- `sudo` run commands as admin
- `sudo su` go into admin mode
- `cd` change directory
- `pwd` current location
- `sudo apt-get update -u` update command
- `clear` to clear screen/terminal
- `mv file_name new_name` rename a file to a new name
- `cp file_name folder_name/file_name` copy file from current location to folder in the same directory
- `rm file_name` delete a file
- `mv file_name folder_name` move a file to a different folder
- `chmod +rwx file_name` add permisisons to a file
  - r - read
  - w - write
  - x - execute
- `ll` check current permissions
- `sudo apt-get install nginx` install web server called NGINX

# Jordan's notes
## Automation
## Manual fixes
- Run `npm install` in /home/ubuntu/app/app to install npm correctly
- Run `npm start` in /home/ubuntu/app/app to run the content
- IP:3000/posts to display content in browser

## Create Environment Variables
- `DB_HOST=mongodb://192.168.10.200:27017/posts` creates an environment variable
- `export DB_HOST=mongodb://192.168.10.200:27017/posts` creates persistant variable
- `echo $DB_HOST` shows value of variable

## Reverse Proxy with NGINX
- What is the default location of nginx file that loads nginx page
- `cd /ect/nginx/sites-available/`
- `sudo rm default` deletes default file
- `sudo nano default` creates and opens new default

`server {
	listen 80;

	server_name _;

	location / {
		proxy_pass http://localhost:3000;
		proxy_http_version 1.1;
		proxy_set_header Upgrade $http_upgrade;
		proxy_set_header Connection 'upgrade';
		proxy_set_header Host $host;
		proxy_cache_bypass $http_upgrade;
	}
}`

- `sudo systemctl restart nginx` to restart
- Use default file in same location to use reverse proxy