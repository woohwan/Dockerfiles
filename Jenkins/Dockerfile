FROM jenkins/jenkins:2.387.3-lts-jdk17
RUN jenkins-plugin-cli --verbose --plugins \
    kubernetes:3923.v294a_d4250b_91 \
    workflow-aggregator:596.v8c21c963d92d \
    git:5.0.2 \
    gitlab-plugin:1.7.13 \
    configuration-as-code:1625.v27444588cc3d \
    aws-credentials:191.vcb_f183ce58b_9 \
    credentials:1224.vc23ca_a_9a_2cb_0 \
    sonar:2.15 \
    gradle:2.7 \
    jira:3.9