Simple VectorDB in C++ 
Hi!  I built this Vector Database from scratch in C++ to learn exactly how things like AI search, semantic similarity, and RAG (Retrieval-Augmented Generation) work under the hood.

I've been diving into C++ and Data Structures (like Trees and Graphs), so instead of just reading about them, I decided to build a real project. This database implements a few different search algorithms so you can actually compare how fast they are. It even has a simple web UI!

✨ What I Built
3 Search Algorithms: I implemented Brute Force, KD-Tree, and HNSW (the one the big production databases use!). You can run them side-by-side to see the speed difference.

Local AI Integration: It connects to Ollama so you can run embeddings and a local LLM entirely on your own machine.

Chat with Documents (RAG): You can upload text, the database will vectorize it, and you can ask an AI questions about your specific text.

Visualizer: A cool 2D scatter plot in the browser so you can literally see how similar concepts group together in vector space.

 How It Works (The Flow)
You give it some text.

It uses Ollama (nomic-embed-text) to turn that text into an array of numbers (a 768-dimensional vector).

My C++ engine stores that vector in a graph/tree structure.

When you search, it finds the nearest neighbors mathematically.

If you use the "Ask AI" feature, it passes those closest results to a local LLM (llama3.2) to answer your question!

How to Run It (Windows)
I built this on a Windows machine. If you want to try it out, here is how to get it running on yours!

1. You'll need a C++ Compiler (MSYS2)
If you don't have g++ installed, you can get it via MSYS2:

Download from msys2.org and install it.

Open the MSYS2 UCRT64 terminal and run these commands to update and install the compiler:

Bash
pacman -Syu
pacman -S mingw-w64-ucrt-x86_64-gcc

3. Make sure to add `C:\msys64\ucrt64\bin` to your Windows Environment `Path` variables!

### 2. Install Ollama (For the AI)
1. Download Ollama from [ollama.com](https://ollama.com).
2. Open PowerShell and download the two models we need:
   ```powershell
   ollama pull nomic-embed-text
   ollama pull llama3.2
3. Clone & Compile
Open your terminal, clone this repo, and navigate into the folder. Then, compile the C++ code:

PowerShell
g++ -std=c++17 -O2 main.cpp -o db -lws2_32
(This will create a db.exe file. It usually takes about 10-20 seconds).

4. Start the Engine!
Make sure Ollama is running in the background (ollama serve). Then, start the database server:

PowerShell
.\db.exe
Open your web browser and go to: http://localhost:8080 

 What I Learned About the Algorithms
Building this helped me understand why different data structures matter:

Brute Force: Super simple. It just checks the distance between your search and every single item in the database. It is 100% accurate, but really slow when you have a lot of data.

KD-Tree: This is a cool binary tree concept that splits data into different dimensions. It's super fast for small dimensions, but I learned it actually slows down a lot when you hit high dimensions (like the 768D vectors from the AI).

HNSW (Hierarchical Navigable Small World): This was the hardest but coolest part. It builds layers of graphs, kind of like highway systems. You take the fast highway at the top layers to get close to your target, then exit to the local streets on the bottom layers to find the exact match. It's incredibly fast!

***********************************
 Troubleshooting
g++: command not found: Double-check that your Windows PATH variable includes the MSYS2 bin folder, and restart your terminal!

AI is typing really slowly: llama3.2 can be heavy on a laptop. You can change it to a smaller model by running ollama pull llama3.2:1b, updating the genModel string inside main.cpp, and recompiling!



Feel free to explore the code! I'm still learning and growing as a developer, so I'd love any feedback or advice on how to improve it.