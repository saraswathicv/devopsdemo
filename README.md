# devopsdemo on 21st Jan 2019

This Excercise will be carried over ubuntu tlarge or txlarge ec2 machine

To Configure Node using UserName and Password in Jenkins. Make sure to perform below actions in ubuntu traget machie
      
      sudo vi /etc/ssh/sshd_config
      sudo passwd ubuntu
      sudo service sshd restart

Find the Line containing “PasswordAuthentication” parameter and change its value from “no” to “yes“
     
     PasswordAuthentication yes
In Jenkins job  configuration mention node label under Restrict where this project can be run

Add Maven Installations as below under Global Tool configuration of Jenkins
      
      Name: MavenHome
      Maven_Home: /usr/share/maven

Install Ansible Playbook plugin in Jenkins and add Ansible installation details in Global Tool configuration of Jenkins

    Name: Ansible
    Path to ansible executables directory: /usr/bin
    
 Jforg:
     1.  Create a Repo in Artifactory by name "helloworld" of Maven type
     2. update Maven settings.xml configuration to mention the repo and snapshot user details in target machine
          
          suod vi /usr/share/maven/conf/settings.xml
              ===
              <server>
                <id>central</id>
                      <username>admin</username>
                      <password>Wipro@123</password>
              </server>

              <server>
                      <id>snapshots</id>
                      <username>admin</username>
                      <password>Wipro@123</password>
              </server>
    
 To Build Appliction in Build section of Jenkins select "Invoke Top-level Maven Targets"
 
     Maven version: MavenHome(same as installation label provided in gloabl tool configuration)
     Goals: package(to build application)
     Goals:sonar:sonar(to perform sonarqube anlaysis)
     Goals: deploy( to upload artifacts to Jfrog)
     
 To Deploy application using Ansible
 
  select Invoke Ansible Playbook in Build section of Jenkins congiguration page
  
        Ansible installation: Ansible( same as Ansible installations mention in global tool configuration)
        Playbook Path: deploy.yaml(yaml file name in your source code)
        Host Subnet:IP adress where Ansible installed
  
  Install sshpass program on target ubuntu machine
      
        sudo apt-get install sshpass
        
1. Add the target host details /etc/ansible/hosts

    <IP> ansible_connection=ssh ansible_user=ubuntu ansible_password=<PASSWORD>
     e.x. 13.233.225.189 ansible_connection=ssh ansible_user=ubuntu ansible_password=Wipro@123
  
2. Disable host_key_checking : /etc/ansible/ansible.cfg
           
           [defaults]
  	    host_key_checking = False
        
3. Add/update Artifactory ip details in deploy.yaml
        
 
  
    
