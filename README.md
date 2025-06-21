# Programming-Capstone-University-of-MI-Ann-Arbor
Capstone: Retrieving, Processing, and Visualizing Data with Python University of Michigan
PageRank Capstone – Project Process Summary
As part of this capstone, I developed and executed a simplified version of a search engine indexing system using Python. The project involved three primary stages: crawling a subset of the web, analyzing link structure through PageRank, and visualizing the resulting network graph using D3.js. The entire system was implemented with a focus on modularity, persistence, and interpretability of results.

Crawling and Data Collection
I began by configuring and running a lightweight web crawler based on the code provided in pagerank.zip. The crawler is designed to systematically retrieve web pages starting from a seed URL. For each page fetched, it parses all anchor tags, extracts the linked URLs, and stores both the page content and link relationships in a local SQLite database.

The crawling logic follows a breadth-first traversal, queueing unretrieved URLs and marking each as processed after retrieval. I chose to limit the crawl to a single domain or subdomain to maintain scope control and data integrity. Additionally, the system is designed to avoid redundant retrievals and allows for restarts without data loss, enabling long-running or staged crawling sessions.

Link Analysis and PageRank Computation
Once a sufficient number of pages were collected, I initiated the PageRank calculation process. The underlying database schema maintains normalized tables of URLs and their interlinking structure, which serve as the basis for the iterative ranking algorithm.

The PageRank model assigns an initial rank (typically 1.0) to each page, then updates those values over successive iterations based on inbound link contributions. Pages with higher inbound links from already well-ranked sources progressively receive higher PageRank scores. The algorithm continues until the ranks converge to stable values, capturing a relative importance metric across the network.

This component of the system operates entirely on local data and is computationally lightweight. It can be reset or rerun multiple times, which proved useful during validation and tuning.

Visualization
For network visualization, I used the spjson.py script to export the top-ranked pages and their link relationships into a JSON structure compatible with D3.js. The accompanying HTML and JavaScript template renders a force-directed graph where node size correlates with PageRank. This interactive visualization provides an intuitive overview of the connectivity and relative authority of the pages within the crawled set.

The output effectively demonstrates the emergence of central nodes and link clusters, reflecting the underlying structure of the crawled web segment.

Conclusion
This capstone project highlights the end-to-end workflow of a basic search engine backend: from data acquisition through web crawling, to index analysis via PageRank, and final visualization using modern web technologies. While the implementation is intentionally minimalistic compared to production-grade systems, it captures the essential principles of search infrastructure, link analysis, and graph-based ranking in a reproducible and extensible form.

Let me know if you’d like this adapted into a resume bullet, case study, or slide deck format.








You said:
more-so case study please, since you ask.


ChatGPT said:
Great. Here is a formal case study version of your PageRank Capstone project, suitable for inclusion in a portfolio, technical presentation, or documentation for prospective collaborators or employers:

🗂 Case Study: PageRank Capstone – Web Crawling, Link Analysis, and Network Visualization
Project Overview
This project aimed to implement a streamlined version of a search engine backend, replicating the core functionalities of web crawling, index building, and ranking through link analysis. Using a custom Python-based crawler and a SQLite backend, I created a local web index that served as the foundation for computing PageRank values and visualizing page relationships via D3.js.

The capstone project was completed using code provided in pagerank.zip, which I extended and operated across several stages to explore network behavior at small scale and reinforce concepts in graph theory, data mining, and visual analytics.

Objectives
Build a persistent web crawler capable of navigating and storing web content from a given starting URL.

Construct a link graph representing the structure of the crawled domain.

Apply the PageRank algorithm to evaluate page importance based on link structure.

Export and visualize the resulting network with attention to node centrality and connectivity.

Technical Implementation
1. Crawling & Storage Layer
The initial phase involved configuring a crawler (spider.py) to traverse and collect content from a web domain (e.g., dr-chuck.com or a portion of Wikipedia). Each retrieved page was parsed for outbound links, and all URL relationships were logged into a SQLite database. The architecture supports resumable crawling sessions and avoids redundant page retrievals.

Key design considerations:

Persistent queueing of unretrieved links.

Page deduplication and retrieval status tracking.

Respect for crawl boundaries to prevent uncontrolled data expansion.

2. Link Graph Analysis & PageRank
Following data acquisition, I used sprank.py to compute PageRank scores for all indexed pages. The algorithm iteratively distributes rank values based on the number and quality of inbound links, with convergence reached after multiple passes over the dataset.

This process mirrors the importance propagation mechanism used in real-world search engines, albeit on a much smaller scale and with simplified damping and edge-weight handling.

Features:

Adjustable iteration depth for convergence tuning.

Reset functionality to restart ranking from uniform distribution.

Efficient in-memory operations due to local data access.

3. Visualization of Link Topology
To interpret the final PageRank scores and link network, I exported the top-ranking pages and their links to JSON using spjson.py. This data was rendered with a D3.js-based force.html visualization, which presented a dynamic graph of the network.

Visualization insights:

Node size represented PageRank magnitude.

Link directionality depicted navigational structure.

Drag-and-drop interaction enhanced exploratory analysis.

Results
The project successfully replicated a minimal search engine pipeline from crawl to rank to visualization. The D3.js output clearly illustrated central nodes with high inbound influence and peripheral nodes with minimal connectivity. Link density and circular paths became apparent as the crawler explored denser sites such as Wikipedia.

The PageRank algorithm demonstrated convergence behavior after approximately 20–30 iterations on sample datasets. Repeated runs confirmed stability and reproducibility of the computed ranks.

Tools & Technologies
Python: core implementation, parsing, and logic.

SQLite: persistent storage of page and link data.

D3.js: force-directed graph visualization.

HTML/JS: front-end rendering for interactive output.

Reflections
This project deepened my understanding of search engine architecture, data graph modeling, and the use of algorithms like PageRank for value attribution in networks. While scaled down, the system emulates real-world crawling and ranking logic, providing a strong foundation for further exploration into large-scale data mining, graph analytics, or distributed crawling systems.
