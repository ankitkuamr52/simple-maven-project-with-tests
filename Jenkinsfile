
pipeline {
    agent any



parameters {
        string(name: 'branch', defaultValue: 'master', description: 'please enter branch to execute')
        choice(name: 'test', choices: ['yes', 'no'], description: 'do you want to test')
    }

    tools {
       
        maven "m3"
    }

    stages {
        stage('Build') {
            steps {
                
                git 'https://github.com/ankitkuamr52/simple-maven-project-with-tests'

                // Run Maven on a Unix agent.
                 sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
