# llama3-finetuning-unsloth
本项目采用了unsloth的Llama3微调框架，并使用自制的微调用数据集，对Llama3进行微调。通过这些微调，使得Llama3能够模拟特定小说、电影或游戏中的某个角色的语气和性格特点，与使用者进行交流。

## Try it now
我已将我训练出来的模型upload到github上了，下载Paimon-unsloth.Q4_K_M.gguf，并使用类似于chat4All或者Ollama的platform便能在local直接使用此微调的llama3模型。我使用了原神里的派蒙文本作为此模型的训练集，并且加入了一些规范化的AI问答和一些使用派蒙语气的AI问答（称之为mutation）来训练特化的派蒙AI模型，此模型在微调之后可以使用派蒙的语气和性格特点来和使用者做出一些简单的交互，在未来，希望能够通过拓展数据集来做出更多高级的交互。

## 相关项目
unsloth：https://github.com/unslothai/unsloth
gpt4all：https://gpt4all.io/
triton：https://github.com/openai/triton
llama.cpp：https://github.com/ggerganov/llama.cpp

## Installation
1、使用unsloth的fine tuning框架微调模型
具体code参考这个链接：https://colab.research.google.com/drive/1RwPqpLXfrt85QQ8dXl5cS5EJzycOwWDu?usp=sharing
我已将权限设为有link就能访问

2、准备数据集
需要自己自备想训练的人物对话数据集，人物语气特化数据集，规范化的AI数据集可以直接下载standardConversation.json。
如果嫌麻烦，可以直接用我整合好的派蒙数据集进行训练，我已将这个数据集upload到了Huggingface上：https://huggingface.co/uITimeCia/Paimon
我已经训练好的《原神》派蒙的gguf file也已经post到Huggingface上了:https://huggingface.co/uITimeCia/Paimon

3、使用之前的unsloth框架来训练微调模型，具体的code我已经将customized parameter cooment了，请直接参考我的code来进行训练。
