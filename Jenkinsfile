pipeline {
    agent any
    tools {
        nodejs 'nodejs'
        //jdk 'jdk-17'
    }
    stages {
        stage('Checkout Code') {
            when { 
                anyOf {
                    branch 'main'
                    changeRequest target: 'main'
                }
            }
            steps {
                //checkout scm
                checkout scmGit(extensions: [], userRemoteConfigs: [[credentialsId: 'jenkins-ssh', url: 'git@github.com:hjaijhoussem/project_react_native_jobs.git']])
                // branches: [[name: '*/master']], 
            }
        }
        stage('Install Dependencies') {
            when { 
                anyOf {
                    branch 'main'
                    changeRequest target: 'main'
                }
            }
            steps {
                sh 'rm -rf node_modules'
                sh 'npm install --force'
            }
        }
        
        // stage('Generate apk' ) {
        //     when { 
        //         anyOf {
        //             branch 'main'
        //             changeRequest target: 'main'
        //         }
        //     }
        //     steps {
        //         dir('android') {
        //             sh './gradlew app:assembleRelease --stacktrace'
        //         }
        //     }
        // }
    }
    post {
        failure {
            echo 'Build failed!'
        }
        success {
            echo 'Build successful!'
        }
    }
}
