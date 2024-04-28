node {
  stage('Build') {
    docker.image('python:2-alpine').inside('-p 1000:1000') {
      sh 'python -m py_compile sources/add2vals.py sources/calc.py'
    }
  }

  stage('Test') {
    docker.image('qnib/pytest').inside('-p 1000:1000') {
      sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
      satash(name: 'compiled-results', includes: 'sources/*.py*')
    }
    post {
      always {
        junit 'test-reports/results.xml'
      }
    }
  }
}
