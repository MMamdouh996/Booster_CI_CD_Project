pipeline {
  agent any

  stages {
    stage('Preparation') {
      steps {
        checkout scm
      }
    }

    stage('Build image') {
      steps {
        sh 'docker build -t my_django_app:v1 .'
      }
    }

    stage('Push image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'my_user', passwordVariable: 'my_pass')]) {
          sh "docker login -u ${my_user} -p ${my_pass}"
          sh "docker tag my_django_app mohamedmamdouhiv/my_django_app:v1"
          sh "docker push mohamedmamdouhiv/my_django_app:v1"
        }
      }
    }

    stage('Deploy') {
      steps {
        sh "docker run -d -p 8000:8000 mohamedmamdouhiv/my_django_app"
      }
    }
  }
}
