pipeline {
    agent any
    tools {
        maven 'maven3'
        jdk 'java17'
    }
    stages {
        stage('download-code') { 
            steps {
                echo "Downloading code from Git"
                git branch: 'main', url: 'https://github.com/saumil1201/maven-jenkins4.git'
            }
        }
        stage('Build') { 
            steps {
                echo "Building the project"
                sh 'mvn clean package'
            }
        }
        stage('Archive-Artifacts') { 
            steps {
                echo "Archiving artifacts"
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('Trigger-Deploy-job') { 
            steps {
                echo "Triggering deploy job"
                build wait: false, job: 'pipeline-deploy'
            }
        }
    }
}
