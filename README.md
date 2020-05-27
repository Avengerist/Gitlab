# Gitlab<br>
<h2>Server Configuration</h2><br>

`dhclient`<br>

`systemctl stop firewalld && systemctl disable firewalld`<br>

`setenforce 0`<br>

<h2>Installing necessary utilits</h2><br>

`yum -y install git curl policycoreutils nano openssh-server openssh-clients`

<h2>Downloading installer Gitlab</h2><br>

`curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash`

<h2>Installing Gitlab</h2><br>

`yum -y install gitlab-ce`<br>

<h2>Change Gitlab Configuration</h2><br>

`nano /etc/gitlab/gitlab.rb`<br>

Change *external_url*<br>
It is in the beggining, 29 line.<br>
Example:<br>

`external_url 'http://myowngitlab.com'`

Save & Exit.<br>

After configuration type the command (it will take some time about **3-5 minutes**)<br>

`gitlab-ctl reconfigure`<br>

After the previous command **open Browser** and type **server's IP**. You can check it with command: `ip a`<br>

`192.168.2.2`<br>

Then enter new password (minimum 8 characters).<br>
username: *root*<br>
password: *your_entered_password*<br>

<h2>Create a project</h2><br>

name: *ansible*<br>

project slug: *ansible*<br>

visibility level: *Public*<br>

When you created a project,you will see **Add SSH KEY**. *Add it*.<br>

If you don't see the button, then type:<br>

*http://your_ip_address/profile/keys*<br>

Come back to your machine and type the following command:<br>

`ssh-keygen -t rsa -b 2048`<br>
*Enter-Enter-Enter*<br>

Now you will need to copy your *Public Key*.<br>

`cat /root/.ssh/id_rsa.pub`<br> 

Copy your key (Maybe it will copy with: *CTRL + SHIFT + C*).<br>

Example of my key, your key *will be different*:<br>

`ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC/rbbS6VIqGumHLoNLtAZA9B/a/o/dVGUb0amf5dlluAQpuT88kyh/oKJwpkmTzeJ0hX0bwcOh9JR3EhkNDSHHWFEnhXWZ4lZxjL40300VvVvw6iTHLkk/xlD97Ue5WWpbtVtfZeyOb8S+wkSfZhE6HnMBx3Fd+WG5mLqmWrDINUGuyyxAPN2T4WIe/6Y3mfbUQqY4cL/a1aqr/35nNNSheoLIaa1J8FD6nAfPSgToCMQ7GYwXtDJlo85n8kxg292gH+5owl5kgZB8nKq5flP4/mWqI8uHZeMLJNzYkQh2YgFwnjSI4vVeq2L+I8EMRw8XzCQMl+lWJjMY1gyJqGNZ root@gitlab`<br>

And Paste it in *Gitlab*, Press *Add Key*.<br>

Come back to your project.<br>

Projects-->Your Projects-->Administrator/Ansible(name of project).<br>

Press *Clone* and copy *Clone with SSH*.<br>

Example:<br>

*git@myowngitlab.com:root/ansible.git*<br>

<h2>Open your VM with Gitlab and do the next step</h2><br>

1) `nano /etc/hosts/`<br>

2) Add below: *ip_address_of_gitlab_server myowngitlab.com*<br>

3) Save & Exit.<br>
 
<h2>Do the cloning of your repository</h2><br>

Example:<br>

`git clone git@myowngitlab.com:root/ansible.git`<br>

`cd ansible`<br>

`nano test.txt`</br>

Type something. Save & Exit.<br>

`git add test.txt`<br>

`git config --global user.email "you@example.com"`<br>

`git config --global user.name "Your Name"`<br>

`git commit -m "Something_what_you_want"`<br>

`git push`<br>

If all is successfully loaded then you can check it in **browser where you project**,but you will see an error.<br>

<h2>Fixing an error with page loading</h2><br>

If you see **error** that page is not loaded then you need to **add your domain in hosts** (*myowngitlab.com and ip of it in hosts file on your original(!!!) machine*).<br>

If you use **Windows**, then do the next step.<br>

1) Open with **Notepad**: *c:\Windows\System32\Drivers\etc\hosts*<br>

2) Add in the end: *myowngitlab.com ip_address_of_your_gitlab*<br>

Example:<br>

*myowngitlab.com 192.168.2.2*<br>

3) Save & Exit.<br>

P.S. If you cannot save it there, then you can save it on Desktop and replace it after.<br>

If you use **Linux**:<br>

1) Open /etc/hosts<br>

2) add in the end: myowngitlab.com ip_address<br>

3) Save & Exit<br>

When you did it, *come back to your Browser* where is opened Gitlab and check that you see your text which was typed in *text.txt*.<br>

*G.J.*
