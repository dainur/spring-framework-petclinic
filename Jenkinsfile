pipeline {
    agent any

    tools {
        maven 'M3'
    }

    stages {
        stage('Build') {
            steps {
                // 1. Очищаємо робочий простір
                cleanWs()
                
                // 2. Клонуємо код репозиторію (де знаходиться pom.xml)
                git branch: 'main', url: 'https://github.com/dainur/spring-framework-petclinic.git'

                // 3. Запускаємо збірку Maven
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy to WildFly') {
            steps {
                // Копіюємо згенерований WAR у папку deployments WildFly
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
