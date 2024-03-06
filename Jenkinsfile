pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }

    environment {
        SNAP_REPO = 'project-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'test1234'
        RELEASE_REPO = 'project-release'
        CENTRAL_REPO = 'project-maven-central'
        NEXUSIP = '172.31.44.234'
        NEXUSPORT = '8081'
        NEXUS_GRP_REPO = 'project-maven-group'
        NEXUS_LOGIN = 'nexuslogin'

    }

    stages {
        stage ('Build') {
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo "Now Archiving"
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage ('Test') {
            steps {
                sh 'mvn -s settings.xml test'
            }
        }

    }
}