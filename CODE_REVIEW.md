***Are there any problems or code smells in the app? (Focus on code in the `libs/books` folder)***
1. I can see memory leak and performance issue, as Observable used for `this.store.select(getAllBooks)` is not unsubscribed in `book-search.component.ts` file.
    - Added async pipe in 'book-search.component.html' , which will automatically unsubscribe the observable as soon as component is destroyed. 
2. For `book-search.component.html` custom method `formateDate()` has been used for date format at line#45. 
    - We can make use of pipe instead of `formateDate()` method to convert date into required format.  A Function will be triggered everytime on change detection whereas a pipe would be evaluated for the expression only once. This will help in performance improvement.
3. Actions - `addToReadingList` & `removeFromReadingList` - in `reading-list.reducer.ts` file triggers the effects to invoke Backend API to add & remove book to & from reading list and at the same time its updating the state by reducer without checking success or failure of backend APIs.
    - Modified the code to update the store only on success action `confirmedAddToReadingList` & `confirmedRemoveFromReadingList`
4. Naming convention is not proper in `book-search.component.html` at line#33.
    - Corrected naming convention in `book-search.component.html`. Renamed 'b' to 'books'.
5. Corrected mobile view to provide better user experience. Mobile UX was not correctly rendered. Book sections, reading list and buttons were overlapping. 
6. Corrected Test cases for reading-list reducer . `failedAddToReadingList` and `failedRemoveFromReadingList` were not implemented in reducer.
7. Added type notation in `reading-List.component.ts` & `reading-list.reducer.ts` for below functions.
    - addBookToReadingList
    - searchExample
    - searchBooks
    - removeFromReadingList


***Are there other improvements you would make to the app? What are they and why?***
1. For better user experience of search API , Spinner should be implemented . `Implemented`
2. Code should be updated to display proper error message , as Error handling is not proper for the API failure scenario. It should display error message when there is a failure . `Implemented`
3. Used `ChangeDetectionStrategy.OnPush` in `book-search.component.html` since we don't change the state of the objects in component. It will perform better rather than default where each change of the object makes run change detector to resolve changes.

***Accessibility***
- **Ran authomated scan using light house and corrected issues.**
  - Issue1- Buttons do not have an accessible name. `FIXED`
  - Issue2 - Contrast ratio is not sufficient for Background and foreground . `FIXED`


- **Manually checked using NVDA Accessiblity tool**
  - Search icon was pronounced as button. Added `aria-label` to make this more meaningful for the user. `FIXED`
  - Reading `Reading List` along with header on focus was not moving correctly. `FIXED`
  - Changed Background color of Reading list button to pink-dark color to make it visible to the user. It was same as header . `FIXED`
  - Alt attribute is missing in `reading-list.component.html` for image tag at line#4. Screen reader may announce the file name and path instead of proper content of image.Added `alt=""` in image tag. `FIXED`
  - `aria-live="assertive"` has been added in book-search.component.html file at line#20 so that Screen reader should give priority to read error message.
  
- `Javascript` is wrapped in anchor tag in `book-search.component.html` even this is not being used for redirection. Changed it to button element. `FIXED`
- Added aria-label for `Want to read` button to make it read with book name. `FIXED`