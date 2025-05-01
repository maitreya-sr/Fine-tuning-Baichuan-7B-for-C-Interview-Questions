# Fine-tuning Baichuan-7B for C++ Interview Questions

## video link
https://youtu.be/3CdDrnwF8mg

## Project Description
This project focuses on adapting the Baichuan-7B large language model for industry-specific applications, specifically in the domain of C++ interview questions. The goal is to improve the model's ability to generate accurate and professional responses to C++ technical queries through fine-tuning.

## Preliminary Data Visualization
The dataset consists of 1067 C++ interview questions and answers, sourced from online interview experiences and GPT-4-generated content. The dataset is divided as follows:
- **Training Set**: 1028 examples
- **Test Set**: 39 examples

### Training set example
"instruction": "什么是 std::string 类？它与C风格的字符串有什么区别？",

"input": "",

"output": "std::string 类是C++标准库中的一个类，用于表示和操作字符串。它提供了很多成员函数和操作符重载，使得字符串的操作更加方便和安全。\n\n与C风格的字符串相比，std::string 类有以下区别：\n\n1. 动态分配内存：std::string 类会自动进行内存管理，对字符串的长度进行动态分配和管理，不需要手动分配和释放内存，避免了内存泄漏或缓冲区溢出的风险。\n\n2. 字符串长度：std::string 类存储了其长度信息，可以通过成员函数 size() 或 length() 获取字符串的长度，而C风格的字符串只能通过遍历整个字符串来计算长度。\n\n3. 可变性：std::string 类提供了许多成员函数来修改存储的字符串，例如插入、删除、替换等操作，而C风格的字符串是不可变的，一旦初始化后就不能再修改。\n\n4. 字符串连接操作：std::string 类支持使用\"+\"运算符进行字符串的连接，而对于C风格的字符串，连接需要通过 strcat() 函数或者手动实现。\n\n5. 字符串比较操作：std::string 类有成员函数用于比较字符串的大小关系，如比较相等、大于或小于等，而C风格的字符串只能使用 strcmp() 函数进行比较。\n\n总而言之，std::string 类提供了更多的功能和安全性，使得字符串的操作更加方便和高效，是C++中推荐使用的字符串表示方式。"

English translation:
"instruction": "What is the std::string class? How does it differ from C-style strings?",

"input": "",

"output": "The std::string class is a class in the C++ standard library used to represent and manipulate strings. It provides many member functions and operator overloads, making string operations more convenient and secure.\n\nCompared to C-style strings, the std::string class has the following differences:\n\n1. Dynamic memory allocation: The std::string class automatically manages memory, dynamically allocating and managing the length of the string. There is no need to manually allocate or release memory, avoiding risks such as memory leaks or buffer overflows.\n\n2. String length: The std::string class stores its length information, and the length of the string can be obtained using member functions such as size() or length(). In contrast, C-style strings require traversing the entire string to calculate the length.\n\n3. Mutability: The std::string class provides many member functions to modify the stored string, such as insert, delete, and replace operations. C-style strings, on the other hand, are immutable and cannot be modified once initialized.\n\n4. String concatenation: The std::string class supports the use of the "+" operator for string concatenation, whereas C-style strings require the use of the strcat() function or manual implementation for concatenation.\n\n5. String comparison: The std::string class has member functions for comparing string relationships, such as equality, greater than, or less than. C-style strings, however, can only be compared using the strcmp() function.\n\nIn summary, the std::string class provides more functionality and safety, making string operations more convenient and efficient. It is the recommended way to represent strings in C++."


## Data Processing Details
The data processing steps completed so far include:
1. **Data Cleaning**: Removed duplicate and incomplete questions.
2. **Tokenization**: Applied subword tokenization to ensure compatibility with the Baichuan-7B tokenizer.
3. **Normalization**: Standardized text formatting, such as converting all characters to lowercase and removing extraneous punctuation.
4. **Dataset Splitting**: Ensured a meaningful test set by selecting diverse questions representative of different C++ topics.

## Modeling Methods Used So Far
We used **LoRA (Low-Rank Adaptation)** for efficient fine-tuning of the Baichuan-7B model. Training was conducted over **25 epochs** until convergence. The training methodology involved:
- **Loss Function**: Cross-entropy loss for supervised fine-tuning.
- **Optimizer**: AdamW with a learning rate scheduler.
- **Evaluation Metrics**: BLEU-4, ROUGE-1, ROUGE-2, and ROUGE-L scores to assess response similarity with ground truth answers.

## Preliminary Results
- **Metric Improvements**:
  - BLEU-4 increased from **21.25** to **26.31** (+23%)
  - ROUGE-1 increased from **46.67** to **50.96** (+9%)
  - ROUGE-2 increased from **22.37** to **26.51** (+19%)
  - ROUGE-L increased from **32.41** to **35.54** (+10%)

- **Qualitative Observations**:
  - The pre-trained model exhibited repetition and irrelevant outputs for technical questions.
  - After fine-tuning, the model provided more structured, relevant, and accurate answers.
  - Compared to human responses (e.g., from Zhihu discussions), the fine-tuned model demonstrated improved coherence and correctness.

## Environment Setup

### 1. Clone this repository

