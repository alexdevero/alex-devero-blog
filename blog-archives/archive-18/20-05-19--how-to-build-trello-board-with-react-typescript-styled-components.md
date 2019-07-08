# How to Build Trello [Board] with React, TypeScript & Styled-components

Have you ever wanted to create a Trello-like board with drag & drop functionality? Well, it is actually easier than you may think. This tutorial will show you how to do it, using React, TypeScript and styled-components. Learn all you need to build your own Trello-like board in just a few minutes.<!--more-->
<!--
Table of Contents:
## Preparing React app
## Adding board data
## Creating the board item
## Creating the board column
## Creating the board
## Building the page component
## Epilogue: How to build Trello board with React, TypeScript & styled-components
-->

## Preparing React app

In order to make it easier, let's use the `create-react-app` to provide us with all files we will need to get started. If you have this package installed on your machine use that. If not, and you don't want to install it, you can use [npx]. This will allow you to use the `create-react-app` package without installing it on your machine.

Using `npx` is similar to using `npm` command to install npm packages. You just replace `npm` with `npx` the rest is the same. One important thing, we will use [TypeScript] in this tutorial. So, make sure to include the `--typescript` when you use `create-react-app`. The whole command will be `npx create-react-app board-app --typescript`.

When `create-react-app` is done we will need to add some additional packages. The first one is `styled-components`. We will use this library for styling the board app. The second is `react-beautiful-dnd`. This library will provide the drag & drop functionality for our board s we can move board items between board columns, or cards. Like in Trello.

We should also add type definitions for these two libraries. With this, TypeScript will provide us with suggestions and type checking for these two libraries. This will result in faster and easier work and also in safer code. So, `yarn add -D @types/react-beautiful-dnd @types/styled-components` or `npm i @types/react-beautiful-dnd @types/styled-components --save`.

```
///
// package.json (part)
///
  ...
  "dependencies": {
    "react": "^16.8.6",
    "react-beautiful-dnd": "^11.0.3",
    "react-dom": "^16.8.6",
    "styled-components": "^4.2.0"
  },
  "devDependencies": {
    "@types/jest": "24.0.13",
    "@types/node": "12.0.2",
    "@types/react": "16.8.17",
    "@types/react-beautiful-dnd": "^11.0.2",
    "@types/react-dom": "16.8.4",
    "@types/styled-components": "^4.1.15",
    "react-scripts": "3.0.1",
    "typescript": "3.4.5"
  }
  ...
```

The last thing. The template generated by `create-react-app` contains some files we will not use in this tutorial. The only file we will use directly will be `index.tsx`. Then, we will create components for the board: `board-column.tsx`, `board-item.tsx`, `board.tsx` and `board-initial-data.ts` containing data displayed on boards. The folder structure will be following:

```
board-app/
├─node_modules
├─public
│ ├─favicon.ico
│ ├─index.html
│ └─manifest.json
├─src
│ ├─components
│ │ └─board-column.tsx
│ │ └─board-item.tsx
│ │ └─board.tsx
│ ├─data
│ │ └─board-initial-data.ts
│ ├─index.tsx
│ └─react-app-env.d.ts
└─ package.json
└─ tsconfig.json
```

## Adding board data

The second step, after customizing the `create-react-app` template, is adding some content for our board. We could do this in the `Board` component we will create. However, that could lead to code that is harder to read and use. Especially if you add more boards or items for board columns. Using a separate file will help keep the code cleaner.

We will store the data for our board as an object with three keys: `items`, `columns` and `columnsOrder`. The value of `items` will be another object containing individual board items. Each item will have two keys: `id` and `content`. The `id` is necessary for drag & drop. Value of `content` key will be what will be displayed on the board.

The value of `columns` key will be also an object. It will contain data for all columns. Each column will have `id`, `title` and `itemsIds`. The `id` is for drag & drop. The `title` will be the column heading displayed on our board. The `itemsIds` will be an array containing ids for board items inside specific column.

