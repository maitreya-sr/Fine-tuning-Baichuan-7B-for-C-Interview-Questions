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

## Next Steps
Moving forward, we plan to:
1. Conduct further hyperparameter tuning to refine model performance.
2. Introduce additional domain-specific datasets for broader generalization.
3. Deploy the model in an interactive system for real-world evaluation.

These steps will help validate the effectiveness of our fine-tuning approach and further optimize the model for industry-specific applications.
