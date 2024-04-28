node {
  stage('Build') {
    docker {
      image 'python:2-alpine'
    }
    sh 'python -m py_compile sources/add2vals.py source/calc.py'
  }

  stage('Test') {
    docker {
      image 'qnib/pytest'
    }
    sh 'py.test --verbose --junit-xml test-reports/result.xml sources/test_calc.py'
    post {
      always {
        junit 'test-reports/results.xml'
      }
    }
  }
}
