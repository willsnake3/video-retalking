<div align="center">

<h2>VideoReTalking <br/> <span style="font-size:12px">Sincronização labial baseada em áudio para edição de vídeo do Talking Head</span> </h2> 

  <a href='https://arxiv.org/abs/2211.14758'><img src='https://img.shields.io/badge/ArXiv-2211.14758-red'></a> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<a href='https://vinthony.github.io/video-retalking/'><img src='https://img.shields.io/badge/Project-Page-Green'></a> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/vinthony/video-retalking/blob/main/quick_demo.ipynb)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
[![Replicate](https://replicate.com/cjwbw/video-retalking/badge)](https://replicate.com/cjwbw/video-retalking)

<div>
    <a target='_blank'>Kun Cheng <sup>*,1,2</sup> </a>&emsp;
    <a href='https://vinthony.github.io/' target='_blank'>Xiaodong Cun <sup>*,2</a>&emsp;
    <a href='https://yzhang2016.github.io/yongnorriszhang.github.io/' target='_blank'>Yong Zhang <sup>2</sup></a>&emsp;
    <a href='https://menghanxia.github.io/' target='_blank'>Menghan Xia <sup>2</sup></a>&emsp;
    <a href='https://feiiyin.github.io/' target='_blank'>Fei Yin <sup>2,3</sup></a>&emsp;<br/>
    <a href='https://web.xidian.edu.cn/mrzhu/en/index.html' target='_blank'>Mingrui Zhu <sup>1</sup></a>&emsp;
    <a href='https://xuanwangvc.github.io/' target='_blank'>Xuan Wang <sup>2</sup></a>&emsp;
    <a href='https://juewang725.github.io/' target='_blank'>Jue Wang <sup>2</sup></a>&emsp;
    <a href='https://web.xidian.edu.cn/nnwang/en/index.html' target='_blank'>Nannan Wang <sup>1</sup></a>
</div>
<br>
<div>
    <sup>1</sup> Xidian University &emsp; <sup>2</sup> Tencent AI Lab &emsp; <sup>3</sup> Tsinghua University
</div>
<br>
<i><strong><a href='https://sa2022.siggraph.org/' target='_blank'>SIGGRAPH Asia 2022 Conference Track</a></strong></i>
<br>
<br>
<img src="https://opentalker.github.io/video-retalking/static/images/teaser.png" width="768px">


<div align="justify">  <BR> Apresentamos o VideoReTalking, um novo sistema para editar os rostos de um vídeo falante do mundo real de acordo com o áudio de entrada, produzindo um vídeo de saída de alta qualidade e sincronização labial, mesmo com uma emoção diferente. Nosso sistema divide esse objetivo em três tarefas sequenciais:
  
 <BR> (1) geração de vídeo facial com expressão canônica
<BR> (2) sincronização labial baseada em áudio e
  <BR> (3) aprimoramento facial para melhorar o fotorrealismo.
  
 <BR>  Dado um vídeo talk-head, primeiro modificamos a expressão de cada quadro de acordo com o mesmo modelo de expressão usando a rede de edição de expressão, resultando em um vídeo com a expressão canônica. Este vídeo, juntamente com o áudio fornecido, é então alimentado na rede de sincronização labial para gerar um vídeo com sincronização labial. Finalmente, melhoramos o fotorrealismo dos rostos sintetizados através de uma rede de aprimoramento facial com reconhecimento de identidade e pós-processamento. Usamos abordagens baseadas em aprendizagem para todas as três etapas e todos os nossos módulos podem ser abordados em um pipeline sequencial, sem qualquer intervenção do usuário.</div>
<BR>

<p>
<img alt='pipeline' src="./docs/static/images/pipeline.png?raw=true" width="768px"><br>
<em align='center'>Pipeline</em>
</p>

</div>

## Resultados (contém áudio)
https://user-images.githubusercontent.com/4397546/224310754-665eb2dd-aadc-47dc-b1f9-2029a937b20a.mp4




## Ambiente
```
git clone https://github.com/vinthony/video-retalking.git
cd video-retalking
conda create -n video_retalking python=3.8
conda activate video_retalking

conda install ffmpeg

# Please follow the instructions from https://pytorch.org/get-started/previous-versions/
# This installation command only works on CUDA 11.1
pip install torch==1.9.0+cu111 torchvision==0.10.0+cu111 -f https://download.pytorch.org/whl/torch_stable.html

pip install -r requirements.txt
```

## Inferência Rápida

#### Modelos pré-treinados
Baixe nossos [modelos pré-treinados](https://drive.google.com/drive/folders/18rhjMpxK8LVVxf7PI6XwOidt8Vouv_H0?usp=share_link)  e coloque-os em `./checkpoints`.

<!-- We also provide some [example videos and audio](https://drive.google.com/drive/folders/14OwbNGDCAMPPdY-l_xO1axpUjkPxI9Dv?usp=share_link). Please put them in `./examples`. -->

#### Inference

```
python3 inference.py \
  --face examples/face/1.mp4 \
  --audio examples/audio/1.wav \
  --outfile results/1_1.mp4
```
Este script inclui etapas de pré-processamento de dados. Você pode testar qualquer vídeo de rosto falante sem alinhamento manual. Mas é importante notar que a DNet não consegue lidar com poses extremas.

Você também pode controlar a expressão adicionando os seguintes parâmetros:

```--exp_img```: Modelo de expressão predefinido. O padrão é "neutro". Você pode escolher "sorriso" ou um caminho de imagem.

```--up_face```: Você pode escolher "surpresa" ou "zangado" para modificar a expressão da face superior com [GANimation](https://github.com/donydchen/ganimation_replicate).



## Citação

Se você achar nosso trabalho útil em sua pesquisa, considere citar:

```
@misc{cheng2022videoretalking,
        title={VideoReTalking: Audio-based Lip Synchronization for Talking Head Video Editing In the Wild}, 
        author={Kun Cheng and Xiaodong Cun and Yong Zhang and Menghan Xia and Fei Yin and Mingrui Zhu and Xuan Wang and Jue Wang and Nannan Wang},
        year={2022},
        eprint={2211.14758},
        archivePrefix={arXiv},
        primaryClass={cs.CV}
  }
```

## Reconhecimento
Obrigado a 
[Wav2Lip](https://github.com/Rudrabha/Wav2Lip),
[PIRenderer](https://github.com/RenYurui/PIRender), 
[GFP-GAN](https://github.com/TencentARC/GFPGAN), 
[GPEN](https://github.com/yangxy/GPEN),
[ganimation_replicate](https://github.com/donydchen/ganimation_replicate),
[STIT](https://github.com/rotemtzaban/STIT)
por compartilhar seu código.


## Trabalho relacionado
- [StyleHEAT: One-Shot High-Resolution Editable Talking Face Generation via Pre-trained StyleGAN (ECCV 2022)](https://github.com/FeiiYin/StyleHEAT)
- [CodeTalker: Speech-Driven 3D Facial Animation with Discrete Motion Prior (CVPR 2023)](https://github.com/Doubiiu/CodeTalker)
- [SadTalker: Learning Realistic 3D Motion Coefficients for Stylized Audio-Driven Single Image Talking Face Animation (CVPR 2023)](https://github.com/Winfredy/SadTalker)
- [DPE: Disentanglement of Pose and Expression for General Video Portrait Editing (CVPR 2023)](https://github.com/Carlyx/DPE)
- [3D GAN Inversion with Facial Symmetry Prior (CVPR 2023)](https://github.com/FeiiYin/SPI/)
- [T2M-GPT: Generating Human Motion from Textual Descriptions with Discrete Representations (CVPR 2023)](https://github.com/Mael-zys/T2M-GPT)

##  Isenção de responsabilidade

Este não é um produto oficial da Tencent.

```
1. Leia atentamente e cumpra a licença de código aberto aplicável a este código antes de usá-lo.
2. Leia atentamente e cumpra a declaração de propriedade intelectual aplicável a este código antes de utilizá-lo.
3. Este código-fonte aberto é executado totalmente offline e não coleta nenhuma informação pessoal ou outros dados. Se você usar este código para fornecer serviços a usuários finais e coletar dados relacionados, tome as medidas de conformidade necessárias de acordo com as leis e regulamentos aplicáveis ​​(como publicação de políticas de privacidade, adoção de estratégias de segurança de dados necessárias, etc.). Caso os dados recolhidos envolvam informações pessoais, deverá ser obtido o consentimento do utilizador (se aplicável). Quaisquer responsabilidades legais decorrentes disso não estão relacionadas à Tencent.
4. Sem a permissão por escrito da Tencent, você não está autorizado a usar os nomes ou logotipos de propriedade legal da Tencent, como "Tencent". Caso contrário, você poderá ser responsabilizado por suas responsabilidades legais.
5. Este código-fonte aberto não tem a capacidade de fornecer serviços diretamente aos usuários finais. Se você precisar usar este código para treinamento adicional ou demonstrações de modelos, como parte de seu produto para fornecer serviços aos usuários finais ou para uso semelhante, cumpra as leis e regulamentos aplicáveis ​​ao seu produto ou serviço. Quaisquer responsabilidades legais decorrentes disso não estão relacionadas à Tencent.
6. É proibido usar este código-fonte aberto para atividades que prejudiquem os direitos e interesses legítimos de terceiros (incluindo, entre outros, fraude, engano, violação dos direitos de retrato, direitos de reputação de terceiros, etc.) ou outros comportamentos. que violem as leis e regulamentos aplicáveis ​​ou que vão contra a ética social e os bons costumes (incluindo o fornecimento de informações incorretas ou falsas, a divulgação de informações pornográficas, terroristas e violentas, etc.). Caso contrário, você poderá ser responsabilizado por suas responsabilidades legais.

```
## Tudo graças aos nossos colaboradores 

<a href="https://github.com/OpenTalker/video-retalking/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=OpenTalker/video-retalking" />
</a>
