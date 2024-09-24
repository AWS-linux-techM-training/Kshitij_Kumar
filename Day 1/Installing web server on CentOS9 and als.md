Installing web server on CentOS9 and also configuring YUM Package manager

Step 1 - First we will mount the iso file to VMware.

Then we have to mount that iso file to a directory.
mount /dev/sr0 /mnt

Step 2: Configure the YUM Repository

cd /etc/yum.repos.d/

Create two new repository configuration file
vim local-baseos.repo
    [BaseOS]
    name=Local BaseOS Repository
    baseurl=file:///mnt/BaseOS
    enabled=1
    gpgcheck=0
vim local-appstream.repo
    [AppStream]
    name=Local AppStream Repository
    baseurl=file:///mnt/AppStream
    enabled=1
    gpgcheck=0

Step 3: Verify the Repositories
    yum clean all
    yum repolist

Step 4: Test the Repository Setup by installing apache web server
    yum install httpd

Step 5: Start and Enable Apache
    systemctl start httpd
    systemctl enable httpd
    systemctl status httpd

Step 6: Configure the Firewall 
    firewall-cmd --permanent --add-service=http
    firewall-cmd --permanent --add-service=https
    firewall-cmd --reload

Step 7: Test Apache in Your Browser
    Find the IP address of your CentOS virtual machine:
        ip a
    Access the Apache web server:
        http://<Your ip>


Optional

Step 8: Configure Apache's Document Root
    vi /var/www/html/index.html

    Add html content.   
    Save and exit the file.
    Restart Apache to load your changes:
    systemctl restart httpd