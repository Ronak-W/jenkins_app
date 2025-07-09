pipeline {
    agent any

    environment {
        ANDROID_HOME = "C:\\Android\\Sdk"
        PATH = "C:\\Android\\Sdk\\cmdline-tools\\latest\\bin;C:\\Android\\Sdk\\platform-tools;"
    }

    tools {
        nodejs 'NodeJs'   
        jdk 'JAVA_JDK'    
    }

    stages {
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
                bat 'npx react-native --version'
            }
        }

        stage('Clean Android Build') {
            steps {
                dir('android') {
                    bat 'gradlew.bat clean'
                }
            }
        }

        stage('Check Android Dir') {
            steps {
            dir('android') {
                bat 'dir'
            }
        }
        }

        stage('Check gradlew.bat') {
        steps {
            dir('android') {
                bat 'if exist gradlew.bat (echo Found gradlew.bat) else (echo gradlew.bat not found)'
            }
        }
    }

        stage('Assemble APK') {
            steps {
                dir('android') {
                    bat 'gradlew.bat assembleRelease --info'
                }
            }
        }

        stage('Archive APK') {
            steps {
                archiveArtifacts artifacts: 'android/app/build/outputs/apk/release/app-release.apk', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Android APK build completed successfully.'
        }
        failure {
            echo '❌ Android APK build failed.'
        }
    }
}
