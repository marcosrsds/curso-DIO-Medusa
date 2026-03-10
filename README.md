# curso-DIO-Medusa
##Laboratorio com ferramenta MEDUSA

Nesta atividade, foi utilizado o laboratorio DVWA, e a ferramenta MEDUSA.

Inicialmente, verificamos se a máquina "alvo" está acessivel, e após, foi iniciado o ataque *(imagem "conexaoEntreMaquinas")*.

Utilizando NMAP, é realizado uma varredura, para identificar portas abertas, serviços rodando e possiveis vulnerabilidades *(imagem "enumeracao")*.

Após identificar o serviço FTP rodando, foi criado duas listas(simples), uma de usuarios e outra de senhas *(imagem "criandoUsuariosSenhas")*.

Com a ferramenta MEDUSA, é realizado o ataque no FTP, conforme imagem *"ataqueFTPcomMedusa"*, foi encontrado usuario e senha para acesso;
utilizado o comando:
medusa -h (alvo) -U (lista de usuarios) -P (lista de senhas) -M (protocolo a ser atacado) -t (quantidade de "treads" a ser usado)
Com usuario e senha localizados, foi feito um acesso para confirmar que estavam corretos, conforme *imagem "verificandoCredenciais"*; Acesso confirmado no serviço FTP.

ByPass em formulario web de login: conforme mostrado no curso, esta etapa foi um pouco mais complicada, pois o servidor estava retornando código 200 mesmo com credenciais erradas.
Conforme *imagem "atacandoFormularioWEB"* o servidor retornava dois codigos 200 na requisição GET e um terceiro 404 (porem relativo ao favicon), mMesmo quando o login falhava;
Na *imagem "acessando"*, quando o login é bem sucedido, vemos que o servidor retorna quatro códigos 200 nas requisições GET;
Isso pode ter "confundido" a ferramenta MEDUSA que marcava todas as tentativas como [SUCESS].

Após realizar o ByPass, foi hora de descobrir usuarios do sistema, utilizando o "enum4linux" com o parametro "-a" e salvando tudo em um arquivo de texto, conforme *imagem "descobrindoUsuarios"*.

Com os usuarios descobertos, foi o momento de usar MEDUSA para realizar um password spraying, e tentar descobri creddenciais sem chamar atenção, conforme *imagem "ataqueSMBNTcomMEDUSA"*. E após o resultado, testar as credenciais localizadas, conforme *imagem "validandoAcessoSMBNT"*.

# RESUMO
Foi um laboratorio muito bom, e com muitas novidades (ao menos para mim), todos os passos que fiz deram certo, exceto quanto ao formulario WEB, que tive o mesmo problema que a instrutora, todos os testes da ferramenta retornavam [SUCCESS].
Consultando a IA e outros tutoriais, aparentemente o problema é o retorno do servidor com código 200 mesmo quando o login falha, o que provavelmente "confundiu" a MEDUSA. Tentei trocar os parametros para redirecionamento ou mensagem de boas vindas, ou ainda para tentar achar um "Logout" caso desse certo, porem nenhuma das tentativas retornou um resultado diferente.
Fora esse pequeno erro todos os outros passos seguiram conforme o ensinado.
