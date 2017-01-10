# TA98 (plus wikipedia) to sqlite parser

This repository contains python scripts to parse the HTML representation of the 
English tree view of Terminologia Anatomica 1998 on-line version found at 
http://www.unifr.ch/ifaa/Public/EntryPage/TA98%20Tree/Alpha/All%20KWIC%20EN.htm

Terminologia Anatomica is a standard for naming anatomical structures in the human body. 
It was ratified by the International Federation of Associations of Anatomists and 
maintained by the University of Fribourg (Switzerland). Please see their site 
(http://www.unifr.ch/ifaa/) for more information.

The respository contains the following subdirectories:
 - `src`: python parsing and database creation code
  * `ta98.py`: HTML parser for TA98 web pages based on BeautifulSoup 4
  * `buildta98db.py`: uses ta98.py to build main sqlite db given a list of HTML pages.  
  You may have to break up the pages into groups to deal with UNIX shell/command line
  limitations (do 0* files and [1-9]* files separately with the same database file).
  * `ta98wikipedia.py`: builds the TA98 to wikipedia table
  * `wikipediainfo.py`: looks up all the table entries generated by ta98wikipedia.py and
  stores wikipedia page info for those pages.
  
 - `ta98-web-src`: crawled copy of the TA98 web site
 - `db`: precompiled sqlite databases
 
 In the `db` directory, the following databases and tables are interesting:
 - `ta98.sqlite`: contains these tables describing TA98 structures
  * `_`: information about each TA98 entry (one row per entry)
  * `synonyms`: all synonyms for each TA98 entry (one row per synonym)
  * `notes`:  notes for each TA98 entry.
  * `hierarchy`: the ancestors of each TA98 entry (one row per ancestor)
  * `fma_names`: mapping of FMA IDs to FMA names
 - `ta98wikipedia.sqlite`: wikipedia information about TA98 terms
  * `_`: mapping from TA IDs to wikipedia titles (one row per title)
  * `page_info`: Information about wikipedia pages, including title, URL, images, and summary.