As a starting condition, we will put all items inside the first column. This means that we will take all ids specified in the `items` object and put them here. Make sure to use correct value of `id` key for each item. Lastly, `columnsOrder` will determine in which order we will display the columns on our board.

```
///
// src/data/board-initial-data.ts
///
export const initialBoardData = {
  items: {
    'item-1': { id: 'item-1', content: 'Content of item 1.'},
    'item-2': { id: 'item-2', content: 'Content of item 2.'},
    'item-3': { id: 'item-3', content: 'Content of item 3.'},
    'item-4': { id: 'item-4', content: 'Content of item 4.'},
    'item-5': { id: 'item-5', content: 'Content of item 5.'},
    'item-6': { id: 'item-6', content: 'Content of item 6.'},
    'item-7': { id: 'item-7', content: 'Content of item 7.'}
  },
  columns: {
    'column-1': {
      id: 'column-1',
      title: 'Column 1',
      itemsIds: ['item-1', 'item-2', 'item-3', 'item-4', 'item-5', 'item-6', 'item-7']
    },
    'column-2': {
      id: 'column-2',
      title: 'Column 2',
      itemsIds: []
    },
    'column-3': {
      id: 'column-3',
      title: 'Column 3',
      itemsIds: []
    },
    'column-4': {
      id: 'column-4',
      title: 'Column 4',
      itemsIds: []
    }
  },
  columnsOrder: ['column-1', 'column-2', 'column-3', 'column-4']
}
```

## Creating the board item

Now, when we have the data for our board ready, let's create the component for board item. Put simply, board items will represent individual items, like to-dos, displayed in columns or cards. The structure will be simple. Similar to a Trello, every item will show only a piece of text. We will do this with props: `props.item.content`.

We will create the board item as `BoardItem` component, using `styled-components`. In order to make the drag & drop work, we need to wrap this component inside `Draggable` component, imported from `react-beautiful-dnd`. This component needs two props: `draggableId` and `index`. The value of `draggableId` will be `props.item.id`. Value of `index` will be `props.index`.

We are not done yet. There are additional props we need to add to `BoardItem` component. `react-beautiful-dnd` requires `{...provided.draggableProps}`, `{...provided.dragHandleProps}` and `ref`. The value of `ref` will be `provided.innerRef`. This will make all board items draggable. The last prop we will add to `BoardItem` component is `isDragging`.

We will use this prop to change the item styles during dragging, with `styled-components`. To detect dragging we will use `snapshot` object and its `isDragging` property, provided by `react-beautiful-dnd`. The value of `isDragging` is boolean, `true` during dragging and `false` in a default state.

One important thing. TypeScript will not accept `isDragging` prop. This means that we have to define type aliases for this prop, as `BoardItemStylesProps`, right after we define types aliases for `BoardItem`, as `BoardItemProps`.

```
///
// src/components/board-item.tsx
///
import * as React from 'react'
import { Draggable } from 'react-beautiful-dnd'
import styled from 'styled-components'

// Define types for board item element properties
type BoardItemProps = {
  index: number
  item: any
}

// Define types for board item element style properties
// This is necessary for TypeScript to accept the 'isDragging' prop.
type BoardItemStylesProps = {
  isDragging: boolean
}

// Create style for board item element
const BoardItemEl = styled.div<BoardItemStylesProps>`
  padding: 8px;
  background-color: ${(props) => props.isDragging ? '#d3e4ee' : '#fff'};
  border-radius: 4px;
  transition: background-color .25s ease-out;

  &:hover {
    background-color: #f7fafc;
  }

  & + & {
    margin-top: 4px;
  }
`

// Create and export the BoardItem component
export const BoardItem = (props: BoardItemProps) => {
  return <Draggable draggableId={props.item.id} index={props.index}>
    {(provided, snapshot) => (
      {/* The BoardItem */}
      <BoardItemEl
        {...provided.draggableProps}
        {...provided.dragHandleProps}
        ref={provided.innerRef}
        isDragging={snapshot.isDragging}
      >
        {/* The content of the BoardItem */}
        {props.item.content}
      </BoardItemEl>
    )}
  </Draggable>
}
```

