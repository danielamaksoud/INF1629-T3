# Instalando Docket toolbox no Windows 7 #
Procedimento que foi preciso fazer para instalar docker toolbox no windows 7 (pode variar de pessoa a pessoa).

## Compatibilidade ##
Ferramenta de detectar se você rodar windows virtual pc (Hardware-Assisted Virtualization):  
https://www.microsoft.com/en-us/download/details.aspx?id=592  
(baixar as instruções pode ajudar a entender o que cada aviso quer dizer)

## Necessita ##
Para rodar Docker toolbox você vai precisar do Hyper-V.  
Para instalar Hyper-V vai precisar do "Remote Server Administration Tools for Windows 7 with Service Pack 1".  

## Hyper-V ##
Painel de controle >>  
Ativar ou desativar recursos do windows >>  
Ferramentas de Administração de Servidor Remoto >>  
Ferramentas de Administração de Funções >>  
Ferramentas do Hyper-V. __(marque isso)__

## Ativando na BIOS ##
Quando o computador esta ligando você pode botar para entrar na BIOS (geralmente é com uma das teclas F, por exemplo F8/F11/F2).  
Desligue seu computador e acesse setup BIOS ou algo do tipo.  
Procure algo sobre virtualização e ative essa opção.
