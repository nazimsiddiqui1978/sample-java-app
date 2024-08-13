pipeline {
    agent any
 
    tools {
        maven 'Maven' // This should match the name of your Maven installation in Jenkins Global Tool Configuration
    }
 
    environment {
        // Use the credentials ID that you have set up in Jenkins for Nexus
        NEXUS_CREDENTIALS = credentials('nexus-credentials') 
        // Nexus repository URL where the artifact will be deployed
        MAVEN_REPO_URL = 'http://3.6.4.139:8081/repository/Maven-Hosted-Nazim/' 
    }
 
    stages {
        stage('Build') {
            steps {
                // This will clean the project and build the package
                sh 'mvn install'
            }
        }
 
        stage('Deploy to Nexus') {
            steps {
                withCredentials([usernamePassword(credentialsId: env.NEXUS_CREDENTIALS, passwordVariable: 'NEXUS_PASS', usernameVariable: 'NEXUS_USER')]) {
                    sh """
                       mvn deploy:deploy-file \
                           -Durl=${env.MAVEN_REPO_URL} \
                           -DrepositoryId=nexus \
                           -Dfile=target/your-artifact.jar \
                           -DgroupId=com.yourcompany \
                           -DartifactId=your-artifact \
                           -Dversion=1.0.0 \
                           -Dpackaging=jar \
                           -DgeneratePom=true \
                           -Dusername=$NEXUS_USER \
                           -Dpassword=$NEXUS_PASS
                    """
                }
            }
        }
    }
}

has context menu