## Creating the board column

The second component we will create will be component for board column, or card if you want. The process will be very similar to one we used to create the board item. We will again start with type aliases for TypeScript. Similar to board item, we will change the style of the board when the item is dragged over it. Meaning, when the column is active and we can drop the item on it.

This will also require creating type alias, now for `isDraggingOver` prop. When we have this, we can use this prop to change the background color of active board column. The column will contain three components, all created with `styled-components`. These are `BoardColumnTitle` and `BoardColumnContent` wrapped inside `BoardColumnWrapper`.

The `BoardColumnTitle` will contain the title of the column. The `BoardColumnContent` will contain all board items belong into that specific column. We will use `map()` to iterate over `items` props to get them. Make sure to import the `BoardItem`. Lastly, to make the dag & drop working, we need to wrap the `BoardColumnContent` in `Droppable` component.

We will import this component from `react-beautiful-dnd` library. This component requires one prop: `droppableId`. This value for this prop will be id of each column. We can get the id from props: `props.column.id`. Similar to board item, we also need to add some props to `BoardColumnContent` to make it "droppable".

These props are `{...provided.droppableProps}` and `ref`. The value of `ref` will be `provided.innerRef`. In order to alter column styles we will add `isDraggingOver` prop and use it to change the background of drop area when it is active. Otherwise, we may not know where to drop the board item.

Like in case of a board item, we will use `snapshot` object provided by `react-beautiful-dnd`. Now, however, we will use its `isDraggingOver` property. The value of `isDraggingOver` property is also a boolean, `true` when the item is above the drop area and `false` if not, when it is in the default state.

```
///
// src/components/board-column.tsx
///
import * as React from 'react'
import { Droppable } from 'react-beautiful-dnd'
import styled from 'styled-components'

// Import BoardItem component
import { BoardItem } from './board-item'

// Define types for board column element properties
type BoardColumnProps = {
  key: string,
  column: any,
  items: any,
}

// Define types for board column content style properties
// This is necessary for TypeScript to accept the 'isDraggingOver' prop.
type BoardColumnContentStylesProps = {
  isDraggingOver: boolean
}

// Create styles for BoardColumnWrapper element
const BoardColumnWrapper = styled.div`
  flex: 1;
  padding: 8px;
  background-color: #e5eff5;
  border-radius: 4px;

  & + & {
    margin-left: 12px;
  }
`

// Create styles for BoardColumnTitle element
const BoardColumnTitle = styled.h2`
  font: 14px sans-serif;
  margin-bottom: 12px;
`

// Create styles for BoardColumnContent element
const BoardColumnContent = styled.div<BoardColumnContentStylesProps>`
  min-height: 20px;
  background-color: ${props => props.isDraggingOver ? '#aecde0' : null};
  border-radius: 4px;
`

// Create and export the BoardColumn component
export const BoardColumn: React.FC<BoardColumnProps> = (props) => {
  return(
    <BoardColumnWrapper>
      {/* Title of the column */}
      <BoardColumnTitle>
        {props.column.title}
      </BoardColumnTitle>

      <Droppable droppableId={props.column.id}>
        {(provided, snapshot) => (
          {/* Content of the column */}
          <BoardColumnContent
            {...provided.droppableProps}
            ref={provided.innerRef}
            isDraggingOver={snapshot.isDraggingOver}
          >
            {/* All board items belong into specific column. */}
            {props.items.map((item: any, index: number) => <BoardItem key={item.id} item={item} index={index} />)}
            {provided.placeholder}
          </BoardColumnContent>
        )}
      </Droppable>
    </BoardColumnWrapper>
  )
}
```

## Creating the board

When we have the components for board item and column, it is time for the hardest part. The board component will contain the logic for drag & drop functionality. It will also load the board data and use it to generate columns. This means we need to import `board-initial-data.ts` and also `BoardColumn` component.

Next, let's use `styled-components` to create styles for the board. The result will be `BoardEl` component we will use as the wrapper element for the board. After that, let's create new React component called `Board`, as a class. We will initialize the state of this class with the `initialBoardData`, or the content of `board-initial-data.ts`.

