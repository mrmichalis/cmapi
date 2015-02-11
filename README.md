----
``` bash
usage: cmxDeploy.py -u "root" -p "cloudera" -m "CM-SERVER-IP" -w "ip1,ip2,ip3,..."
```
----

#### pre-requisite

You have a running Cloudera Manager Server with embedded database started-up. You can use the preferred option as documented in ["Installation Path B - Manual Installation Using Cloudera Manager Packages"] [1](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Installation-Guide/cm5ig_install_path_B.html?scroll=cmig_topic_6_6), or easier option using ["Installation Path A - Automated Installation by Cloudera Manager
"] [2](http://www.cloudera.com/content/cloudera-content/cloudera-docs/CM5/latest/Cloudera-Manager-Installation-Guide/cm5ig_install_path_A.html)

#### TL;DR: copy-and-paste below Example in RHEL/CentOS
``` bash
yum install -y git python-setuptools
easy_install pip
git clone https://github.com/cloudera/cm_api.git $HOME/cm_api && pip install $HOME/cm_api/python
curl -L https://raw.githubusercontent.com/gdgt/cmapi/master/bootstrap-cm.sh | bash
curl -L https://raw.githubusercontent.com/gdgt/cmapi/master/cmxDeploy.py -o $HOME/cmxDeploy.py && chmod +x $HOME/cmxDeploy.py
python $HOME/cmxDeploy.py -u "root" -p "cloudera" -m "cm-ip" -w "ip1,ip2,ip3,..."
```
- SSH credentials - this allows CM to configure the rest of the hosts -u/--ssh-root-user, -p/--ssh-root-password **OR** -k/--ssh-private-key
- create Hive in embedded PosgreSQL database, bash script provided below (also included in [bootstrap-cm.sh](https://github.com/gdgt/cmapi/blob/master/bootstrap-cm.sh#L13-L21)). 

#### Usage
``` bash
Usage: cmxDeploy.py [options]

Options:
  -h, --help                show this help message and exit
  -m CM_SERVER,         --cm-server=CM_SERVER
                            *Set Cloudera Manager Server Host.
                            Note: This is the host where the Cloudera Management Services get installed.
  -w HOST_NAMES,        --host-names=HOST_NAMES
                            *Set target node(s) list, separate with comma eg: -w
                            "host1,host2,...,host(n)". 
                            Notes: 
                             - enclose in double quote, also avoid leaving spaces between commas.
                             - CM_SERVER excluded in this list, if you want install CDH Services in CM_SERVER 
                             add the host to this list..
  -n CLUSTER_NAME,      --cluster-name=CLUSTER_NAME
                            Set Cloudera Manager Cluster name enclosed in double
                            quotes. Default "Cluster 1"
  -p SSH_ROOT_PASSWORD, --ssh-root-password=SSH_ROOT_PASSWORD
                            *Set target node(s) ssh password..
  -u SSH_ROOT_USER,     --ssh-root-user=SSH_ROOT_USER
                            Set target node(s) ssh username. Default "root"
  -k SSH_PRIVATE_KEY,   --ssh-private-key=SSH_PRIVATE_KEY
                            The private key to authenticate with the hosts.
                            Specify either this OR a password.
  -l LICENSE_FILE,      --license-file=LICENSE_FILE
                            Cloudera Manager License file name
  -d, --teardown            Teardown Cloudera Manager Cluster. Required arguments "keep_cluster" or "remove_cluster".
```
## References
https://raw.githubusercontent.com/justinhayes/cm_api/master/python/examples/auto-deploy/deploycloudera.py

https://github.com/eBay/hadrian

----