pipeline
	{
	    agent any
	     stages {
	      
	        stage(' GIT ') {
	            steps {
	                echo 'Pulliing ...';
	                git branch: 'main', url: 'https://github.com/Samehbr21/projectcd.git'          
	            }
	     
	        }
			stage(' install node modules ') {
	            steps {
	            sh ' npm install' 
	            
	            }
	        }
	
	/*
	        stage(' BUILD ') {
	            steps {
	            sh ' npm run build --prod'
	            }
	        } */
	
	        stage(' BUILD ') {
	            steps {
	                script {
	                    sh ' ansible-playbook ansible/build.yml -i ansible/inventory/host.yml '
	                 }
	            }
	        }
			stage('docker') {
  steps {
    script{
      sh "ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml -K -vvv"
    }
  }
}

stage('Docker hub Build and Push') {
	       steps {
	         withDockerRegistry([credentialsId: "docker-hub", url: ""]) {
	           sh 'printenv'
	           sh ' docker build -t samehbrdocker/devops:latest .'
	           sh 'docker push samehbrdocker/devops:latest '
			 }
		   }
}
		 }
	}
