pipeline {
    agent any
    stages {
        stage("compilar") {
            steps {
                sh "./gradlew compileJava"
            }
        }
        stage("Test"){
            steps {
                sh "./gradlew test"
            }
        }
    }
}
