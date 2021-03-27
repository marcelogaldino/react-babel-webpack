# WebPack

<blockquote alt="[ignore]">
<p>
    Confira esse projeto aqui <a href="https://github.com/marcelogaldino/react-babel" >React com Babel</a> antes de prosseguir com este para um melhor entendimento das ferramentas Babel e Webpack em projetos com React. 
</p>
</blockquote>

<br>

O babel apenas transpila o nosso código js, já o webpack, nos da funcionalidades de import por exemplo, para importamos arquivos .js, .css .png dentro do javascript. O Webpack automatiza o processo de identificar o que precisamos importar (CSS, imagens, js) e ativa os loaders para para fazer isso. Existe o  css-loader, image-loader...

Na raiz do projeto crie um arquivo chamado  webpack.config.js com o seguinte conteúdo

```jsx
const path = require('path')

module.exports = {
    entry: path.resolve(__dirname, 'src', 'index.js'),
    output: {
        path: path.resolve(__dirname, 'public'),
        filename: 'bundle.js'
    },
    devServer: {
        contentBase: path.resolve(__dirname, 'public')
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader'
                }
            }
        ]
    } 
}
```

Nesse arquivo, basicamente dizemos ao webpack quais são os nossos arquivos de entrada (index.js) e o arquivo de saída (o nosso bundle) que esta na pasta public (bundle.js).

Também configuramos algumas regras com expressões regulares, para transpilar usando o babel-loader todos os arquivos que terminam com .js exceto a pasta node_modules.

Ao executar o comando abaixo, podemos olhar que o nosso arquivo bundle.js foi modificado

```bash
yarn webpack --mode development
```

Mas toda vez que houver uma alteração na nossa aplicação temos que rodar novamente o comando acima, para resolver isso, vamos instalar o webpack-dev-server para habilitar o live reload

```bash
# a flag -D instala como uma depêndencia de desenvolvimento
yarn add webpack-dev-server -D
```

Para rodar o projeto execute o comando abaixo

```bash
yarn webpack serve --mode development
```

Você pode acessar seu projeto agora na url [http://localhost:8080](http://localhost:8080) e vera que no seu terminal a aplicação continuará em execução esperando por atualizações. Além disso as funcionalidades de import ja podem ser utilizadas
