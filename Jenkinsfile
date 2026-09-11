pipeline{
    agent any
    environment{
        SONAR_HOME= tool 'SonarQube-Scanner'
    }
    stages{
        stage('Code'){
            steps{
                echo "This is Chandra Sharma at stage of 'Code' "
            }
        }
        stage('Code Clone from GitHub'){
            steps{
                echo "This is Chandra Sharma at stage of Code Clone from GitHub "
                git url: "https://github.com/Chandrashar/wanderlust.git", branch: "devops" 
            }
        }
        stage('SonarQube Quality Analysis'){
            steps{
                echo "This is Chandra Sharma at stage of SonarQube Scanning.. "
                withSonarQubeEnv("SonarQube-Server"){
                    sh "$SONAR_HOME/bin/sonar-scanner -Dsonar.projectName=wanderlust -Dsonar.projectKey=wanderlust"
                }
            }
        }
        stage('OWASP Dependency Check'){
            steps{
                echo "This is Owasp Dependency Check Skipping due to heavy build download.. "
              //  dependencyCheck additionalArguments: '--scan ./', odcInstallation: 'dc'
              // dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        stage('Sonar Quality Gate Scan'){
            steps{
                 echo "This is Sonar Quality Gate Scan Skipping for now....since above.. "
              //  timeout(time: 2, unit: "MINUTES")
             //   waitforQualityGate abortPipeline: false
            }
        }
        stage('Trivy File System Scan'){
            steps{
                echo "This is Trivy file System scanning "
                sh "trivy fs --format table -o trivy-fs-report.html ."
            }
        }
        
        stage("Deploy using Docker compose"){
            steps{
                sh "docker compose up -d"
            }
        }

    }
}
