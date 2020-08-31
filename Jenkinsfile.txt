pipeline{

   agent any
   environment {
   
     MSBuild = "C:\Program Files (x86)\Microsoft Visual Studio\2019\Professional\MSBuild\Current\Bin"
     CONFIG = 'Release'
     PLATFORM = 'x64'
   }

   stages{

      stage ("Build") {

        steps {
           echo 'Building application'

           bat "NuGet.exe restore your_project.sln"

           bat "\"${MSBuild}\" your_project.sln /p:Configuration=${env.CONFIG};Platform=${env.PLATFORM} /maxcpucount:%NUMBER_OF_PROCESSORS% /nodeReuse:false"

         }

       }

       stage ("Unit Test") {
      
          steps {
            echo 'Running Unit tests of application'
          }

        }

    }

}