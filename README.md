# svelte fun learning example - Manga Chapter Reader

## A zipped manga chapter reader with intention of learning svelte.

### A zipped manga chapter reader for learning svelte. If you have zip file that contains a manga chapter, and file names starts with a common name and ends with page number(i.e: commonpart1.jpg,commonpart2.jpg,...etc), this project can read the zip file and prints the page as the given page numbers.

## Some Goals To Achieve For Manga Reader:
- [x]  Select a zip file and get file name and contents(using JSZip).
- [x]  Sort zip file contents according to manga page number at the end of file name. 
- [x]  Show manga chapter's pages according to page number.
- [ ]  Page Display mode settings.
  - [ ] Fit Width
  - [ ] Fit Height
  - [ ] Continious(For Manhuas which are one continious image through chapter)
  - [ ] 2 page view
  - [ ] Search, check and add any other good view modes
- [ ] Pagination (back, forward, go to Nth page)  
- [ ] Chapter page re-sorting, and downloading sorted chapter as new zip
- [ ] Open,select or fetch  zip files remotely(decide and update this later)
- [ ] Manga Listing
  - [ ] Manga entity(name, genre, etc... decide and update this later)
  - [ ] Manga searching( decide search type and mechanisms and update this later)
  - [ ] Paginated listing
  - [ ] Some new manga fetching ideas.
- [ ] User area
  - [ ] Authantication/Authorization mechanism (decide and update this later)
  - [ ] Manga Fav'ing ( decide and update this later)
  - [ ] Sharing custom manga lists.
  - [ ] Tracking mangas
  - [ ] Sub'bing mangas
  - [ ] User Types(reader, collaboration type(coordinator,raw provider,redrawer, translator, proofreader)
  - [ ] Translation teaming, team member selection, team supporting
  - [ ] Manga Translation Collaboration
    - [ ] CRUD of mangas/chapters/pages with some kind of confirmation mechanism
    - [ ] Realtime image editing/collaboration online (search for solutions)
    - [ ] Translate, redraw, proofreading feasability tests.
    - [ ] Reporting a work (sniping etc.)

## To run the project

```
npm install

npm run dev
```
