---
layout: post

title: Detecção de assinaturas em listas de presenças - Parte 1
date: 2018-08-21 08:44:21
author: Bruno Teonácio
summary: Parte 1 do algoritmo de detecção de assinaturas em listas de presenças
comments: true
categories: jekyll pdi visao_computacional opencv zbar qrcode assinaturas
tags:
 - jekyll
 - pdi
 - visao_computacional
 - opencv
 - zbar
 - qrcode
 - assinaturas
---
Olá,
<br><br>
Nesse post será iniciado uma discussão acerca de um dos trabalhos desenvolvidos durante a minha graduação na Universidade Federal do Rio Grande do Norte - UFRN.
<br><br>
Nele, iremos tratar de como detectar assinaturas (escritas a mão pelos alunos) em listas de presenças, muito utilizadas em nível de graduação para a presença dos alunos.
<br><br>
<h1>Introdução</h1>
Existem diversas maneiras de obter as presenças dos alunos em uma sala de aula: Pela web (site), por assinatura dos alunos, preenchendo um formulário impresso (com "X", "O", dentre outros símbolos), detecção via reconhecimento facial, detecção via ponto eletrônico, dentre outras.
<br><br>
Focando no método pelas assinaturas dos alunos, é um método bastante utilizado em diversas instituições de ensino superior pelo Brasil (como na UFRN), onde é passado uma lista de assinaturas para os alunos preencherem.
<br><br>
O problema é quando precisa salvar essas assinaturas em algum outro lugar (como na Web), pois demanda um tempo considerável para o docente ter que conferir folha a folha, assinatura a assinatura, para salva-las no site da instutição (muitas vezes o mesmo opta por colocar presença em todos os alunos, todos os dias, para se livrar desse trabalho).
<br><br>
O algoritmo cuja discussão será iniciada aqui visa um reconhecimento automático dessas assinaturas, utilizando de ferramentas como OpenCV (biblioteca multi-linguagem para algoritmos em Visão Computacional) e QR code (código de barras multidimensional bastante conhecido pela internet).
<br>
<h1>Modelo</h1>
Abaixo segue um link para o modelo de lista de assinaturas sobre o qual o algoritmo foi construido:
<br><br>
[Link para o modelo](https://github.com/teonacio/GIT_lista_de_presenca/blob/master/modelo_lista.pdf)
<br><br>
Pergunta 1: Pode usar outro modelo?
<br>
Resposta 1: Não. O algoritmo foi desenvolvido para reconhecer as assinaturas escritas nesse modelo, mas pode ser facilmente adaptado ou ajustado para qualquer instituição (preferencialmente de ensino superior).
<br><br>
Note os QR codes nos cantos da folha, iremos discutir eles mais adiante. Não se preoculpem com a ordem alfabética dos nomes na folha, isso não interfere na detecção.

<h1>QR Codes e ZBar</h1>
Acredito que vocês já devem estar familiarizados com QR codes, certo? De qualquer forma, segue abaixo um modelo de QR code:
![Exemplo de QR code]({{ "/assets/images/qrcode-example.png"}})

Apesar dos círculos vermelhos estarem exagerados - :) - o intuito é explicar que, utilizando a biblioteca ZBar (biblioteca para detecção de QR codes e barcodes em geral), conseguimos recuperar não apenas o conteúdo do QR code scaneado, mas também as posições dos pixels extremos de cada QR code.
<br><br>
Para facilitar a detecção, cada QR code foi configurado com um texto para que, ao ser scaneado, o algoritmo saiba diferenciar os QR codes (SE - Superior Esquerdo, SD - Superior Direito, IE - Inferior Esquerdo, ID - Inferior Direito).
<br><br>
Essa informação é muito útil, pois ao scanear o modelo, recuperamos as posições dos extremos do sub-retângulo com as assinaturas, utilizando apenas as posições dos extremos dos quatro QR codes do modelo (olhe abaixo):
<br><br>
![Modelo da lista de assinaturas com os códigos QR e as informações dos mesmos]({{ "/assets/images/modelo-001.jpg" / absolute_url}})
![Modelo da lista de assinaturas com o ponto do meio selecionado]({{ "/assets/images/modelo-002.jpg" / absolute_url}})
![Modelo da lista de assinaturas com o sub-retângulo das assinaturas selecionado]({{ "/assets/images/modelo-003.jpg" / absolute_url}})

Ou seja: Todo o resto do modelo (espaços em branco) não interferem no algoritmo, e podem ser utilizados para inserir informações acerca da instuição (logotipo, nome) e da turma (disciplina, turno, professor).
<br><br>
No próximo post, iremos tratar como reajustar imagens "desalinhadas" (note na última imagem do post que o sub-retângulo ficou desalinhado, se não for corrigido esse detalhe irá interferir no algoritmo), além de explicar como tratar a imagem de forma binária (essencial para o algoritmo).

Até lá!
