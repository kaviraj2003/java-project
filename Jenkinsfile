pipeline{
    agent any
    parameters{
        string(name:'Branch_name',defaultValue:'dev-main',description:'Enter the new branch name:')
    }
    options{
        discardConcurrentbuilds()
        retry(4)
    }
    stages{
        stage('cleaning the workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Clone the repo'){
            steps{
                script{
                    bat 'git clone https://github.com/kaviraj2003/java-project.git'
                    dir('java-project'){
                        bat 'git checkout main'
                        bat 'git pull origin main'
                    }
                }
            }
        }
        stage('Create the new branch'){
            steps{
                script{
                    dir('java-project'){
                        withCredentials([usernamePassword(credentialsId: 'Kavi-git', passwordVariable: 'GIT_CREDEN_PWD', usernameVariable: 'GIT_CREDEN_USR')]) {
                        bat '"C:/Users/nkj408/AppData/Local/Programs/Git/bin/git.exe" checkout -b ${Branch_name}'
                        bat '"C:/Users/nkj408/AppData/Local/Programs/Git/bin/git.exe" config --global core.compression 9'
                        bat '"C:/Users/nkj408/AppData/Local/Programs/Git/bin/git.exe" push --set-upstream origin ${Branch_name}'
                        }
                    }
                }
            }
        }
    }
}
