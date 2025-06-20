pipeline {
	agent none

		environment {
			AWS_REGION = 'ap-south-1'
				S3_BUCKET = 'demo-14-static'
		}

	stages {
		stage('Checkout Code') {
			agent { label 'compile' }
			steps {
				git branch: 'main', url: 'https://github.com/prajwal-d14/my-static-site.git'
			}
		}

		stage('Upload to S3') {
			agent { label 'compile' }
			steps {
				sh '''
					aws s3 sync /home/ubuntu/my-static-site s3://$S3_BUCKET/ \
					--region $AWS_REGION
					'''
			}
		}
	}

	post {
		success {
			echo "Website successfully deployed to S3"
		}
		failure {
			echo "Deployment failed"
		}
	}
}
