pipeline {
  agent any
  stages {
    stage ('Testing') {
      steps {
          git branch: 'stg', credentialsId: 'for-git', url: 'https://github.com/AAT-technologies/cartservice.git'
          sh ''' sudo docker login -u delalixx -p dckr_pat_-dfSKHYHBVZNLTVX1R5sxmNGJwo
          '''
          sh ''' sudo docker system prune -af
          '''
         
         sh '''    cd app-cart/cartservice/src
                   ls
                   sudo docker build -t delalixx/cartservice .
                   sudo docker push delalixx/cartservice
                   '''
         sh ''' sudo docker system prune -af
                  '''
         
      }
    }
     stage ('Create Deploy to Yaml file') {
       steps {
         sh ''' ls
         '''
            withCredentials([aws(credentialsId: 'aws-credentials', region: 'ca-central-1')]) {
           sh 'kubectl version --client --output=yaml'
           sh '''
                 aws eks --region ca-central-1 update-kubeconfig --name boot-staging
                 kubectl config current-context
                 kubectl config use-context arn:aws:eks:ca-central-1:487585538889:cluster/boot-staging 
                 kubectl apply -f cluster.yaml
                 kubectl get node
                 kubectl get service
                 '''
           }
        }
     }
  }
}
