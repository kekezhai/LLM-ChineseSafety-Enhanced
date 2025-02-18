# LLM-ChineseSafety-Enhanced

## 介绍
- **基于多维度攻击防御增强的大模型生成安全性方法**

当前大模型在面对复杂攻击指令时容易生成有害内容，从而使得大模型的防御能力显著下降，本文针对这个问题提出了一种基于多维度攻击防御对齐数据构建的方法来增强大模型的生成安全性。本文方法的核心是通过创新方法增加攻击指令维度多样性和生成安全回复的准确性来提升大模型安全对齐学习的效果。为了验证该方法的有效性，在已有的安全评测基准测试之外我们额外设计了新的安全评测基准测试，并使用Llama-3.2-1B-Instruct作为基线模型进行对照实验验证。最终实验效果证明了我们的方法可以显著提升大模型在复杂指令攻击下的生成安全性，同时兼顾模型通用能力的保持和提升。论文详见: [A Method for Enhancing the Safety of Large Model Generation Based on Multi-dimensional Attack and Defense](https://arxiv.org/abs/2501.00517)


## 模型地址
[Llama-3.2-1B-Instruct-ChineseSafety-Enhanced](https://modelscope.cn/models/kkzhai/Llama-3.2-1B-Instruct-ChineseSafety-Enhanced)

### 模型训练
```
安装LLaMA-Factory：
   git clone --depth 1 https://github.com/hiyouga/LLaMA-Factory.git
   cd LLaMA-Factory
   pip install -e ".[torch,metrics]"
执行训练脚本：sh train.sh
```
### SafetyBench评估
```
git clone https://github.com/thu-coai/SafetyBench.git
执行 ./SafetyBench-main/code/download_data.sh或者download_data.py 获取评测问题和few-shot样例
执行 ./SafetyBench-main/code/evaluate_llama3.2_1b_sft.py 对待评估模型进行安全测试
输出结果 ./SafetyBench-main/data/test_zh_eva_Llama-3.2-1B-Instruct-ChineseSafety-Enhanced1.0_zeroshotFalse_res_processed.json

登录SafetyBench安全评测平台: https://llmbench.ai/safety/submit提交上一步输出结果
评估结果示例如下:
Avg.	EM	IA	MH	OFF	PH	PP	UB	Type	
59.6	55.4	67.3	71.4	56.3	54.1	69.5	46.6	zh	
```
### 通用能力评估
```
提前安装LLaMA-Factory，使用内置工具评估
llamafactory-cli eval ./eval_conf/llama3.2_1b_sft_mmlu_eval.yaml
llamafactory-cli eval ./eval_conf/llama3.2_1b_sft_cmmlu_eval.yaml
llamafactory-cli eval ./eval_conf/llama3.2_1b_sft_ceval_eval.yaml
```




