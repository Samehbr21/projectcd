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
			stage(' Node modules ') {
	            steps {
	            sh ' npm install' 
	            
	            }
	        }
	
	        stage(' BUILD ') {
	            steps {
	                script {
	                    sh ' ansible-playbook ansible/build.yml -i ansible/inventory/host.yml '
	                 }
	            }
	        }
			stage('DOCKER ') {
  steps {
    script{
      sh "ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml -K -vvv"
    }
  }
}

stage(' DOCKER Registry ') {
	            steps {
					withDockerRegistry(credentialsId: '0b81e4c9-3797-4e6c-b976-4e88cf2c1f15', url: '') {
	                script {
                      sh "ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml -K -vvv"
	                 }
	                 }
	            }
	        }

		 }
	}
