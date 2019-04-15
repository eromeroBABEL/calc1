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
	stage("constuir") {
	    steps {
		sh "./gradlew build"
	     } 
        }
	stage("docker constuir") {
	    steps {
		sh "docker build -t localhost:5000/calculadora"
	     } 
        }

    }
}
