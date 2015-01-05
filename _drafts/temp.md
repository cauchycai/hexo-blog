# Searching and Replacement #

## Basics of Incremental Search ##

1. C-s (isearch-forward)

2. C-r (isearch-backward)

3. When you are satisfied with the place you have reached, type RET, this stops searching, leaving the cursor where the search brought it.

4. When you exit the invremental search, *it adds the original value of point to the mark ring*, without activating the mark; you can thus use C-u C-SPC to return to where you were before beginning the search.

5. After exiting a search, you can search for the same string again by typing just C-s C-s

6. To *reuse earlier search strings*, use the search ring. The commands M-p and M-n move through the ring to pick a search string to reuse.

7. *M-e* to edit the current search string in the minibuffer.
