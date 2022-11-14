pipeline {
    agent any
    
    stages{
    
    
        stage('Pull'){
            steps {
               
                  git branch: 'main',
                  url : 'https://github.com/samar-b/LastHope.git';
            }
        }
        
        
        stage('Build'){
             steps { 
                    script{
                    sh "ansible-playbook ansible/build.yml -i ansible/inventory/host.yml --ask-become-pass"
                    }
                }
             }
             
         
        stage('docker')
        {
             steps {
                    script{
             sh "ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml -e 'ansible_python_interpreter=/usr/bin/python3' "
                          }
                   }
          }         
                   
        stage('push to hub')
        {
             steps {
                    script{
             sh "ansible-playbook ansible/docker-registry.yml -i ansible/inventory/host.yml --ask-become-pass"
                          }
                   }         
        }        
       
}
}
