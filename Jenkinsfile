pipeline{
    // agent {label 'sonar'}
    agent any
    stages{
       /*stage('Git Checkout Stage'){
            steps{
                git branch: 'main', url: 'https://github.com/tranju664/Sonar-Qube-war-example.git'
            }
         }*/       
       stage('Build Stage'){
            steps{
                sh 'mvn clean install'
            }
         }
    }
        post {
                success {
                    script {
                        def server = Artifactory.newServer(url: 'http://http://3.110.208.138:8081/artifactory/', credentialsId: 'jfrog')
                        def rtMaven = Artifactory.newMavenBuild()
                        //rtMaven.deployer server: server, releaseRepo: 'libs-release/', snapshotRepo: 'libs-snapshot/'
                        rtMaven.deployer server: server, releaseRepo: 'psm/', snapshotRepo: 'sagar/'
                        rtMaven.tool = 'maven'
                        rtMaven.run(pom: 'pom.xml', goals: 'clean install')
                    }
                }
            }
    }
