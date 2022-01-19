# TRABALHO REALIZADO NA SEMANA #11

## 3: Lab Tasks

### Task 1: Becoming a Certificate Authority (CA)


>Before starting, we had to have the config file in the folder we wanted. To that we used the command:
>
>>cp /usr/lib/ssl/openssl.cnf myCA_openssl.cnf
>
>In this task we had to create a Certificate Authority (CA), which is a trusted authority that creates and signs digital certificates.
>
>By being a CA we can atest that someone (or website) is the owner of a said public key.
>
>To create a cerficate of our CA we had to use the following command:
>
>>openssl req -x509 -newkey rsa:4096 -sha256 -days 3650 -keyout ca.key -out ca.crt -subj "/CN=www.modelCA.com/O=Model CA LTD./C=US" -passout pass:dees
>
>the file "ca.key" contains the private key of the CA while "ca.ct" has the public key.
>
>This is the content of the "ca.crt":
>
>>![week11_0](https://cdn.discordapp.com/attachments/903555414715670578/933492135934705734/unknown.png)
>>![week11_1](https://cdn.discordapp.com/attachments/903555414715670578/933492236631564298/unknown.png)
>
>>**What part of the certificate indicates this is a CA’s certificate?**
>>
>>In the section "basic constraints" there is an attribute "certificate aithority" is set to "Yes". This shows that it is the certificate for the CA.
>
>>**What part of the certificate indicates this is a self-signed certificate?**
>>
>>This is a self-signed certificate because in the file we can see that the subject and the issuer are the same. On top of that in the command we ran was include the flag "-x509" (used to create self-signed certificates).
>>
>
>>**In the RSA algorithm, we have a public exponent e, a private exponent d, a modulus n, and two secret numbers p and q, such that n = pq. Please identify the values for these elements in your certificate and key files.**
>>
>>

### Task 2: Generating a Certificate Request for Your Web Server

>On this task, the objective was to create a "Certificate Signing Request", CSR. This will be generate by the CA that we created in the task 1.
>
>To do that, we used the following command:
>
>>openssl req -newkey rsa:2048 -sha256 -keyout server.key -out server.csr -subj "/CN=www.bank32.com/O=Bank32 Inc./C=US" -passout pass:dees
>>
>After that, is sugested to do some alterations to the last command, so the certificate allows alternative names to the website.
>
>>openssl req -newkey rsa:2048 -sha256 -keyout server.key -out server.csr -subj "/CN=www.bank32.com/O=Bank32 Inc./C=US" -passout pass:dees -addext "subjectAltName = DNS:www.bank32.com, DNS:www.bank32A.com, DNS:www.bank32B.com"
>
>We an see this information by using the following commands:
>
>>openssl req -in server.csr -text -noout
>
>>penssl rsa -in server.key -text -noout
>
>With the correct server name ofcourse and obtain the following results:
>
>>![week11_4](https://cdn.discordapp.com/attachments/903555414715670578/933495048753004605/unknown.png)
>
>And..
>
>>![week11_5](https://cdn.discordapp.com/attachments/903555414715670578/933495883952181308/unknown.png)
>
>>![week11_6](https://cdn.discordapp.com/attachments/903555414715670578/933495977761996871/unknown.png)

### Task 3: Generating a Certificate for your server

>As instructed we used the following command:
>
>>openssl ca -config myCA_openssl.cnf -policy policy_anything -md sha256 -days 3650 -in server.csr -out server.crt -batch -cert ca.crt -keyfile ca.key
>
>This command allows us to convert the "server.csr" in a self-signed certificate, "server.crt".
>
>>![week11_7](https://cdn.discordapp.com/attachments/903555414715670578/933497905422155786/unknown.png)
>
>>![week11_8](https://cdn.discordapp.com/attachments/903555414715670578/933498273354899466/unknown.png)
