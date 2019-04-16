def control = 0
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
		sh "sudo docker build -t localhost:5000/calculadora ."
	     } 
        }
	
	stage("docker push") {
	    steps {
		sh "sudo docker push localhost:5000/calculadora"
	     } 
        }
	
	stage("borrar contenedor") {
            when {
                expression { sh script: '''if [ -z $(sudo docker ps -f name=calculadora -q) ]; then true; else false; fi''', returnStatus: true
                  }
              }
	    steps {
		sh "sudo docker stop calculadora"
		sh "sudo docker rm calculadora"
	     } 
        }

	stage("docker crear contenedor") {
	    steps {
		sh "sudo docker run -d -p 9090:8090 --name calculadora  localhost:5000/calculadora"
	     } 
        }
	
	stage("comprobar funcionamiento") {
	    steps {
                script { 
                control = expression { sh script: '''if [ -z $(./lanzar_test.sh) ]; then true; else false; fi''', returnStatus: true
                }
              echo "${control}"

	     } 
	     } 
        }
	stage("produccion") {
	    steps {
		sh "sudo ansible-playbook playbook.yml"
	     } 
        }
    }
}
