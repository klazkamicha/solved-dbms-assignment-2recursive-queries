Download Link: https://assignmentchef.com/product/solved-dbms-assignment-2recursive-queries
<br>
<ol>

 <li>Please complete this assignment <em>individually</em>.</li>

 <li>You will submit just 1 file: query.sql.</li>

 <li>Use PostgreSQL 13 for your homework. See <a href="https://www.postgresql.org/download/">this link</a> for instructions on how to download and install it on your OS. The .sql files are run automatically using the psql command using the i option, so please ensure that there are no syntax errors in the file. <em>If we are unable to run your file, you get an automatic reduction to 0 marks.</em></li>

</ol>

To understand how to run many queries at once from text file, a dummy query file <a href="https://drive.google.com/file/d/1IH8zYTSiEYQFZZRnUF20RE_zouapPuon/view">example.sql</a> is available. To run <a href="https://drive.google.com/file/d/1IH8zYTSiEYQFZZRnUF20RE_zouapPuon/view">example.sql</a> in PostgreSQL, type the following command in the terminal: sudo -u postgres psql <em>dbname</em>

i /address/to/example.sql

This command will run all the queries listed in <a href="https://drive.google.com/file/d/1IH8zYTSiEYQFZZRnUF20RE_zouapPuon/view">example.sql</a> at once.

