pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
              script {
                def repo = checkout scm
                commit7 = repo.GIT_COMMIT.take(7)
                commit = repo.GIT_COMMIT
                branch = repo.GIT_BRANCH
                withCredentials([gitUsernamePassword(credentialsId: 'minegit', gitToolName: 'git-tool')]) {
                sh """cd test
                      git pull
                      if [ $branch != 'develop' ]; then
                        git checkout release/1.0.0
                        ls -ltr
                        git merge origin/develop
                        git push origin release/1.0.0
                      fi
                    """
                 }
                }    
            }
        }
    }
}

