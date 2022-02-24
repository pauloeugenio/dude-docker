# Como Instalar o The Dude no Docker
<img src="http://pauloeugenio.com.br/img/theDude.png">    <img src="https://cdn-icons-png.flaticon.com/512/37/37770.png" height="150"><img src="https://raw.githubusercontent.com/docker/compose/v2/logo.png">

Já imaginou instalar o The dude no Docker ou Docker-compose ? e poder monitorar seus ativos de rede ?</br>
Vamos lá!!!

<h1>Instalando o The Dude</h1>
Antes de iniciarmos, gostaria de lembrar que é necessario <a target="_blank" href="https://github.com/pauloeugenio/docker">instalar o docker e docker-compose</a> para poder utilizar o the dude como um container no docker. a documentação da imagem do container The dude pode ser acessada <a target="_blank" href="https://hub.docker.com/r/alexanderfefelov/dude">aqui</a>.</br><br/>

Atenção! Este é um contêiner servidor, e não um cliente! Para acessar a interface grafica para configurar seus dispositivos, será nescessario utilizar um cliente Dude. A última versão do servidor The Dude para Windows é a 4.0beta3 lançada em 2011, e pode ser baixada <a target="blank" href="http://www.pauloeugenio.com.br/docs/dude-install-4.0beta3.zip">aqui (Site)</a> ou nesse outro <a href="https://drive.google.com/file/d/1BUhiSW_vUd9BcFgOVsShawxqHIG7pX25/view?usp=sharing">link (Drive)</a>. Sem mais enrrolação, vamos instalar o container dude.

<h2>Criando o container atraves do prompt de comando</h2>
Você pode criar o container de duas maneiras:
<h3>Maneira 1:</h3>
Maneira recomendada pelo desenvolvedor da imagem.
<pre>
<code>
docker run \
  --name dude \
  --detach \
  --restart unless-stopped \
  --volume /etc/localtime:/etc/localtime:ro --volume /etc/timezone:/etc/timezone:ro \
  --volume dude:/dude/data \
  --publish 80:80 \
  --publish 443:443 \
  --publish 514:514/udp \
  --publish 2210:2210 \
  --publish 2211:2211 \
  --health-cmd /healthcheck.sh --health-start-period 3s --health-interval 1m --health-timeout 1s --health-retries 3 \
  --log-opt max-size=10m --log-opt max-file=5 \
  alexanderfefelov/dude
</code>
</pre>
<h3>Maneira 2:</h3>
Maneira mais simplificada:
<pre>
<code>
docker run -d --name duce --restart always --network default -p 9000:80 -p 444:443 -p 514:514 -p 2210:2210 -p 2211:2211 -v /etc/localtime:/etc/localtime:ro -v /etc/timezone:/etc/timezone:ro alexanderfefelov/dude
</code>
</pre>

Ao realizar qualquer uma das maneiras acima, você verá o seu Dude funcionando perfeitamente, isso mesmo! simples assim! ...para testar basta conectar ao servidor utilizando um cliente Dude, o mesmo citado acima na versão para windows, basta colocar o ip da maquina que está rodando o docker e voa-lá você terá acesso a sua interface do The Dude.</br></br>

<h2>Instalar o The Dude com Docker-compose(Versão 2.0 acima)</h2>
Se você quer deixar o docker-compose configurado para realizar a instalação/manutenção do seu the dude de maneira ainda mais simples, basta seguir os passos a seguir.

<h3>Primeiro Passo:</h3>
Baixe o repositorio dude-docker em seu linux, para isso utilize o comando abaixo:
<pre>
<code>
git clone https://github.com/pauloeugenio/dude-docker
</code>
</pre>
Feito isso, acesse o diretorio que você acabou de baixar e torne o arquivo "services" executavel com o seguinte comando abaixo:
<pre>
<code>
sudo chmod +x services
</code>
</pre>
Na sequencia é só realizar a instalação do seu dude com o seguinte comando:
<pre>
<code>
sudo ./services start
</code>
</pre>
Feito isso, você terá o seu The dude rodando.

<h2>Atenção!!!</h2>
Se você estiver utilizando uma versão antiga do docker-compose(inferior a 2.0) você deverá utilizar o seguinte passo:<br>

Baixe o repositorio dude-docker em seu linux, para isso utilize o comando abaixo:
<pre>
<code>
git clone https://github.com/pauloeugenio/dude-docker
</code>
</pre>
Feito isso, acesse o diretorio que você acabou de baixar e torne o arquivo "services-old" executavel com o seguinte comando abaixo:
<pre>
<code>
sudo chmod +x services-old
</code>
</pre>
Na sequencia é só realizar a instalação do seu dude com o seguinte comando:
<pre>
<code>
sudo ./services-old start
</code>
</pre>

