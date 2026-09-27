pipeline {
    agent any

    tools {
        maven 'M3'
    }

    stages {
        stage('Build') {
            steps {
                cleanWs()
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy to WildFly') {
            steps {
                // Копіюємо згенерований WAR у папку автодеплою WildFly
                sh 'cp target/*.war /opt/wildfly/standalone/deployments/'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'target/*.war', allowEmptyArchive: true
        }
    }
}