<ol start="4">

 <li>The format of the file should be as follows. You can have a preamble where you may create views if you like (please note that no procedures are allowed (this has to be pure SQL), and correspondingly have a cleanup section where these views are removed. One line should identify the query number (note the two hyphens before and after the query number), followed by the actual, syntactically correct SQL query. Leave a blank line after each query.

  <ul>

   <li>-PREAMBLE- OPTIONAL DEFINITIONS</li>

   <li>-1- –</li>

  </ul></li>

</ol>

SQL QUERY

<ul>

 <li>-2- –</li>

</ul>

SQL QUERY

<ul>

 <li>-3- –</li>

</ul>

SQL QUERY

<ul>

 <li>-CLEANUP- –</li>

</ul>

CLEANUP EVERYTHING YOU CREATED HERE

<ol start="5">

 <li>Some of the queries below require an ’ORDER BY’ clause. If you made an error in this clause, your answer may be evaluated as incorrect, giving you zero marks for that query.</li>

 <li>The submission will be done on Moodle. No changes are allowed in attribute names or table names.</li>

 <li>If unspecified, order in ascending order by column 1, then column 2 .. etc. In case of any doubts please ask on Piazza. The instructors ordering will be final and no queries will be entertained on the same.</li>

 <li>There are no NULL values in the dataset, so you need not worry about that.</li>

 <li>There is no data provided for these queries. For testing, make your own dataset. The .sql file that you submit however, should contain only queries</li>

 <li>If any query asks you to output top <em>x </em>rows and you are getting <em>y </em>rows, output <em>min</em>(<em>x,y</em>)</li>

 <li>You are allowed to submit the assignment one day late with a penalty of 25% of assignment marks.</li>

</ol>

<h1>1        Dataset 1</h1>

<ol>

 <li>In this first part of the assignment, you’ll work with a real world Flights and Airports dataset. The schema of the same is described below, but we won’t share the actual dataset that will be used for evaluation.</li>

 <li>The database will include following two tables and you should use only these tables while writing solution of the queries. You can create temporary views while handling any SQL query but you should include SQL queries for creating and deleting these temporary views at the starting and end of your SQL file respectively. Note – you don’t have to define these tables in the submission file, these will already be present while evaluation.

  <ul>

   <li>airports</li>

  </ul></li>

</ol>

<table width="361">

 <tbody>

  <tr>

   <td width="121">airportid : integer</td>

   <td width="75">city : text</td>

   <td width="81">state : text</td>

   <td width="84">name : text</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>flights</li>

</ul>

<table width="585">

 <tbody>

  <tr>

   <td width="138">flightid : integer</td>

   <td width="154">originairportid : integer</td>

   <td width="156">destairportid : integer</td>

   <td width="137">carrier : text</td>

  </tr>

  <tr>

   <td width="138">dayofmonth : integer</td>

   <td width="154">dayofweek : integer</td>

   <td width="156">departuredelay : integer</td>

   <td width="137">arrivaldelay : integer</td>

  </tr>

 </tbody>

</table>

<ol start="3">

 <li>Keys:

  <ul>

   <li>airportid is primary key for airports table</li>

   <li>flightid is primary key for flights table</li>

  </ul></li>

 <li>Flight f is a direct flight between airports A and B if there exists a flight f in flights table such that</li>

</ol>

f.originairportid = A, f.destairportid = B

<ol start="5">

 <li>Airports a and b are said to be connected via a series of connecting flights if there exist a sequence of flights f0, f1, … , fn: each a direct flight between (a, a1), (a1, a2), (a2, a3), …, (an, b) respectively.</li>

 <li>Note that in the airports table, a city can potentially have multiple airports. If we want you to consider a particular airport for a city, we will mention the airportid.</li>

 <li>In flights table, the dayofmonth represents the calendar date of the month and lies in the range [1<em>,</em>31] In flights table, the dayofweek represents the enumerated index of the days of week (Sunday, Monday … Saturday) and lies in the range [1<em>,</em>7]</li>

 <li>In flights table, the arrivaldelay and departuredelay represents the numeric value of the delay (in minutes) where a negative value of delay signifies the flight was early. For eg: departuredelay = -10 will signify the flight departed 10 minutes early.</li>

</ol>

<h1>2        Queries</h1>

<a href="https://en.wikipedia.org/wiki/Air_Transport_Network">Air Transport Network</a> is an example of transport networks and spatial networks. The nodes of the network are the airports and the links represent direct flight routes between two airports. Alternatively, cities can be considered as the nodes with links representing direct flight connection between them. Air transport networks can be defined worldwide as well as for one region or for one airline company; the scale of the network can be global or domestic

Consider the collaboration network <em>G </em>formed by the airports and flights tables. The nodes for this graph will be the airports, and there will exist a directed edge from airport A to B iff there is a flight from A to B. There is an edge from airport A to B are if there exists a direct flight between A and B.

Mathematically, <em>G </em>= (<em>V,E</em>) where:

<ul>

 <li><em>V </em>= {airportid}</li>

 <li><em>E </em>= {(<em>u,v</em>) : ∃ f in flights s.t. f.originairportid = u and f.destairportid = v }</li>

</ul>

<ol>

 <li>Find all cities reachable from Albuquerque (airportid: 10140) through a series of one or more connecting flights by the same carrier.</li>

</ol>

Output column: name. Sort output by name in ascending order.

<ol start="2">

 <li>Find all cities reachable from Albuquerque (airportid: 10140) through a series of one or more connecting flights, with all connecting flights operating on the same day of the week.</li>

</ol>

Output column: name. Sort output by name in ascending order.

<ol start="3">

 <li>Find all the cities reachable from Albuquerque (airportid: 10140) by exactly one path, ie list all cities ‘c’ such that there is exactly one path from Albuquerque to ‘c’.</li>

</ol>

Output column: name. Sort output by name in ascending order.

<ol start="4">

 <li>Find the length of the longest possible circular trip containing Albuquerque (airportid: 10140) through a series of one or more connecting flights. “Longest” here is defined by the number of stops (or the number of cities).</li>

</ol>

Output column: length.

<ol start="5">

 <li>Find the length of the longest possible circular trip through a series of one or more connecting flights. “Longest” here is defined by the number of stops (or the number of cities).</li>

</ol>

Output column: length.

<ol start="6">

 <li>Given a source city (Albuquerque) and a destination city (Chicago) return the number of paths between these two cities through interstate flights. Interstate means the state of the source city should be different than the state of the destination.</li>

</ol>

Output column: count.

<ol start="7">

 <li>Given a source city (Albuquerque) and a destination city (Chicago) return the number of paths between these two cities which also pass through Washington.</li>

</ol>

Output column: count.

<ol start="8">

 <li>Find all the pairs of cities (c1, c2) such that there is no path from c1 to c2.</li>

</ol>

Output columns: (name1, name2). Sort your output based on the first column in ascending order. Resolve ties using the second column.

<ol start="9">

 <li>When taking a flight from Albuquerque, output days of the Month when you will face the least amount of delays. Delays here means the sum of arrival delay and departure delay.</li>

</ol>

Output column: day. Sort output of days of the month based on the increasing amount of delays. If 2 days have the same delay, then order by date.

<ol start="10">

 <li>Find all the cities in the State of “New York” which act as a travel center for the state, i.e. all the cities in the state can be visited via that city through direct flights.</li>

</ol>

Output column: name. Sort output by name in ascending order.

<ol start="11">

 <li>Find all the pairs of cities (c1, c2) such that there is a path from c1 to c2, such that successive delay times between the consecutive cities is in increasing order (delay time here is the sum of arrival and departure delays).</li>

</ol>

Output columns: (name1, name2). Sort your output based on the first column.

<h1>3        Dataset 2</h1>

<ol>

 <li>In this second part of the assignment, you’ll work with a synthetically generated dataset. The schema of the same is described below, but we won’t share the actual dataset that will be used for evaluation.</li>

 <li>The database will include following four tables and you should use only these tables while writing solution of the queries. You can create temporary views while handling any SQL query but you should include SQL queries for creating and deleting these temporary views at the starting and end of your SQL file respectively. Note – you don’t have to define these tables in the submission file, these will already be present while evaluation.

  <ul>

   <li>authordetails</li>

  </ul></li>

</ol>

<table width="496">

 <tbody>

  <tr>

   <td width="119">authorid : integer</td>

   <td width="123">authorname : text</td>

   <td width="75">city : text</td>

   <td width="92">gender : text</td>

   <td width="89">age : integer</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>paperdetails</li>

</ul>

<table width="473">

 <tbody>

  <tr>

   <td width="113">paperid : integer</td>

   <td width="117">papername : text</td>

   <td width="144">conferencename : text</td>

   <td width="98">score : integer</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>authorpaperlist</li>

</ul>

<table width="232">

 <tbody>

  <tr>

   <td width="119">authorid : integer</td>

   <td width="113">paperid : integer</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>citationlist</li>

</ul>

<table width="240">

 <tbody>

  <tr>

   <td width="120">paperid1 : integer</td>

   <td width="120">paperid2 : integer</td>

  </tr>

 </tbody>

</table>

<ol start="3">

 <li>Keys:

  <ul>

   <li>authorid is primary key for authordetails table</li>

   <li>paperid is primary key for paperdetails table</li>

   <li>(authorid, paperid) is primary key for authorpaperlist table</li>

   <li>(paperid1, paperid2) is primary key for citationlist table</li>

  </ul></li>

 <li>Authors a and b are connected by an edge if there exists a paper with paperid p such that (<sub>a, p) </sub>∈ authorpaperlist and (b, p) ∈</li>

 <li>Authors a and b are connected if there exist a sequence of authors a1, a2, … , an such that there is an edge between (a, a1), (a1, a2), (a2, a3), …, (an, b).</li>

 <li>A paper with paperid p cites a paper with paperid c if (p, c) ∈ citationlist</li>

 <li>(p, c) is treated as an direct citation if (p, c) ∈</li>

 <li>(<sub>p, c) </sub>is treated as an indirect citation if there exist a sequence of papers with paperids p1, p2, … ,</li>

</ol>

pn such that (p, p1), (p1, p2), (p2, p3), …, (pn, c) ∈ citationlist.

<h1>4        Queries</h1>

<a href="https://en.wikipedia.org/wiki/Scientific_collaboration_network">Scientific collaboration network</a> is a social network where nodes are scientists and links are co-authorships as the latter is one of the most well documented forms of scientific collaboration.It is an undirected, scalefree network where the degree distribution follows a power law with an exponential cutoff – most authors are sparsely connected while a few authors are intensively connected

Consider the collaboration network <em>G </em>formed by the authorpaperlist and authordetails and paperdetails tables. The nodes for this graph will be the authors, and there will exist an edge between them iff they have co-authored a paper. Two authors are connected by an edge if there exist a paper p auch that (author1, p),

(author2, p) is present in citationlist table. In the queries that follow, “components” refer to the usual components in a graph.

Mathematically, <em>G </em>= (<em>V,E</em>) where:

<ul>

 <li><em>V </em>= {authorid}</li>

 <li><em>E </em>= {(<em>u,v,p</em>) : (<em>u,p</em>) ∈ authorpaperlist and (<em>v,p</em>) ∈ authorpaperlist;<em>p </em>∈ paperid;<em>u,v </em>∈ authordetails.authorid}</li>

</ul>

<ol start="12">

 <li>Find the length of shortest path from author A to every other author in G. If the shortest path goes like: A → <em>a</em><sub>1 </sub>→ <em>a</em><sub>2 </sub>→ ··· → <em>a<sub>n </sub></em>→ B, output <em>n </em>+ 1. If there is no path from author A to some author, output -1. Give the author id, length of shortest path from author A. Sort in descending order of length of shortest path and resolve all ties by ascending order of destination authorid.</li>

</ol>

Output columns: authorid, length. Take A = 1235

<ol start="13">

 <li>Find the number of paths in Graph G from author A to B such that all authors on the path have an age more than 35 and consecutive authors on the path have different genders. Return -1 if they don’t belong to the same component, else return number of paths.</li>

</ol>

Output column: count. Take A = 1558, B = 2826.

<ol start="14">

 <li>Find the number of paths from A to B in <em>G </em>such that at least one person on the path has directly or indirectly cited a paper with paperid p. Return -1 if they don’t belong to the same component, else return number of paths. Output column: count. Take A = 704, B = 102, p=126</li>

 <li>Find the number of paths in graph <em>G </em>from author A to B such that the total number of citations of authors on the path is in strictly increasing order or strictly decreasing order. The total number of citations of an author is defined as the sum of citations of papers that the author is associated with. Return -1 if they don’t belong to the same component, else return number of paths.</li>

</ol>

Output column: count. Take A = 1745, B = 456

<ol start="16">

 <li>We define “number of future collaborations of a author A” as authors whose papers has been cited by author A and haven’t co-authored a paper with author A. Give the author ids of top 10 people with most number of future collaborations. Sort in descending order of number of future collaborations and resolve all ties by ascending order of author ids. Output column: authorid</li>

 <li>Author A’s third degree connections are people connected to him with shortest path length of 3 in graph <em>G</em>. Give the author ids of top 10 authors with the most number of citations of papers written by their third degree connections. Sort in descending order of number of citations and resolve all ties by ascending order of user ids. Output column: authorid</li>

 <li>Find the number of paths in Graph G from author A and B that also pass through at least one of the authors C1, C2, C3. Note that A → <em>a</em><sub>1 </sub>→ <em>C </em>→ <em>a</em><sub>2 </sub>→ B and A → <em>a</em><sub>1 </sub>→ <em>C </em>→ <em>a</em><sub>3 </sub>→ B constitute two distinct paths in graph <em>G</em>, that is, in path from A to B (via C), if even a single node is different (may be in A→C part or in C→B part), then it counts as a different path. All the vertices in the path <em>A </em>→ <em>C </em>should be distinct, that is, a path like <em>A </em>→ ···<em>a</em><sub>1 </sub>→ ···<em>B </em>→ ···<em>a</em><sub>1 </sub>→ ···<em>C </em>is not valid. Return -1 if they don’t belong to the same component.</li>

</ol>

Output column: count. Take A = 3552, B = 321, C1 = 1436, C2 = 562, C3=921

<ol start="19">

 <li>Find the number of paths in Graph <em>G </em>from author A to B such that no two authors on the path are from the same city and no two persons have directly cited each other’s papers. Return -1 if they don’t belong to the same component, else return number of paths.</li>

</ol>

Output column: count. Take A = 3552, B = 321

<ol start="20">

 <li>Find the number of paths in Graph <em>G </em>from author A to B such that any author on the path hasn’t directly or indirectly cited any other author on that path. Return -1 if they don’t belong to the same component, else return number of paths. Output column: count. Take A = 3552, B = 321</li>

 <li>We say “authors A and B are conference(X)-connected” if there exists a path from author A to B in G where all the edges on the path correspond to papers published in conference X. A conference connected component is a subgraph(H) of G where every pair of vertices in H are conference-connected. For every conference X, find total number of conference(X) connected components in <em>G</em>. Sort in descending order of conference connected components and resolve all ties by ascending order of conferencename.</li>

</ol>

Output columns: conferencename, count

<ol start="22">

 <li>For each conference, give the conferencename, number of authors in each conference connected component of <em>G</em>. If a conference has three connected components then the output should have three rows with the conference name and the number of authors in each component. Sort in ascending order of number of authors and resolve all ties by ascending order of conferencename.</li>

</ol>

Output columns: conferencename, count