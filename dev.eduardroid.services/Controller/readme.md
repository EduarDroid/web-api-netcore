
#part 1 , to run net core container
#to build Image
docker build --no-cache --pull --rm -f "Dockerfile" -t eduardroid-service:latest "."

#to Run Image, and use port 8080
docker run -d -p 8080:80 --name eduardroid-service eduardroid-service:latest

#try to run it with volumes (do not use)
docker run -d -p 8080:80 -v ~/dev.eduardroid.services:/app/ -w /app/ --name eduardroid-service eduardroid-service:latest

#part 2, run SQL container
#to pull msssql for linux
docker pull mcr.microsoft.com/mssql/server

#Start a mssql-server instance running as the SQL Express edition
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=C._p7,ZF^'gZ.Uk)" -e "MSSQL_PID=Express"  -p 1433:1433 --name SqlServerExpress -v D:\Eduardo\Projects\DBDockerVolume:/var/opt/mssql/data -d mcr.microsoft.com/mssql/server:latest

#part 3, Entity Framework CLI
#install dotnet entity framework tool: -g es para que sea una instalacion global
dotnet tool install dotnet-ef -g
#to create database
dotnet ef database update
#to migrate class to db
dotnet ef migrations add InitialDb