pipeline {

    agent any

    environment {
        GITLAB=credentials('usr-psw-gitlab')
        GITLAB_URL="15.152.61.141:8929/root/MyApplication"

    }

    stages {
        stage("Calculate & Set version") {
            when {
                branch "main"
            }
            steps {
                script {
                    majorMinor="1.0"

                    previousTag = sh(script: "git describe --tags --abbrev=0 | grep -E '^$majorMinor' || true", returnStdout: true).trim()

                    if (!previousTag) {
                        patch = "0"
                    } else {
                        patch = (previousTag.tokenize(".")[2].toInteger() + 1).toString()
                    }
                    env.VERSION = majorMinor + "." + patch

                }
            }
        }  
    }
}
