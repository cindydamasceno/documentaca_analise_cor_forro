# **Uma análise colométrica do Forró**

Há diversas maneiras de se falar de amor no Forró – é um gênero quente e vivo e colorido.

Este _script_ traz, em etapas, como procurar os 200 artistas de forró mais populares via Spotify e traz a contagem de cores mais utilizadas nas capas desde o pioneiro do gênero, Abios e Vaquejadas, lançado por Luiz Gonzaga em 1956.
<hr>

## Utilizando Spotipy para reunir artistas mais populares do Gênero Forró

A Biblioteca Python **Spotipy** foi utilizada para acessar informações do Spotify. Ela reduz a burocracia da WebAPI, trazendo rapidez para o acesso de informações. Aqui, ela é utilizada em dois momentos: para listas os artistas mais populares no gênero forró e para encontrar a capa de todos os álbuns registrados na plataforma para aquele artista. Como a API limita a 50 artistas por solicitação, foi utilizado o parâmetro offset de modo a aumentar a quantidade de artistas lidos até atingir a quantidade desejada. 

```python
# OFFSET: É COMO UMA PAGINAÇÃO. QUANDO ELE É 0, ELE PEGA OS ARTISTAS DE 0 A 50. QUANDO É 50, PEGA OS PRÓXIMOS 50 (50 A 100)

paginas=[0,50,100,150] # PEGA OS 150 PRIMEIROS ARTISTAS QUE APARECEM NO SPOTIFY PARA PESQUISA "FORRÓ"


dados_completos=pd.DataFrame()

for pagina in paginas:
    print(pagina)
    resultado = sp.search(q='genre:"forro"', type='artist',offset=pagina,limit=50)

    dados=pd.DataFrame()

    for artista in tqdm(resultado['artists']['items'],desc="Artistas"):
       
        nome=(artista['name'])
        foto=(artista['images'][0]['url'])
        generos=', '.join(artista['genres'])
        seguidores=(artista['followers']['total'])
        id=(artista['id'])
        popularidade=(artista['popularity'])

        df=pd.DataFrame({
            "pagina":[pagina], # COLOCA A PÁGINACAO PRA NÃO SE PERDER
            "id":[id],
            "artista":[nome],
            "foto":[foto],
            "generos":[generos],
            "seguidores":[seguidores],
            "popularidade":[popularidade],
        })

        dados=pd.concat([dados,df],ignore_index=True)
    
    dados_completos=pd.concat([dados_completos,dados],ignore_index=True)
```



