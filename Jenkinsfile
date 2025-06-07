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
       NEXUS_REPOSITORY = 'vprofile-release'
       NEXUSIP = '172.31.94.159'
       NEXUSPORT = '8081'
       NEXUS_REPOGRP_ID = 'vpro-maven-group'
       NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo "Now Archiving."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Test'){
            steps{
                sh 'mvn -s settings.xml test'
            }
        }

        stage('Checkstyle Analysis'){
            steps{
                sh 'mvn -s settings.xml checkstyle:checkstyle'
            }
        }
    }
}