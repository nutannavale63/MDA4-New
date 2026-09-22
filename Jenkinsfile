    pipeline {
        agent any
        
        stages {
            stage "Pull stage" {
                steps {
                    bat 'git clone https://github.com/Ishikapbhatt/MDA4.git'
                }
            }

            stage "Infrastructure" {
                steps {
                    bat 'cd Terraform/eks-modules'
                    bat 'terraform init'
                    bat 'terraform apply -auto-approve'
                }
            }

            stage "Build" {
                steps {
                    bat 'cd docker/student-app/database'
                    bat 'docker build -t studentapp-db .'
                    bat 'cd ../backend'
                    bat 'docker build -t studentapp-be .'
                    bat 'cd ../frontend'
                    bat 'docker build -t studentapp-fe .'
                }
            }

            stage "push stage" {
                steps {
                    bat 'docker push studentapp-db'
                    bat 'docker push studentapp-be'
                    bat 'docker push studentapp-fe'
                }
            }
            
            stage "Deploy" {
                steps {
                    bat 'cd Kubernetes/student-app/'
                    bat 'kubectl apply -f KUbernetes/student-app/'
                }
            }
        }
    }