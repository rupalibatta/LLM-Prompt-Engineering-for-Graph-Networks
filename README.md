# LLM-Prompt-Engineering-for-Graph-Networks
CS 159 Project - Exploring Encoding and Prompting Methods for Graph Reasoning in Large Language Models.
This is a snippet from the report, which is included in this repository.

# 1 Summary
This paper aims to compare graph reasoning capabilities on two metrics, encoding type and prompting heuristics. It is hypothesized that LLMs will be more capable at processing text-based graphs that are as close to text it has been trained on before, such as text that sounds natural and appears frequently in training datasets. Therefore, four different sets of graph encodings were generated: texting, commute, citation, and adjacency. This paper also delves into various modern prompting techniques, namely Few-Shot and varieties of Chain of Thought. These methods were compared against a simple Zero-Shot benchmark, totaling five different prompting methods: Zero-Shot, Few-Shot, Random Chain of Thought, Matched Chain of Thought, and Adjacency Chain of Thought. To compare the success of these four encodings and five prompting methods with one another, a bank of ten questions pertaining to directed and weighted graphs was carefully selected. An answer key to these ten questions for each of the forty generated graphs was created algorithmically.
After comparing the LLM-produced answers to the true answers, we found that Random Chain of Thought outperformed the Zero-Shot benchmark by 103%, the best result of our prompting methods. The Adjacency Chain of Thought method, which we proposed to resemble a more computational and quantitative type of prompting, performed unsurprisingly worst. The four encoding types were all marginally similar, with some variation based on subject topic. These results will be fully explored later in this paper.

# 2 Prompting Heuristics
We briefly introduce the prompting methods utilized in this project. 

## 2.1 Prompting types
* Zero-Shot: This method involves giving the model a graph and a list of graph tasks, requesting it to produce the desired output without any prior training specific to the task.
* Few-Shot: This method supplies the model with three graphs, their lists of graph tasks, and their respective answers to such tasks. The model then learns from these examples to handle a new graph and its respective list of tasks. In this project specifically, each example graph was of a distinct encoding type, and the "test" graph was also of a distinct encoding.
* Random-CoT: This method supplies the model with a graph, its list of graph task questions, and the respective answers, along with a Chain-of-Thought reasoning that explains how each answer was obtained. The model then learns from this example to handle a new graph of a different encoding type and its own list of tasks.
* Matched-CoT: This method supplies the model with a graph, its list of graph task questions, and the respective answers, along with a Chain-of-Thought reasoning that explains how each answer was obtained. The model then learns from this example to handle a new graph of the same encoding type and its own list of tasks.
* Adjacency-CoT: This method supplies the model with a graph, its adjacency matrix representation, and its list of graph task questions, all without any prior training.

## 2.2 Graph Question-Answer Tasks

* Edge existence: Determine whether a given edge exists in a graph.
* Node degree: Calculate the degree of a given node in a graph.
* Node count: Count the number of nodes in a graph.
* Edge count: Count the number of edges in a graph.
* Connected nodes: Find all the nodes that are connected to a given node in a graph.
* Cycle check: Determine whether a graph contains a cycle.
* Disconnected nodes: Find all the nodes that are not connected to a given node in a graph.
* Reachability: Determine whether there is a path from one node to another.
* Shortest path: Calculate the length of the shortest path from one node to another.
* Weakly Connected: Determine whether a graph is weakly connected.

## 2.3 Graph Encoding Types

* Texting: Using well-known English first names as node encoding and texting as edge encoding.
* Commute: Using popular American cities as node encoding and traveling as edge encoding.
* Citation: Using well-known diverse last names as node encoding and citation as edge encoding.
* Adjacency: Using integer node encoding and parenthesis edge encoding.

# 3 Discussion
The Random Chain of Thought (CoT) method achieved the highest score, 59 points out of 100. This can likely be attributed to the nature of CoT reasoning, which better suits the LLM’s strengths in processing and generating textual content. While still highly effective, the Matched CoT method scored slightly lower than Random CoT, possibly due to the LLM overfitting to the particular reasoning patterns presented, leading to less flexibility in handling varied tasks. The randomness introduced in Random-CoT seems to mitigate potential biases or confusion, allowing for a more generalized understanding and learning. Few-Shot prompting demonstrated moderate effectiveness, outperforming Zero-Shot but lagging behind CoT methods. Providing a few examples helps the LLM understand the task better, but without the structured reasoning of CoT prompts, it does not reach the same level of performance. The Adjacency CoT method did not perform as well as expected, scoring below Few-Shot and other CoT methods, likely due to the reliance on numerical adjacency matrices, which are less intuitive for the LLM to interpret compared to textual data. The introduction of numbers instead of natural language text likely contributed to confusion and lower performance. As anticipated, Zero-Shot prompting scored the lowest, serving as the baseline for comparison. Without examples or structured reasoning to guide it, the LLM struggled to interpret and answer graph-related tasks, reflecting the inherent difficulty of the tasks without additional context.

The Texting encoding method achieved the highest average score, possibly because the use of alphabetized names helped the LLM in encoding and processing the graph information more effectively. Additionally, it is conceivable that GPT-3, being trained on a substantial corpus of social media data, finds this format familiar and easier to interpret. The Commute encoding method resulted in the lowest average score. The use of real city names may have introduced confusion for the LLM, as LLMs trained on factual information could have misinterpreted the context, reducing accuracy in solving the graph tasks. The Reachability and Cycle Check tasks received the highest scores, likely due to the structure of the graphs in the custom dataset, which were large and highly connected, often containing cycles. This high connectivity made it easier for the LLM to identify reachability and cycles, as many nodes were only one or two edges apart. Additionally, these tasks are binary (true/false), which inherently reduces the potential for error. Even with imperfect reasoning, the LLM had a higher chance of providing the correct answer. The regular presence of cycles and reachable nodes in the dataset provided consistent patterns for the LLM to recognize and learn from. Weakly connected components, while slightly lower in performance, likely benefited from the same factors.

# 4 Conclusion
This project initially aimed to identify specific methods that could enhance an LLM’s performance in graph-related tasks. From the results, it appears that ensuring consistency and clarity in prompts, particularly regarding graph properties such as "weighted and directed," is crucial. Contextually framed questions that cater to the LLM’s natural language processing strengths, as demonstrated in studies like Google’s, tend to perform better. This is illustrated by the performance in the Random-CoT method, which achieved the highest performance, underscoring the importance of leveraging the LLM’s strengths in textual processing.

Future research directions should focus on developing sophisticated prompting methods that align with the strengths of LLMs in textual processing. By emphasizing methods like Random CoT, which effectively leverage the LLM’s capabilities in understanding and reasoning about textual data, future studies can achieve more effective and interpretable outcomes in graph analysis tasks. Additionally, exploring the application of LLMs to more complex graph types, such as weighted and directed graphs, would provide valuable insights into their capabilities and limitations in handling diverse data formats. This aligns with the aim of extending previous works’ understanding to apply more broadly to real-world scenarios, where graphs are often weighted and directed. By addressing these aspects, future studies can build on the findings of this research to achieve more robust and accurate results.
