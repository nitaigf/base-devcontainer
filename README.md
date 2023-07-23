# Inicialização do Docker-Machine no terminal do Mac High-Sierra 10.13

Para iniciar o docker-machine é necessário levantá-lo com o comando abaixo no bash:

```shell
bash --login '/Applications/Docker/Docker Quickstart Terminal.app/Contents/Resources/Scripts/start.sh'

docker-machine start default
```

No POWERSHELL para rodar 'vagrant ssh' é necessário definir o ambiente ssh

$Env:VAGRANT_PREFER_SYSTEM_BIN += 0


No POWERSHELL para entrar no docker após levantado é necessário usar o comando

docker exec -it base-dev sh