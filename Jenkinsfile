pipeline {
    agent any

    environment {
        AC_PAT = credentials('ac-pat')
        PROFILE_ID = env.PROFILE_ID
        ENT_PROFILE_ID = env.ENT_PROFILE_ID
        GIT_REPO = 'https://github.com/hiilhan/appcircle-sample-ios.git'
        BRANCH = 'test/fastlane-plugins-td-eas'
        DIR = 'appcircle-sample-ios'
    }

    stages {
        // stage('Clone Repository') {
        //     steps {
        //         // Clone the specific branch from the repository
        //         // git branch: "${env.BRANCH}", url: "${env.GIT_REPO}"
        //         sh 'git clone -b test/fastlane-plugins-td-eas https://github.com/hiilhan/appcircle-sample-ios.git --single-branch --depth 1'
        //     }
        // }

        // stage('Setup') {
        //   steps {
        //     dir(DIR) {
        //         withCredentials([
	// 		 	file(credentialsId: 'PROVISIONING_PROFILE', variable: 'PROVISIONING_PROFILE'),
	// 		 	file(credentialsId: 'DISTRIBUTION_CERTIFICATE', variable: 'DISTRIBUTION_CERTIFICATE')
	// 		 ]) {
        //             sh 'mkdir certificates'
        //             sh 'cp $PROVISIONING_PROFILE certificates/ac-sample-adhoc.mobileprovision'
        //             sh 'cp $DISTRIBUTION_CERTIFICATE certificates/ac-sample-distribution.p12'
	// 		 }
        //     }
        //   }
        // }

        // stage('Build App') {
        //     steps {
        //         dir(DIR) {
        //             // Call fastlane to build the iOS app
        //             sh 'fastlane ios build_signed'
        //         }
        //     }
        // }
        
        stage('Deploy') {
            steps {
                withCredentials([
			file(credentialsId: 'appcircle-ipa-signed', variable: 'APPCIRCLE_IPA')
		]) {
                    // // TD
                    // greet accessToken: hudson.util.Secret.fromString(AC_PAT),
                    //       profileID: '${PROFILE_ID}',
                    //       appPath: '${APPCIRCLE_IPA}',
                    //       message: 'Hello from Jenkins to TD iOS'
                          
                    // EAS
                    greet accessToken: hudson.util.Secret.fromString(AC_PAT),
                          entProfileId: '${ENT_PROFILE_ID}',
                          appPath: '${APPCIRCLE_IPA}',
                          summary: 'This is a summary.',
                          releaseNote: 'This is a release note.',
                          publishType: '1'
		}
            }
        }
    }

    post {
        always {
            cleanWs() // Clean up workspace
        }
        success {
            echo 'Build and archive completed successfully.'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
