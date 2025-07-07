Capstone: Retrieving, Processing, and Visualizing Data with Python University of Michigan PageRank Capstone – Project Process Summary

🗂 Case Study: PageRank Capstone – Web Crawling, Link Analysis, and Network Visualization Project Overview This project aimed to implement a streamlined version of a search engine backend, replicating the core functionalities of web crawling, index building, and ranking through link analysis. Using a custom Python-based crawler and a SQLite backend, I created a local web index that served as the foundation for computing PageRank values and visualizing page relationships via D3.js.

The capstone project was completed using code provided in pagerank.zip, which I extended and operated across several stages to explore network behavior at small scale and reinforce concepts in graph theory, data mining, and visual analytics.

Objectives:
-Build a persistent web crawler capable of navigating and storing web content from a given starting URL.

-Construct a link graph representing the structure of the crawled domain.

-Apply the PageRank algorithm to evaluate page importance based on link structure.

-Export and visualize the resulting network with attention to node centrality and connectivity.

-Technical Implementation

Crawling & Storage Layer:


The initial phase involved configuring a crawler (spider.py) to traverse and collect content from a web domain (e.g., dr-chuck.com or a portion of Wikipedia). Each retrieved page was parsed for outbound links, and all URL relationships were logged into a SQLite database. The architecture supports resumable crawling sessions and avoids redundant page retrievals.


Key design considerations:

-Persistent queueing of unretrieved links.

-Page deduplication and retrieval status tracking.

-Respect for crawl boundaries to prevent uncontrolled data expansion.

Link Graph Analysis & PageRank:


 Following data acquisition, I used sprank.py to compute PageRank scores for all indexed pages. The algorithm iteratively distributes rank values based on the number and quality of inbound links, with convergence reached after multiple passes over the dataset.
This process mirrors the importance propagation mechanism used in real-world search engines, albeit on a much smaller scale and with simplified damping and edge-weight handling.

Features:

Adjustable iteration depth for convergence tuning.

Reset functionality to restart ranking from uniform distribution.

Efficient in-memory operations due to local data access.

Visualization of Link Topology:


To interpret the final PageRank scores and link network, I exported the top-ranking pages and their links to JSON using spjson.py. This data was rendered with a D3.js-based force.html visualization, which presented a dynamic graph of the network.
Visualization insights:



-Node size represented PageRank magnitude.

-Link directionality depicted navigational structure.

-Drag-and-drop interaction enhanced exploratory analysis.


Results:


 The project successfully replicated a minimal search engine pipeline from crawl to rank to visualization. The D3.js output clearly illustrated central nodes with high inbound influence and peripheral nodes with minimal connectivity. Link density and circular paths became apparent as the crawler explored denser sites such as Wikipedia.

The PageRank algorithm demonstrated convergence behavior after approximately 20–30 iterations on sample datasets. Repeated runs confirmed stability and reproducibility of the computed ranks.

Tools & Technologies Python: core implementation, parsing, and logic.

SQLite: persistent storage of page and link data.

D3.js: force-directed graph visualization.

HTML/JS: front-end rendering for interactive output.


Reflections:


 This project deepened my understanding of search engine architecture, data graph modeling, and the use of algorithms like PageRank for value attribution in networks. While scaled down, the system emulates real-world crawling and ranking logic, providing a strong foundation for further exploration into large-scale data mining, graph analytics, or distributed crawling systems.


________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

Sprank.py Stage Notes:

After running 12 iterations, I observe that the difference between the old and new page ranks has significantly decreased. This reduction is due to the convergence of the ranks, where the average difference now falls below 0.005. To illustrate this stabilization more clearly, I decide to execute one additional iteration. Upon doing so, I confirm that the rank values are beginning to stabilize.

Assuming the role of a search engine like Google, I proceed to execute python3 spider.py to simulate ranking behavior on an extended dataset. I opt to crawl ten additional pages, expecting that these newly introduced pages will initially be assigned a default page rank of 1.

After completing the crawl, I exit and refresh the data view to inspect the updated new ranks, verifying the impact of the additional pages on the overall distribution.
________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

SPJson and SPdumping Stage Notes:

After initializing the crawl and computing page ranks, I chose not to reset the algorithm using spreset.py, opting instead to move directly into data extraction and visualization—the more insightful part of the process. I began with spdump.py, a straightforward helper script that executes a SQL query against the local SQLite database. The goal here was to list the top 10 most-linked pages by ordering them in descending count of inbound links. Running this gave me a quick validation of the structure and content of my collected data, with my blog appearing at the top of the list, confirming the page link logic was functioning as expected.

Once the data check was complete, I transitioned into the visualization phase using spjson.py. This script performs a SQL join to collect all relevant link information, filtered to exclude rows with null HTML or error values, and ordered by the number of inbound links. From this, I extracted the top-ranked entries—typically the top 20 pages—along with their page rank values. Given that the page rank values can vary widely (ranging from near-zero to 20 or more), I normalized the data by subtracting the minimum rank and adjusting it proportionally. This normalized value was used to determine both the line thickness of the graph edges and the size of the node circles in the visualization.

The script then wrote this information into a JavaScript file, spider.js, defining node and edge objects. Each node includes an identifier, weight (used to scale the circle size), and associated rank, while each edge encodes link directionality and visual weight. This file was then consumed by force.html, which integrates with the D3.js visualization library. D3 rendered the graph dynamically, with node size reflecting page rank and link thickness indicating relative influence.

Finally, I opened force.html in a browser. The result was an interactive, force-directed graph that allowed for intuitive exploration of the crawled web structure. By hovering and dragging nodes, I could easily identify central pages and their relative importance within the local crawl. The entire process not only provided validation for the underlying page rank computations but also offered a clear, visual representation of link structure density and node significance.
