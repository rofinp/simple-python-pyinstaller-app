node {
  stage('Build') {
    docker.image('python:2-alpine').inside('-p 3000:3000') {
      -v /home/rofinugraha/GitHub/simple-python-pyinstaller-app/sources:/var/jenkins_home/workspace/submission-cicd-pipeline-rofi-nugraha/sources:rw,z
      sh 'python -m py_compile sources/add2vals.py sources/calc.py'
    }
  }

  stage('Test') {
    docker.image('qnib/pytest').inside('-p 3000:3000') {
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