Now, it is time to create the logic for drag & drop. Let's create method called `onDragEnd`. This method will check if the dragged item is dropped outside the list. Then, it will check if the dragged item is dropped into the same place. If any of these conditions is true, we don't want to do anything. Adding `return` to stop execution will do the job.

Next, we need to handle situation when the item is dropped into a different place, but in the same column. First, we need to find column from which the item was dragged from. Then, we need to find column in which the item was dropped. If these two are the same, we know that the item was dropped into different place, but in the same column.

First, we need to get all item ids in currently active list. Next, we must remove the id of dragged item from its original position. Next, we must insert the id of dragged item to the new position. Now, we need to create new, updated, object with data for columns and items. After that, can create new board state with updated data for columns and items. When this is done we can finally update the board state with new data.

The second scenario is when item is dragged from one list to another. In that case, we again need to get all item ids in the source list and remove the id of dragged item from its original position. Next, we can again create new, updated, object with data for source column. After that, we need data from the destination list, where we dropped item.

We can follow process similar to the previous. First, we need to get all item ids in destination list. Next, we must insert the id of dragged item to the new position in the destination list. Then, we can again create new, updated, object with data, now for the destination column. Then comes creating new board state with updated data for both, source and destination.

As the last step, we can update the board state with new data. The result of all this is that we can change the order of items in a column dragging them from one place to another. And, we can also take item from list and move it to another. Now, the very last step, rendering all columns in the board. This will be relatively easy.

First, we need to import `DragDropContext` component from `react-beautiful-dnd`. Next, in the `render` method of `Board` class, we will use the `BoardEl` component we created with `styled-components` and we will put the `DragDropContext` inside it. This will create the context for drag & drop, provide draggable and droppable components with necessary data.

Inside the `DragDropContext` we will use `map()` to iterate over the `columnsOrder` array in `board-initial-data.ts`. This will give us the order in which we want to render the columns. Next, for each column, we need to get the id of the column and also the items belonging to that column. Having all this data, we can render the `BoardColumn` component into the board.

```
///
// src/components/board.tsx
///
import * as React from 'react'
import { DragDropContext } from 'react-beautiful-dnd'
import styled from 'styled-components'

// Import data for board
import { initialBoardData } from '../data/board-initial-data'

// Import BoardColumn component
import { BoardColumn } from './board-column'

// Create styles board element properties
const BoardEl = styled.div`
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
`

export class Board extends React.Component {
  // Initialize board state with board data
  state = initialBoardData

  // Handle drag & drop
  onDragEnd = (result: any) => {
    const { source, destination, draggableId } = result

    // Do nothing if item is dropped outside the list
    if (!destination) {
      return
    }

    // Do nothing if the item is dropped into the same place
    if (destination.droppableId === source.droppableId && destination.index === source.index) {
      return
    }

    // Find column from which the item was dragged from
    const columnStart = (this.state.columns as any)[source.droppableId]

    // Find column in which the item was dropped
    const columnFinish = (this.state.columns as any)[destination.droppableId]

    // Moving items in the same list
    if (columnStart === columnFinish) {
      // Get all item ids in currently active list
      const newItemsIds = Array.from(columnStart.itemsIds)

      // Remove the id of dragged item from its original position
      newItemsIds.splice(source.index, 1)

      // Insert the id of dragged item to the new position
      newItemsIds.splice(destination.index, 0, draggableId)

      // Create new, updated, object with data for columns
      const newColumnStart = {
        ...columnStart,
        itemsIds: newItemsIds
      }

      // Create new board state with updated data for columns
      const newState = {
        ...this.state,
        columns: {
          ...this.state.columns,
          [newColumnStart.id]: newColumnStart
        }
      }

      // Update the board state with new data
      this.setState(newState)
    } else {
      // Moving items from one list to another
      // Get all item ids in source list
      const newStartItemsIds = Array.from(columnStart.itemsIds)

      // Remove the id of dragged item from its original position
      newStartItemsIds.splice(source.index, 1)

      // Create new, updated, object with data for source column
      const newColumnStart = {
        ...columnStart,
        itemsIds: newStartItemsIds
      }

      // Get all item ids in destination list
      const newFinishItemsIds = Array.from(columnFinish.itemsIds)

      // Insert the id of dragged item to the new position in destination list
      newFinishItemsIds.splice(destination.index, 0, draggableId)

      // Create new, updated, object with data for destination column
      const newColumnFinish = {
        ...columnFinish,
        itemsIds: newFinishItemsIds
      }

      // Create new board state with updated data for both, source and destination columns
      const newState = {
        ...this.state,
        columns: {
          ...this.state.columns,
          [newColumnStart.id]: newColumnStart,
          [newColumnFinish.id]: newColumnFinish
        }
      }

      // Update the board state with new data
      this.setState(newState)
    }
  }

  render() {
    return(
      <BoardEl>
        {/* Create context for drag & drop */}
        <DragDropContext onDragEnd={this.onDragEnd}>
          {/* Get all columns in the order specified in 'board-initial-data.ts' */}
          {this.state.columnsOrder.map(columnId => {
            // Get id of the current column
            const column = (this.state.columns as any)[columnId]

            // Get item belonging to the current column
            const items = column.itemsIds.map((itemId: string) => (this.state.items as any)[itemId])

            // Render the BoardColumn component
            return <BoardColumn key={column.id} column={column} items={items} />
          })}
        </DragDropContext>
      </BoardEl>
    )
  }
}
```

