FROM jenkins/jenkins:latest


USER root

ENV JENKINS_USER admin
ENV JENKINS_PASS Admin@123
ENV JAVA_OPTS "-Xmx2048m -Dhudson.slaves.NodeProvisioner.MARGIN=50 -Dhudson.slaves.NodeProvisioner.MARGIN0=0.85 \
    -Dhudson.slaves.SlaveComputer.allowUnsupportedRemotingVersions=true -Djenkins.install.runSetupWizard=false \
    -Duser.timezone=CET"


RUN apt-get update -y && apt-get install -y openjdk-11-jdk
RUN apt install tini

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /bin/jenkins-plugin-cli --plugin-file /usr/share/jenkins/ref/plugins.txt

COPY default-user.groovy /usr/share/jenkins/ref/init.groovy.d/default-user.groovy
ENTRYPOINT ["/usr/bin/tini", "--", "/usr/local/bin/jenkins.sh"]
