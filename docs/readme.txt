#Ceilometer setup

#Install common components

sudo apt-get install git -y

sudo apt-get install python-dev libssl-dev python-pip git-core libxml2-dev libxslt-dev pkg-config libffi-dev libpq-dev libmysqlclient-dev libvirt-dev graphviz libsqlite3-dev -y

sudo apt-get install jq

#CEPH Installation

git clone https://github.com/theanalyst/ceph-bootstrap

cd ceph-bootstrap

#Add virtual IP address 

-Add entry 10.0.2.15 <hostname> to /etc/hosts

sudo ifconfig eth0:0 10.0.2.15

./ceph-install.sh giant

#Prepare for Devstack Installation

git clone https://github.com/openstack-dev/devstack.git

cd ~/devstack

-copy https://github.com/ceph/ceph-devstack/localrc to ~/devstack/localrc

-set REMOTE_CEPH=True in the copied localrc

-replace CEPH_FSID to the current ceph fsid (use command sudo ceph status)

#Enable Ceilometer Services

-Follow instructions as suggested in http://docs.openstack.org/developer/ceilometer/install/development.html

#Install Devstack

./stack.sh

#Restart Ceilometer Auditing

-restart nova and cinder after changes mentioned in http://docs.openstack.org/developer/ceilometer/install/development.html

-Note: all the above localrc changes are readily available in the checked in localrc to this git site




