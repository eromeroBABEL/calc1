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
	stage("construir") {
	    steps {
		sh "./gradlew build"
	     } 
        }
	stage("docker constuir") {
	    steps {
		sh "docker build -t localhost:5000/calculadora"
	     } 
        }
	
	stage("docker push") {
	    steps {
		sh "docker push localhost:5000/calculadora"
	     } 
        }
	
	stage("borrar contenedor") {
	    steps {
		sh "docker rm calculadora"
	     } 
        }

	stage("docker crear contenedor") {
	    steps {
		sh "docker run -d -p 9090:8090 --name calculadora  localhost:5000/calculadora"
	     } 
        }
    }
}
