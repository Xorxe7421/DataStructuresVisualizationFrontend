# Data Structures Visualization — Frontend

An interactive React web app for creating, operating on, and visually exploring data structures step by step. Users can create named instances of 11 data structure types across multiple implementations, execute operations, and watch animated memory snapshots of each step rendered in D3 SVG. Supports PDF export of operation snapshots, zoom/pan, and JWT-authenticated sessions.

> **This is the frontend half of a full-stack project.** The backend provides the REST API that executes operations and returns memory snapshots. See the backend repository for the server-side implementation.

---

## Features

- **11 data structure types** — Vector, Stack, Queue, Map, Set, Tree, Editor Buffer, Grid, Deque, Web Browser, Big Integer
- **Multiple implementations per type** — e.g. Stack can be Array, Linked List, or Two-Queue; Queue supports Array, Linked List, and four Priority Queue variants
- **Step-by-step snapshot playback** — each operation returns multiple intermediate memory snapshots; navigate forward/backward or auto-play at configurable speed
- **7 D3-powered visualizations** — dedicated renderers for arrays, singly linked lists, doubly linked lists, hash structures, binary search trees, grids, and the two-stack editor buffer
- **Big-O annotations** — every operation shows its time complexity for the selected implementation inline in the UI
- **Operation history** — full log of all operations performed on a data structure, clickable to replay any past state
- **PDF export** — exports all snapshots of the current operation to a multi-page PDF via html2canvas + jsPDF, with a progress indicator
- **Zoom & pan** — D3 zoom on the SVG canvas with zoom-in, zoom-out, and auto-fit controls
- **JWT authentication** — login/register flow with token stored in localStorage; protected routes redirect unauthenticated users
- **Responsive layout** — Tailwind CSS, works on desktop and tablet

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | React 19 |
| Routing | React Router v7 |
| Visualization | D3.js v7 |
| HTTP | Axios |
| Styling | Tailwind CSS |
| PDF Export | jsPDF + html2canvas |
| Icons | Lucide React |
| Build | Create React App |

---

## Getting Started

### Prerequisites

- Node.js 18+
- The backend server running (see backend README)

### Installation

```bash
git clone https://github.com/Xorxe7421/DataStructuresVisualizationFrontend
cd DataStructuresVisualizationFrontend
npm install
```

### Configuration

Create or edit `.env`:

```env
REACT_APP_API_URL=http://localhost:8080
```

### Run

```bash
npm start
```

The app opens at `http://localhost:3000`.

---

## Usage

### Creating a data structure

1. Log in or register
2. On the home page, click **Create New**
3. Choose a name, type, and implementation
4. For Grid: also specify rows and columns
5. For Big Integer: specify the initial value
6. Click **Create** — you're taken directly to the visualization page

### Operating on a data structure

On the data structure page, the left panel shows all available operations with inline argument inputs and Big-O annotations. Click **Perform** to execute. The visualization updates immediately.

### Navigating snapshots

Each operation produces multiple intermediate memory snapshots showing the state of variables and heap objects at each step. Use the snapshot navigation controls at the bottom of the visualization panel:

- `⏮` — jump to first snapshot
- `◀` — previous snapshot
- `▶ / ⏸` — auto-play / pause
- `▶` — next snapshot
- `⏭` — jump to last snapshot
- Speed selector — Slow / Normal / Fast

### Exporting to PDF

Click the download icon (↓) in the visualization header to export all snapshots of the current operation as a PDF. Each page shows a snapshot image and its result value if applicable.

---

## Data Structures & Operations

| Type | Implementations | Operations |
|---|---|---|
| Vector | Array, Linked List | add, get, set, insertAt, removeAt, size, isEmpty, clear |
| Stack | Array, Linked List, Two-Queue | push, pop, peek, size, isEmpty, clear |
| Queue | Array, Linked List, Unsorted Vector Priority, Sorted Linked List Priority, Unsorted Doubly Linked List Priority, Binary Heap Priority | enqueue, dequeue, peek, size, isEmpty, clear |
| Map | Array, Hash | put, get, containsKey, size, isEmpty, clear |
| Set | Hash, Move-To-Front | add, remove, contains, size, isEmpty, clear |
| Tree | Binary Search | insert, remove, search, clear |
| Editor Buffer | Array, Two-Stack, Linked List, Doubly Linked List | insertCharacter, deleteCharacter, moveCursorForward, moveCursorBackward, moveCursorToStart, moveCursorToEnd |
| Grid | Grid | set, get, numRows, numColumns, inBounds |
| Deque | Deque | pushFront, pushBack, popFront, popBack, getFront, getBack, size, isEmpty, clear |
| Web Browser | (Doubly Linked List) | visit, forward, back |
| Big Integer | Big Integer | add, isGreaterThan |

---

## Visualization Renderers

Each data structure type is rendered by a dedicated D3 module:

- **ArrayStructureVisualization** — renders the instance/local variable boxes and the backing array, with address boxes linking variables to array cells. Handles both primitive and object-valued cells.
- **LinkedStructureVisualization** — traverses the linked list from the head pointer, renders nodes in a horizontal chain, and draws "next" pointer arrows. Isolated (orphan) nodes rendered in a separate grid zone.
- **DoublyLinkedStructure** — extends linked structure rendering with both `next` (blue) and `prev` (red) arrows. Used for Deque and Web Browser.
- **HashStructureVisualization** — renders the bucket array on the left and chains of nodes extending to the right, with arrows from bucket cells to chain heads.
- **TreeVisualization** — recursive BST layout with adaptive horizontal/vertical spacing based on tree depth. Renders left/right child pointer arrows from the appropriate field rows.
- **GridStructureVisualization** — renders a 2D grid of cells with row address pointers, showing the full row-of-arrays structure.
- **TwoStackEditorBufferVisualization** — renders the left and right stacks side by side with a cursor indicator between them.

All renderers share a library of utilities (`visualizationUtils.js`) for arrowhead definitions, variable box rendering, node rendering, and orthogonal path generation with rounded corners.

---

## Project Structure

```
src/
├── App.js                          # Router setup, ProtectedRoute
├── context/
│   └── AuthContext.js              # JWT auth state, login/register/logout
├── services/
│   └── api.js                      # Axios instance + dataStructureService
├── components/
│   └── Navbar.js                   # Top nav with auth-aware links
├── pages/
│   ├── LoginPage.js
│   ├── RegisterPage.js
│   ├── HomePage.js                 # Data structure list + create modal
│   └── DataStructurePage.js        # Main visualization page
├── utils/
│   └── visualizationUtils.js       # Shared D3 rendering utilities
└── visualizations/
    ├── ArrayStructureVisualization.js
    ├── LinkedStructureVisualization.js
    ├── DoublyLinkedStructure.js
    ├── HashStructureVisualization.js
    ├── TreeVisualization.js
    ├── GridStructureVisualization.js
    └── TwoStackEditorBufferVisualization.js
```

---

## Author

**Giorgi Pavliashvili**  
Backend Java Developer  
[LinkedIn](https://www.linkedin.com/in/giorgi-pavliashvili-6718861b6/) · [GitHub](https://github.com/Xorxe7421)
