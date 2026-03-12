#guia aula:

#usando o gpg (gnuPG):
##====== criptografia simetrica ======
###passo1 um criar um arquivo .txt com a mensagem a ser cifrada

###passo2 cifrar o arquivo: estando no terminal na pasta onde criou o arquivo
>gpg --symmetric <nome arquivo> 
-adicione uma senha: chave privada que será necessária para descriptografar
-será criado um arquivo com a extensao .gpg (arquivo cifrado) --> abra o arquivo em modo texto para ver seu conteúdo

###passo3 decifrar o arquivo: estando no terminal na pasta onde criou o arquivo
>gpg --decrypt <arquivo cifrado .gpg>
isso mostrará em tela a mensagem cifrada.
Opcionalmente: você pode também redirecionar a saída para um arquivo
>gpg --decrypt <arquivo cifrado .gpg> > <novo arquivo com a mensagem decifrada .txt>

##=====criptografia assimetrica =====
###passo1:(no user A) criar chaves (deve informar nome do usuario e email): Padrão RSA
>gpg --gen-key
(solicita ao fim uma senha: chave privada)
para mais detalhes como escolha do algoritmo, quando expira e tamanho da chave
>gpg --full-gen-key

###passo2:(no user A) exportar a chave pública para enviar aos interessados a te enviar mensagens cifradas
>gpg --export -a <userA> > <arquivo.asc>
o arquivo com a chave publica .asc será criado

###passo3:(no user B) importando a chave públiica de outra pessoa com o arquivo .asc
>gpg --import <arquivo_com_pubkey_userA.asc>

###passo4:(no user B) encriptar: -e
deve-se especificar qual usuário (chave publica) vamos utilizar -r (pode ser mais de um) e o arquivo
>gpg -e -r <userA> <arquivo_sem_criptografia>
vai encriptar usando a chave pública de <userA> e será decriptado com a chave privada de <userA> (um password)

###passo5:(no user A) decriptar:
>gpg -d <arquivo.gpg>
para redirecionar:
>gpg -d <arquivo.gpg> > <novo_arquivo.txt>

###outros:
####listar as chaves (o aquivo onde as chaves são criadas também aparece)
>gpg -k

--local das chaves no ubuntu (pasta pessoal): /home/<user>/.gnupg/pubring.kbx 
--para excluir as chaves basta remover esse arquivo:
>rm -rf ~/.gnupg/pubring.kbx# segInfo2026
