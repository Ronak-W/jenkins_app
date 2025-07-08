pipeline {
    agent any

    environment {
        // SDK and Java Paths (hardcoded)
        ANDROID_HOME = 'C:\\Android\\Sdk'
        JAVA_HOME = 'C:\\Program Files\\Java\\jdk-17.0.12'
        PATH = "C:\\Android\\Sdk\\platform-tools;" +
               "C:\\Android\\Sdk\\cmdline-tools\\latest\\bin;" +
               "C:\\Android\\Sdk\\build-tools\\34.0.0;" +
               "C:\\Program Files\\Java\\jdk-17.0.12\\bin;" +
               "${env.PATH}"
    }

    stages {
        stage('Environment Check') {
            steps {
                bat 'echo === SDK LOCATION: %ANDROID_HOME% ==='
                bat 'adb --version'
                bat 'sdkmanager --list'
                bat 'java -version'
            }
        }

        stage('Clean Build') {
            steps {
                bat './gradlew clean'
            }
        }

        stage('Assemble APK') {
            steps {
                bat './gradlew assembleDebug'
            }
        }

        stage('Post Build') {
            steps {
                bat 'dir app\\build\\outputs\\apk\\debug'
            }
        }
    }

    post {
        failure {
            echo '❌ Build failed!'
        }
        success {
            echo '✅ Build completed successfully!'
        }
    }
}
