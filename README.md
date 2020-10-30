## Dependências
Para que seja possível consumir o serviço do google: `https://www.google.com/recaptcha/api/siteverify` é necessário uma aplicação backend que seja um cliente dessa API, pelo frontend, com AJAX, acontece erro no CORS.
No caso é utilizado essa aplicação `https://github.com/andersoncvlh/google-recaptcha-client`

## Executar como servidor
1. Intalar lib http-server através do npm: `npm i --global http-server`
2. Executar o servidor: `http-server ./ --port 8181`


## Proxy 
Aqui está um exemplo simples de uma configuração de proxy para que o front se comunique com o backend em um exemplo localhost. Utilizando nginx:
```
//[...]
server {
	//listen       8?....[...];

	// fazendo com que o front-end seja acessado por 127.0.0.1
	location / {
	    proxy_pass http://127.0.0.1:8181;
	    proxy_set_header X-Real-IP  $remote_addr;
	    proxy_set_header X-Forwarded-For $remote_addr;
	    proxy_set_header Host $host;
	}
	// fazendo com que o front-end seja acessado por 127.0.0.1/recaptcha
	location /recaptcha {
	    proxy_pass http://127.0.0.1:8080;
	    proxy_set_header X-Real-IP  $remote_addr;
	    proxy_set_header X-Forwarded-For $remote_addr;
	    proxy_set_header Host $host;
	}

	//[...]
}
```

## Referências
### V2
- Site: https://developers.google.com/recaptcha/docs/display
- Servidor: https://developers.google.com/recaptcha/docs/verify
### V3
- Site: https://developers.google.com/recaptcha/docs/v3
- Servidor: https://developers.google.com/recaptcha/docs/verify