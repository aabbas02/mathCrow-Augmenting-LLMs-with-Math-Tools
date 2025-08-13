# mathCrow: Agentic AI for math and reasoning tasks

## Abstract

mathCrow is a proof-of-concept extension of ChemCrow [1] to math-based tasks. The mathCrow agent has access to two expertly designed tools and the ability to independently determine which tool to call to accomplish a given task. This framework provides greater autonomy than a human-based framework, where a human expert would parse the input prompt, decide which tool (function or software package) to call and preprocess the data according to the requirements of the selected tool. We provide an open-source/zero cost implementation of mathCrow using Meta’s llama3.3 model and Huggingface embeddings. We test our proposed mathCrow framework on text datasets derived from two research papers and with complex linear assignment problems (LAP). Our results show that mathCrow i) reduces hallucinations in LLM generated responses, and ii) increases autonomous task completion by formulating a precise linear assignment problem from a complex input prompt. Interestingly, our results also confirm that, for the reasoning-based LAP task, GPT-o reasoning models perform better than their general counterparts.

## Description

The MathCrow agent has access to two compnents, A) tools
and B) memory.

### A) Tools Description
#### Tool 1 Agentic-Retrieval Augmented Generation (RAG) Tool: 

First, we describe the difference between agentic RAG and RAG.
A thorough comparison between the two can also be found
at [9]. While both methods involve retrieving context from
an external vector database Fig. 5, agentic RAG, where recall
that the agent is essentially an LLM, rewrites the query before
searching for relevant context in the vector database 5. This
is crucial because user/input queries to the vector database
are often in the form of questions whereas the content of
the database is not. To rewrite the query, the agent uses the
description of the retrieval tool, which is a brief description
of the data/documents stored in the vector database.

#### Tool 2 Linear Assignment Problem (LAP) solver

The LAP solver tool is implemented by wrapping the ‘linear sum assignment’ function from the
‘scipy.optimize’ library as a tool. Wrapping a function as a
tool, which is possible using Langgraph, makes these functions
callable for the agent (or LLM). Langgraph also allows a
description of the of the function arguments so that the agent
can design these arguments appropriately when calling it.

### B) Memory/Vectorstore Description
The vector store is an external storage that contains the
dense embeddings of the text. A key design requirement
of the vector store is that it should allow a fast similarity
search of the stored text with the input query. There are
two widely used vector dataabaes: FAISS from Meta [8] and
Chroma [10]. It is important to note thats the input query
and the documents in the database are compared based off of
the numerical embeddings. This is unlike other word-based
frequency matching methods such as TF-IDF.


## Algorithm and LangGraph Implementation

We use LangGraph, which implements agentic frameworks using states, nodes and edges. States
are represented by a global variable, usually a list of strings.
The graph begins at the ‘start’ node with the state variable
equal to input query. The state is then passed from the start
node, through a sequence of nodes, to the ‘end’ node. The
state flow (transitioning between nodes) is controlled by edges.
Nodes and edges are both represented by python function.
Typically, nodes modify the state (by appending the list of
messages) and edges analyze, given the current state, the
next node to transition to. For a visual representation of the
mathCrow agentic framework, see the figure below.

![plot](./figures/problem_setup.png)

## Results


## References
1.  Andres M. Bran, Sam Cox, Oliver Schilter, Carlo Baldassari, Andrew D White, and Philippe Schwaller. Augmenting large language models with chemistry tools. Nature Machine Intelligence, 6(5):525–535, 2024.
