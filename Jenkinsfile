pipeline {
    agent any

    // Define tools to be installed
    tools {
        // Install Node.js tool with a specific version
        nodejs 'node:latest'
    }

    environment {
        // JWT_SECRET = 'TestSecreatKey'
        MONGO_URI = 'mongodb+srv://yadiraelham0:WKamEQsZ5XPm4q0V@cluster0.ke7jv.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0'
    }
    stages {
        stage('Checkout') {
      steps {
        // Check out the repository from GitHub
        git branch: 'main', url: 'https://github.com/mooon-dev/chat-app-mern.git'
      }
        }

        stage('Install frontend Dependencies') {
      steps {
        // Change to the client directory and install dependencies
        dir('frontend') {
          sh 'npm install'
        }
      }
        }

        stage('Build frontend') {
      steps {
        // Change to the client directory and run the build command
        dir('frontend') {
          sh 'CI=false npm run build'
        }
      }
        }

        stage('Install Backend Dependencies') {
      steps {
        // Change to the backend directory and install dependencies
        dir('backend') {
          sh 'npm install'
          sh 'export MONGODB_URI=$MONGODB_URI'
        //   sh 'export TOKEN_KEY=$TOKEN_KEY'
        }
      }
        }
    }

    post {
        success {
      echo 'Pipeline completed successfully!'
        }
        failure {
      echo 'Pipeline failed.'
        }
    }
}
