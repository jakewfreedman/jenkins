def flag = false;

pipeline {
  agent any
  stages {
    stage('Checkout'){
      steps {
        echo 'Checking out from repository...'
        git credentialsId: 'shared_credentials', url: 'https://github.com/jakewfreedman/jenkins/tree/kevin'
      }
    }

    stage("Test changeset") {
      when { changeset "**/Jenkinsfile"}
      steps {
        echo("changeset works")
      }
    }

    stage('1 - Run if hello.py changed') {
      when { changeset pattern: "hello.py", comparator: "EQUALS"}
      steps { 
        echo 'hello.py changed!'
        sh 'ls'
	      sh 'python hello.py' 
        script{ flag = true }
      }
    }

    stage('2 Run if hello.py ran') {
      when { expression { flag == true } }
      steps {
        echo 'hello.py ran! Now run goodbye.py'
        sh 'ls'
        sh 'python goodbye.py'
      }
    }
  }
}
