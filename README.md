create a new repository on the command line
-----------------------------------------------
echo "# jenkins-devops-microservice" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/karthikeyanr4java/jenkins-devops-microservice.git
git push -u origin main


push an existing repository from the command line
---------------------------------------------------------
git remote add origin https://github.com/karthikeyanr4java/jenkins-devops-microservice.git
git branch -M main
git push -u origin main