## Building the page component

This is the last step. Now, we will create `Page` component. This component will contain the `Board` component we just finished. Before we render the `Page` component in DOM, we can make it a bit prettier with `style-component`. Let's use `createGlobalStyle` helper imported from `styled-components` library.

This helper allows us to define global styles. Those global styles are not limited to specific local CSS class. Put simply, we can use `createGlobalStyle` to define styles for elements such as `html` and `body`. So, if you want to add some CSS resets or base styles you want to apply everywhere, `createGlobalStyle` is what you are looking for.

For now we can keep it simple and just change the background of the `body` element. This will help us make the board columns stand out.

```
///
// src/index.tsx
///
import * as React from 'react'
import * as ReactDOM from 'react-dom'
import { createGlobalStyle } from 'styled-components'

// Import main Board component
import { Board } from './components/board'

// Use createGlobalStyle to change the background of 'body' element
const GlobalStyle = createGlobalStyle`
  body {
    background-color: #4bcffa;
  }
`

// Create component for the page
const Page = () => (<>
  {/* Add main Board component */}
  <Board />

  {/* Add GlobalStyle */}
  <GlobalStyle />
</>)

// Render the page into DOM
ReactDOM.render(<Page />, document.getElementById('root'))
```

## Epilogue: How to build Trello board with React, TypeScript & styled-components

Congratulations! You've just finished this tutorial and created your own drag & drop Trello-like board! Good job! I hope you enjoyed this tutorial. I also hope you have a chance to learn something new, or at least practice what you already know. Where to go next? You can learn more about the things you've worked with today.

You can start with [styled-components website]. Here, you can learn how to make your board look better. Or, you can take a look at what else can you do with [react-beautiful-dnd]. If you are new to TypeScript, and you like it, take a look at its [website]. By the way, if you never used TypeScript before, I highly recommend giving it a try.

TypeScript can help you take your code to a whole new level. The same also applies to your productivity. Writing cleaner, safer and more maintainable code is almost automatic with TypeScript. TypeScript is a game changer. Give it a try and you will never want to write anything in plain JavaScript again. And, with that, thank you for time your time.

[xyz-ihs snippet="thank-you-message"]

<!-- ### Links -->
[npx]: https://github.com/zkat/npx
[TypeScript]: https://www.typescriptlang.org
[styled-components website]: https://www.styled-components.com
[react-beautiful-dnd]: https://github.com/atlassian/react-beautiful-dnd
[website]: https://www.typescriptlang.org/

<!--
#### Meta:
-
-->

<!--
#### Inspiration:
-
-->