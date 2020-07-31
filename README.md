# Estudo arquiteturas STT GIT - reconhecimento de fala

Estudo de arquiteturas de reconhecimento de fala(speech recognition) para a língua portuguesa (Brasil), problema conhecido também como Speech-To-Text. 

## Base de Dados - Português Brasil

### Corpus CEFALA 1

Os arquivos de audio utilizados para o reconhecimento de fala em português fazem parte da base de dados [Corpus CEFALA-1](https://www.cefala.org/pages/base-de-dados-corpus-cefala-1.html#base-de-dados-corpus-cefala-1) do Centro de Estudos da Fala, Acústica, Linguagem e músicA (CEFALA-UFMG). O Corpus CEFALA-1 possui audios de 104 locutores diferentes. Cada locutor foi gravado com 5 microfones diferentes, o que gera 5 arquivos de audio distintos para cada locutor. Cada arquivo de audio é dividido em três partes. O primeiro segmento é referente a fala espontânea, o segundo segmento refere-se a leitura de um texto longo e por último segmentos referentes a leitura de 20 frases curtas. Os textos referentes a fala espontânea não são disponibilizados. O texto longo e as 20 frases podem ser encontradas no arquivo "CorpusCEFALA1_textos.json". Para segmentação dos audios é disponibilizado arquivos TEXTGRID. A extensão TEXTGRID pode ser visualizada com o [Praat](https://www.fon.hum.uva.nl/praat/) juntamente com os arquivos de audio. O Praat é um software livre criado por Paul Boersma e David Weenink da Universidade de Amsterdã. O pacote de Python "praat-textgrid" foi usado para manipulação do arquivo TEXTGRID. Esse pacote pode ser  instalado com o seguinde comando:

```bash
pip install praat-textgrids
```

Esse pacote foi utilizado para segmentar os arquivos de audios originais com os arquivos TEXTGRID originais, e também para gerar novos arquivos TEXTGRID para particionar os arquivos de audio referente a leitura de texto, juntamente com a ajuda do pacote "aeneas". O pacote "aeneas" pode ser instalado com o seguinte comando:

```bash
pip install aeneas
```
Para a segmentação dos audios referentes ao texto além do pacote aeneas, é utilizado também o arquivo "CorpusCEFALA1_TEXTO.txt" que divide os paragrafos com uma quebra de linha. Assim o pacote aeneas segmenta os audios em cada paragrafo.

Após download do Corpus CEFALA1, colocar o diretório CorpusCEFALA1 dentro da pasta "data"

```bash
data/CorpusCEFALA1
```

Para o pré-processamento é necessário também fazer download também da pasta "SEG"" com todos os arquivos textgrid. Colocar esta pasta dentro do diretório "data/CorpusCEFALA1""

```bash
data/CorpusCEFALA1/SEG
```

Obs: Pasta SEG utilizada para o pré-processamento do Corpus CEFALA1 com o notebook de jupyter.

### Corpus - C-ORAL-BRASIL


O projeto [C-ORAL-BRASIL](http://www.c-oral-brasil.org/) visa ao estudo da fala espontânea do português brasileiro. O projeto tem sua sede no Laboratório de Estudos Empíricos e Experimentais da Linguagem ([LEEL](http://www.letras.ufmg.br/leel/)) da Faculdade de letras da UFMG, coordenados pelos professores Tommaso Raso e Heliana Mello.

Consiste em um conjunto de audios referentes a conversações entre diferentes locutores. E acompanhado de arquivo que contém a transcrição dos audios, porém precisam de ser tratados para retirar informações e o que não é necessário.

## Modelos STT - Git

Ao invés de baixar direto do Git o repositório, usar o repositório dentro desta pasta com as configurações para o treinamento em português.

### SpeechWavenet

O modelo [Speech-to-Text-WaveNet](https://github.com/buriburisuri/speech-to-text-wavenet) não possui artigo, somente o repositório no Github. 

No repositório, tem-se os arquivos para fazer o treinamento com base de dados em inglês. Baseando-se nesses arquivos, foi gerado dois notebooks de jupyter com scripts em python para realizar o treinamento com a base de dados em português.

O modelo tbm tem alguns pré-requisitos de versão de pacotes, como o tensorflow e sugartensor. Neste caso é indicado criar um novo ambiente com a versão do Python 3.5.6.

Com o conda pode ser criado com o seguinte comando:

```
conda create -n speech-wavenet python=3.5.6
```
Após a criação do ambiente, para configuração dos pacotes do python pode-se usar o arquivo "require_speechwavenet_pt.txt"

```
pip install -r require_speechwavenet_pt.txt
```

Após a configuração do ambiente será possível a utilização dos scripts em python dos notebooks de jupyter.

* CorpusCEFALA1-process.ipynb

* Train-Speech-Wavenet.ipynb

Caso os scripts no notebook "Train-Speech-Wavenet.ipynb" estejam todos funcionando, pode se usar o script:

```
python train.py
```

A seguir um exemplo da convergência do modelo com os dados Corpus CEFALA1:

![Função de custo no treinamento Corpus CEFALA1](loss-train-speechwavenet.png?raw=true "Title")

### Deep Speech 

O [DeepSpeech](https://github.com/mozilla/DeepSpeech) é o modelo do Baidu. Ah também um pacote python do deepspeech para usar com os modelos gerados nos treinamentos.

```bash
pip install deepspeech
```

Baixar modelo em inglês pré treinado para o deepspeech(1.8Gb)

```bash
wget https://github.com/mozilla/DeepSpeech/releases/download/v0.5.1/deepspeech-0.5.1-models.tar.gz

tar xvfz deepspeech-0.5.1-models.tar.gz
```

Altere o nome da nova pasta criada para "models".

## Usar

Com o comando a seguir você consegue acessar os arquivos "CorpusCEFALA1-process.ipynb" e "Train-Speech-Wavenet.ipynb".

```bash
jupyter-notebook
```


## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)

