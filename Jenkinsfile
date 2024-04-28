node {
  stage('Build') {
    docker.image('python:2-alpine').inside {
      -v '/home/myuser/GitHub/simple-python-pyinstaller-app/sources:/var/jenkins_home/workspace/submission-cicd-pipeline-rofi-nugraha/sources:rw,z'
      sh 'python -m py_compile sources/add2vals.py sources/calc.py'
    }
  }

  stage('Test') {
    docker.image('qnib/pytest').inside {
      sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
    }
    post {
      always {
        junit 'test-reports/results.xml'
      }
    }
  }
}
