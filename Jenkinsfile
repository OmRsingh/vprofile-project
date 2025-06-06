pipeline {
    agent any
    tools {
        jdk "JDK17"
        maven "MAVEN3.9"
    }

    environment {
       SNAP_REPO = 'vprofile-snapshot'
       NEXUS_USER = 'admin'
       NEXUS_PASS = '1219'
       CENTRAL_REPO = 'vprofile-release'
       NEXUSIP = '172.31.94.159'
       NEXUSPORT = '8081'
       NEXUS_GRP_REPO = 'vpro-maven-group'
       NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
        }
    }
}