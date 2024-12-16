# **Uma análise colométrica do Forró**

Há diversas maneiras de se falar de amor no Forró – é um gênero quente e vivo e colorido.

Este _script_ traz, em etapas, como procurar os 200 artistas de forró mais populares via Spotify e traz a contagem de cores mais utilizadas nas capas desde o pioneiro do gênero, Abios e Vaquejadas, lançado por Luiz Gonzaga em 1956.
<hr>

## Utilizando Spotipy para reunir artistas mais populares do Gênero Forró

A Biblioteca Python **Spotipy** foi utilizada para acessar informações do Spotify. Ela reduz a burocracia da WebAPI, trazendo rapidez para o acesso de informações. Aqui, ela é utilizada em dois momentos: para listas os artistas mais populares no gênero forró e para encontrar a capa de todos os álbuns registrados na plataforma para aquele artista. Como a API limita a 50 artistas por solicitação, foi utilizado o parâmetro offset de modo a aumentar a quantidade de artistas lidos até atingir a quantidade desejada. 