### 2. Download the Baichuan-7B pretrained model
```bash
# From the project root, create a folder for the model
mkdir baichuan-inc
cd baichuan-inc

git lfs install
git clone https://huggingface.co/baichuan-inc/baichuan-7B

#### 3. Install Python dependencies
```sh
pip3 install -r requirements.txt
```

#### 4. Hardware requirements
- GPU memory ≥ 18 GB


## Fine-Tuning
### 1. Prepare the data
Put the training and test files in the data directory or supply your own dataset in the same schema：
```json
[
    {
        "instruction": "C++ 虚析构函数有什么作用？",
        "input": "",
        "output": "C++中，虚析构函数用于在多态场景下正确释放一个对象的资源。\n\n当一个类中存在虚函数时，该类通常也应该拥有一个虚析构函数。虚析构函数能够确保当通过基类指针删除一个派生类对象时，调用正确的析构函数，从而正确释放对象的资源。\n\n如果派生类中的析构函数不是虚函数，那么当通过基类指针删除派生类对象时，只会调用基类的析构函数，而不会调用派生类的析构函数。这可能导致派生类对象中的资源无法被正确释放，造成内存泄漏等问题。\n\n因此，使用虚析构函数可以确保在多态场景下正确释放对象资源，防止内存泄漏等问题的发生。"
    },
     {
        "instruction": "C++ 虚函数与普通成员函数的区别是什么？",
        "input": "",
        "output": "C++中的虚函数和普通成员函数之间有几个主要的区别：\n\n1. 声明方式：虚函数通过在基类中使用关键字`virtual`进行声明，而普通成员函数没有这个关键字。\n\n2. 动态绑定：使用了虚函数的类在运行时实现了动态绑定（也称为后期绑定或运行时多态），这意味着调用虚函数的时候，实际调用的具体实现将根据对象的类型决定。而普通成员函数在编译时通过静态绑定（也称为早期绑定或编译时多态）确定调用的具体实现。\n\n3. 表现形式：虚函数通常在基类中声明，并在派生类中重写。这使得我们可以使用基类的指针或引用调用派生类对象的虚函数，以实现多态性。普通成员函数没有这种特性。\n\n4. 动态绑定的开销：虚函数的动态绑定带来了额外的开销，涉及到虚函数指针和虚函数表（vtable）的查找。而普通成员函数的调用没有这样的开销。\n\n总而言之，虚函数的主要特点是实现动态绑定，可以在运行时根据对象的类型调用不同的实现，而普通成员函数没有这个能力。虚函数的动态绑定需要额外的开销，因此在性能要求高的场景下可能不适合使用。"
    },
]
```

### 2. LoRA Fine-Tuning

#### Continue training from an existing LoRA checkpoint

A previously fine-tuned checkpoint is stored in the baichuan_lora_checkpoint directory. You can resume LoRA fine-tuning from it.

CUDA_VISIBLE_DEVICES=0: single-GPU training

--model_name_or_path: path to the pretrained model

--dataset: training dataset

--checkpoint_dir: path to the existing LoRA checkpoint

--output_dir: directory where the new checkpoint will be saved

```sh
CUDA_VISIBLE_DEVICES=0 python src/finetune_lora.py \
    --model_name_or_path baichuan-inc/baichuan-7B \
    --do_train \
    --dataset_dir data \
    --dataset cpp_interview_train \
    --max_source_length 256 \
    --max_target_length 3000 \
    --checkpoint_dir baichuan_lora_checkpoint \
    --output_dir baichuan_lora_checkpoint2 \
    --overwrite_cache \
    --per_device_train_batch_size 1 \
    --gradient_accumulation_steps 1 \
    --lr_scheduler_type cosine \
    --logging_steps 10 \
    --save_steps 1000 \
    --learning_rate 5e-5 \
    --num_train_epochs 10.0 \
    --plot_loss \
    --fp16  \
    --dev_ratio 0.05 \
    --lora_target W_pack
```

#### Fine-tune directly on the pretrained model
You can choose either this step or the previous one.

CUDA_VISIBLE_DEVICES=0: single-GPU training

--model_name_or_path: path to the pretrained model

--dataset: training dataset

--output_dir: directory where the new checkpoint will be saved

```sh
CUDA_VISIBLE_DEVICES=0 python src/finetune_lora.py \
    --model_name_or_path baichuan-inc/baichuan-7B \
    --do_train \
    --dataset_dir data \
    --dataset cpp_interview_train \
    --max_source_length 256 \
    --max_target_length 3000 \
    --output_dir baichuan_lora_checkpoint \
    --overwrite_cache \
    --per_device_train_batch_size 1 \
    --gradient_accumulation_steps 1 \
    --lr_scheduler_type cosine \
    --logging_steps 10 \
    --save_steps 1000 \
    --learning_rate 5e-5 \
    --num_train_epochs 10.0 \
    --plot_loss \
    --fp16  \
    --dev_ratio 0.05 \
    --lora_target W_pack
```

#### Evaluate the fine-tuned model
--model_name_or_path: path to the pretrained model

--checkpoint_dir: path to the fine-tuned checkpoint

--output_dir: directory where the evaluation results will be saved

```sh
CUDA_VISIBLE_DEVICES=0 python src/finetune_lora.py \
    --model_name_or_path baichuan-inc/baichuan-7B \
    --do_eval \
    --dataset_dir data \
    --dataset cpp_interview_test \
    --checkpoint_dir baichuan_lora_checkpoint \
    --output_dir baichuan_lora_eval_result \
    --per_device_eval_batch_size 4 \
    --max_samples 100 \
    --predict_with_generate
    
```

#### Chat with the model
--model_name_or_path: path to the pretrained model

--checkpoint_dir: path to the fine-tuned checkpoint

```sh
python src/cli_demo.py \
    --model_name_or_path baichuan-inc/baichuan-7B \
    --checkpoint_dir baichuan_lora_checkpoint \
    --max_new_tokens 1024
```

