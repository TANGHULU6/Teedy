pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Generate Javadoc') {
            steps {
                // 生成 Javadoc 文档
                sh 'mvn javadoc:javadoc'
            }
        }
        stage('pmd') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
        stage('Test report') {
            steps {
                // 运行测试并生成 Surefire 报告
                sh 'mvn test -Dmaven.test.failure.ignore=true'
            }
        }
        
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            archiveArtifacts artifacts: '**/target/surefire-reports/*.xml', fingerprint: true
        }
    }
}
