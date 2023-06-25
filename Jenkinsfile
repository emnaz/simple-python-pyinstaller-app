node {
    docker.image('python:2-alpine').inside {
        catchError {
            stage('Checkout') {
                checkout scm
            }
            stage('Build') {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
	        }
        }
    }
	
	stage('Test') {
		agent {
            docker {
				image 'qnib/pytest'
            }
        }
		sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
        post {
			always {
				junit 'test-reports/results.xml'
            }
        }
	}
}