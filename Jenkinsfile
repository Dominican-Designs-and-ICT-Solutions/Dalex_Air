pipeline {
  agent any

  environment {
    DJANGO_ENV = 'production'
    PYTHON_VERSION = '3.9'
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/SomkeneA/Dalex_Air.git'
      }
    }

    stage('Setup') {
      steps {
        sh 'python3 -m venv venv'
        sh 'source venv/bin/activate'
        sh 'pip install -r requirements.txt'
      }
    }

    stage('Lint') {
      steps {
        sh 'python manage.py lint'
      }
    }

    stage('Test') {
      steps {
        sh 'python manage.py test'
      }
    }

    stage('Build') {
      steps {
        sh 'python manage.py collectstatic --noinput'
        sh 'python manage.py migrate'
      }
    }

    stage('Deploy') {
      steps {
        // Add deployment steps here, such as pushing the code to a production server or using a deployment tool
      }
    }
  }

  post {
    always {
      sh 'deactivate'
    }
    success {
      echo 'Pipeline executed successfully!'
    }
    failure {
      echo 'Pipeline failed!'
    }
  }
}
