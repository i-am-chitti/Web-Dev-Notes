# REACT JS Version Upgrades

## React v18.0

### Key Features

#### Concurrent React

Before concurrent react, rendering is a single, uninterrupted and synchronous transaction. Once rendering starts, nothing can interrupt it until user can see the result on screen.

In concurrent react, that is not always the case. React may start rendering an update, pause in the middle, then continue later. It may even abandon an in-progress render altogether. React guarantees that the UI will appear consistent even if a render is interrupted.
