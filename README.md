# django-vercel-app

Criar arquivo `vercel.json` na raiz do projeto, setando o nome do seu projeto. No meu caso `vercel/wsgi.py`

```json
{
  "version": 2,
  "builds": [
    {
      "src": "vercel/wsgi.py",
      "use": "@vercel/python",
      "config": { "maxLambdaSize": "15mb", "runtime": "python3.9" }
    },
    {
      "src": "build_files.sh",
      "use": "@vercel/static-build",
      "config": {
        "distDir": "staticfiles_build"
      }
    }
  ],
  "routes": [
    {
      "src": "/static/(.*)",
      "dest": "/static/$1"
    },
    {
      "src": "/(.*)",
      "dest": "vercel/wsgi.py"
    }
  ]
}
```

No arquivo `vercel/wsgi.py` adicionar o seguinte trecho no final do arquivo.

```python
app = application
```


No arquivo `settings.py` adicionar

```python
STATIC_URL = '/static/'
STATIC_ROOT = BASE_DIR / 'staticfiles'
```

Após adicionar as configurações acima, podemos realizar o build do projeto. Importando o repositório do github na vercel e seguindo com as opções default da vercel.

