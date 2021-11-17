# TRABALHO REALIZADO NA SEMANA #4

### Task 1: Manipulating Environment Variables

- O printenv lista todos os ambientes de variáveis do sistema, para procurar um ambiente especifico, podemos fazer, por exemplo, escrever o comando printenv PWD"  e irá imprimir apenas /home/seed

### Task 2: Passing Environment Variables from Parent Process to Child Process

### Task 3: Environment Variables and execve()

### Task 4: Environment Variables and system()

### Task 5: Environment Variable and Set-UID Programs

### Task 6: The PATH Environment Variable and Set-UID Programs



# CTF

Reconhecimento
O primeiro passo foi aceder a página do servidor wordpress e fazer a análise da programação do site (com as ferramentas para developers do web browser). Ápos isso, no html da página, procuramos por informações que pudessem ajudar na identificação de uma vulnerabilidade.
A informações coletadas foram: 

    versão do wordpress 5.8.2;
    plugin instalado woocommerce 5.7.1;
    Tema do storefront (... gutenber-blocks.css versão 3.9,1);
    dentre outras;

Uma coisa que ajudou foi procurar por wp-content e wp-content/plugins na área de pesquisa do documento html (uma vez que já sabiamos que era um seridor wordpress).

As possíveis contas de usuários também foram verificadas utilizando o link: http://ctf-fsi.fe.up.pt:5001/wp-json/wp/v2/users/1.
Onde indicava que o admin possui o nome "admin" e o id associado a conta é 1 (o que nós ajudoou mais tarde).

Com essas informações procuramos em diferentes sites sobre cves associados as mesmas. Com algum trabalho encontramos o CVE-2021-34646, que funcionava com as informações que tinhamos. (e com isso obtivemos a flag do desafio 1).

Porcuramos por um exploit já feito para a CVE-2021-34646, encontramos no site "https://www.exploit-db.com/exploits/50299"; a utilização da mesma foi simples e funcional.

Para corrermos o exploit foi simpleste utilizar o comando: python 50299.py website_pretendido id_da_conta (como mencionado no própio exploit). No nosso caso foi: python 50299.py ctf http://ctf-fsi.fe.up.pt:5001/ 1
Id 1 pois representava o admin (segundo o que verficamos). O exploit deu-nos alguns links em que um deles redirecionava para a página do admin já autenticada.

Com isso foi simplesmente abrir a página onde se encrontrava a flag do desafio 2.