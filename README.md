# DEPRECATED
## This repo is no longer maintained.<br>For a list of current demos, please visit:<br>https://gitlab.com/cumulus-consulting/goldenturtle/<br><br><br>

Routing On the Host (RoH) Demo
===========================

This demo shows a topology using 'Routing on the Host' to add host reachability directly into a BGP routed fabric. Switches are Cumulus Linux and servers running Ubuntu. This playbook configures a CLOS topology running BGP unnumbered in the fabric with numbered links towards the hosts, and installs a webserver on one of the hosts to serve as a Hello World example. The Ubunut server acts as the host to redistribute kernel routes as /32 host routes into the routing table when VMs or containers become available. When the demo runs successfully, any server on the network should be able to access the webserver via the BGP routes established over the fabric.

This demo is written for the [cldemo-vagrant](https://github.com/cumulusnetworks/cldemo-vagrant) reference topology and applies the reference BGP unnumbered configuration from [cldemo-config-routing](https://github.com/cumulusnetworks/cldemo-config-routing).


Quickstart: Run the demo
------------------------
Before running this demo, install [VirtualBox](https://www.virtualbox.org/wiki/Download_Old_Builds) and [Vagrant](https://releases.hashicorp.com/vagrant/). The currently supported versions of VirtualBox and Vagrant can be found on the [cldemo-vagrant](https://github.com/cumulusnetworks/cldemo-vagrant).

    ### Bring up the vagrant topology
    git clone https://github.com/cumulusnetworks/cldemo-vagrant
    cd cldemo-vagrant
    vagrant up oob-mgmt-server oob-mgmt-switch leaf01 leaf02 spine01 spine02 server01 server02

    ### setup oob mgmt server
    vagrant ssh oob-mgmt-server

    ### Run the ROH demo
    git clone https://github.com/cumulusnetworks/cldemo-roh-ansible
    cd cldemo-roh-ansible
    ansible-playbook run-demo.yml

    ### check reachability of server02 from server01
    ssh server01
    wget 10.0.0.32
    cat index.html
