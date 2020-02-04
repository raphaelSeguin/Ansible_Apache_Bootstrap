Role Name
=========

Installation de Jenkins et de ses dépendances.

Requirements
------------

    apt-get update
    apt-get install -y openjdk-8-jdk git
    curl -s -LO https://www-us.apache.org/dist/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
    tar -xzf apache-maven-3.6.3-bin.tar.gz -C /opt/
    echo 'export MAVEN_HOME=/opt/apache-maven-3.6.3' > /etc/profile.d/mvn.sh
    echo 'export PATH=$PATH:$MAVEN_HOME/bin' >> /etc/profile.d/mvn.sh
    curl -s -LO http://mirrors.jenkins.io/war-stable/latest/jenkins.war
    mkdir -p /usr/lib/jenkins
    mv jenkins.war /usr/lib/jenkins/jenkins.war
    mkdir -p /data/
    useradd --system -md /data/jenkins jenkins
    echo -e '[Unit]\nDescription=Jenkins Daemon\nAfter=network.target\n\n[Service]\nType=simple\nEnvironment="JENKINS_HOME=/data/jenkins"\nExecStart=/usr/bin/java -jar /usr/lib/jenkins/jenkins.war\nUser=jenkins\n\n[Install]\nWantedBy=multi-user.target' > /etc/systemd/system/jenkins.service
    systemctl daemon-reload
    systemctl start jenkins.service
    systemctl status jenkins.service
    systemctl enable jenkins.service

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
