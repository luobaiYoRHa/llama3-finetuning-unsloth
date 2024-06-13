# llama3-finetuning-unsloth
本项目采用了unsloth的Llama3微调框架，并使用自制的微调用数据集，对Llama3进行微调。通过这些微调，使得Llama3能够模拟特定小说、电影或游戏中的某个角色的语气和性格特点，与使用者进行交流。

## Try it now
我已将我训练出来的模型upload到github上了，下载Paimon-unsloth.Q4_K_M.gguf，并使用类似于chat4All或者Ollama的platform便能在local直接使用此微调的llama3模型。我使用了原神里的派蒙文本作为此模型的训练集，并且加入了一些规范化的AI问答和一些使用派蒙语气的AI问答（称之为mutation）来训练特化的派蒙AI模型，此模型在微调之后可以使用派蒙的语气和性格特点来和使用者做出一些简单的交互，在未来，希望能够通过拓展数据集来做出更多高级的交互。

## Installation
1、使用unsloth的fine tuning框架微调模型
具体code参考这个链接：https://colab.research.google.com/drive/1RwPqpLXfrt85QQ8dXl5cS5EJzycOwWDu?usp=sharing
我已将权限设为有link就能访问

2、准备数据集

