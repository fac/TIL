# Searching in Trello

## Keyboard Shortcuts

`/` puts the cursor in the search box

`b` opens the boards menu

`f` opens the card filter menu to search through cards on a single board

`q` toggles "cards assigned to me"

`x` clears all active card filters

## Finding an archived card

Menu -> More -> Archived Items

- opens a search box restricted to archived cards

## Search Operators

Combine these in any search/filter menu (including archive) for a power-search experience

-operator

- e.g. -has:members to search for cards without any members assigned

@name

- Returns cards assigned to a member. member: also works.
- @me will include only your cards.

label:

- Returns labeled cards. #label also works.

board:id

- Returns cards within a specific board.

board:name

- e.g “board:trello” returns cards on boards with trello in the board name.

list:name

- Returns cards within the list named “name”. Or whatever you type besides “name”.

has:attachments

- Returns cards with attachments.

has:description, has:cover, has:members, and has:stickers also work as you would expect.

due:day

- Returns cards due within 24 hours.

due:week

- returns cards that are due within the following 7 days.
- due:month, and due:overdue also work as expected.

due:14

- will include cards due in the next 14 days.

due:complete or due:incomplete

- for due dates that are marked as complete or incomplete.

created:day

- Returns cards created in the last 24 hours.
- created:week, created:month, created:14 also work as expected.

edited:day

- Returns cards edited in the last 24 hours.
- edited:week, edited:month, edited:21 also work as expected.

description:, checklist:, comment:, name:

- Return cards matching the text of card descriptions, checklists, comments, or names.
- comment:"FIX IT" will return cards with “FIX IT” in a comment.

is:open

- returns open cards.

is: archived

- returns archived cards.
- If neither is specified, Trello will return both types.

is:starred

- Only include cards on starred boards.


## Trello Tips Reference

<https://trello.com/b/QtjSVKOf/the-ultimate-board-of-trello-tips-tricks>
