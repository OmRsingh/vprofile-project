pipeline {
    agent any
/*    tools {
        jdk "JDK17"
        maven "MAVEN3.9"
    } */

    environment {
       NEXUS_VERSION = 'nexus3'
       NEXUS_PROTOCOL = "http"
       NEXUS_USER = 'admin'
       NEXUS_PASS = '1219'
       NEXUS_REPOSITORY = 'vprofile-release'
       NEXUSIP = '172.31.94.159'
       NEXUSPORT = '8081'
       NEXUS_REPOGRP_ID = 'vpro-maven-group'
       NEXUS_CREDENTIAL_ID = 'nexuslogin'
       SONARSERVER = 'sonarserver'
       SONARSCANNER = 'sonarscanner'
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

        stage('Code Analysis using Checkstyle'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
            post {
                success {
                    echo 'Generated Analysis Result.'
                }
            }
        }

        stage ('Code Analysis with SonarQube') {
            environment {
                scannerHome = tool "${SONARSCANNER}"
            }

            steps {
                withSonarQubeEnv("${SONARSERVER}"){
                    sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                    -Dsonar.projectName=vprofile-repo \
                    -Dsonar.projectVersion=1.0 \
                    -Dsonar.sources=src/ \
                    -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                    -Dsonar.junit.reportsPath=target/surefire-reports/ \
                    -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                    -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
                }
            }
        }
    }
}