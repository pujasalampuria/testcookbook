node {
        // Clean workspace before doing anything
    deleteDir()
    try {
        stage ('Clone') {
                checkout scm
        }
        stage ('SCA') {
            sh "cd /var/lib/jenkins/workspace/testcookbook/cookbooks && foodcritic ."
        }
        stage ('Unit Test') {
            sh "cd /var/lib/jenkins/workspace/testcookbook/cookbooks && chef exec rspec spec/"
        }
        stage ('Integration Test') {
            sh "cd /var/lib/jenkins/workspace/testcookbook/cookbooks && kitchen verify"
        }
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
