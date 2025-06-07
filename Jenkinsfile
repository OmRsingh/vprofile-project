pipeline {
    agent any
/*    tools {
        jdk "JDK17"
        maven "MAVEN3.9"
    } */

    environment {
       NEXUS_PROTOCOL = "nexus3"
       NEXUS_USER = 'admin'
       NEXUS_PASS = '1219'
       NEXUS_REPOSITORY = 'vprofile-release'
       NEXUSIP = '172.31.94.159'
       NEXUSPORT = '8081'
       NEXUS_REPOGRP_ID = 'vpro-maven-group'
       NEXUS_CREDENTIAL_ID = 'nexuslogin'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install -DskipTests install'
            }
            post {
                success {
                    echo "Now Archiving."
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('UNIT TEST'){
            steps{
                sh 'mvn test'
            }
        }

        stage('Checkstyle Analysis'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
    }
}