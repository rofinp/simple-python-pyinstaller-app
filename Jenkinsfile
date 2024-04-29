node {
  stage('Build') {
    docker.image('python:2-alpine').inside {
      sh 'python -m py_compile ./home/GitHub/simple-python-pyinstaller-app/sources/add2vals.py ./home/GitHub/simple-python-pyinstaller-app/sources/calc.py'
    }
  }

  stage('Test') {
    docker.image('qnib/pytest').inside {
      sh 'py.test --verbose --junit-xml test-reports/results.xml ./home/GitHub/simple-python-pyinstaller-app/sources/test_calc.py'
    }
    post {
      always {
        junit 'test-reports/results.xml'
      }
    }
  }
}
