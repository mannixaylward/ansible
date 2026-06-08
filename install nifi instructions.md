#Install Java 21
ansible-playbook --ask-become-pass install_java21.yml

#update /etc/environment
JAVA_HOME="/usr/lib/jvm/java-1.21.0-openjdk-amd64"

#Install nifi
ansible-playbook --ask-become-pass download_extract_nifi2.yml

#Prepare nifi
sudo ln -s /opt/nifi-2.9.0/ /opt/nifi
sudo vi /opt/nifi/conf/nifi.properties

Update this from/to
nifi.web.https.host=localhost
nifi.web.https.host=10.1.4.101

Update this from/to
nifi.web.proxy.host=
nifi.web.proxy.host=10.1.4.101:8443

#Start nifi in foreground
sudo /opt/nifi/bin/nifi.sh run

Tail the log file
tail -f /opt/nifi/logs/nifi-app.log

#Capture this information
Generated Username [f2673f5f-e48a-4ffe-8244-a45eeac2d6f0]
Generated Password [fqMwoQRw5Q1KuFY1DEmVUVi2kcYoPwPV]

sudo /opt/nifi/bin/nifi.sh set-single-user-credentials admin adminpassword

#restart nifi.