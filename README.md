launch redhat 8 ec2 instance
image: ami-0619404f9180a28b3

Installing cdp 

pre-requiste:

sudo yum install wget -y

sudo sysctl -a | grep vm.swappiness

 sudo su -c 'cat >>/etc/sysctl.conf <<EOL
 'vm.swappiness=1' 
EOL' 

sudo sysctl -p

echo "echo never > /sys/kernel/mm/transparent_hugepage/defrag" | sudo tee -a /etc/rc.d/rc.local
echo "echo never > /sys/kernel/mm/transparent_hugepage/enabled" | sudo tee -a /etc/rc.d/rc.local


# Make rc.local executable
sudo chmod +x /etc/rc.d/rc.local

cat /sys/kernel/mm/transparent_hugepage/enabled
cat /sys/kernel/mm/transparent_hugepage/defrag

# Update SELinux configuration to disable it
echo "SELINUX=disabled" | sudo tee /etc/selinux/config

sestatus

sudo su -c "touch /home/centos/.ssh/config; echo -e 'Host *\n  StrictHostKeyChecking no\n  UserKnownHostsFile=/dev/null' >> /home/centos/.ssh/config"

echo -e  'y\n'| ssh-keygen -t rsa -P "" -f $HOME/.ssh/id_rsa

cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys

sudo systemctl restart sshd.service

1. Take machine with pre requisits done 
2. wget https://archive.cloudera.com/cm7/7.4.4/cloudera-manager-installer.bin

3.after downloading  installer bin (step2) use below url steps.
https://docs.cloudera.com/cdp-private-cloud-base/7.1.7/installation/topics/cdp-quick-start-streams-run-cm-server-installer.html

4. For web cm run time installation use below url
https://docs.cloudera.com/cdp-private-cloud-base/7.1.7/installation/topics/cdp-quick-start-deployment-streams-install-runtime.html[cloudera.bin (1).txt](https://github.com/user-attachments/files/17243303/cloudera.bin.1.txt)
