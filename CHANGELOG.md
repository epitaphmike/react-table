## 6.3.0
##### New Features
- `defaultSortDesc` - allows you to set the default sorting direction for all columns to descending.
- `column.defaultSortDesc` - allows you to set the default sorting direction for a specific column. Falls back to the global `defaultSortDesc` when not set at all.

## 6.0.0

##### New Features
- New Renderers:
  - `Aggregated` - Custom renderer for aggregated cells
  - `Pivot` - Custom renderer for Pivoted Cells (utilizes `Expander` and `PivotValue`)
  - `PivotValue` - Custom renderer for Pivot cell values (deprecates the undocumented `pivotRender` option)
  - `Expander` - Custom renderer for Pivot cell Expander
- Added custom sorting methods per table via `defaultSortMethod` and per column via `column.sortMethod`
- Pivot columns are now visibly separate and sorted/filtered independently.
- Added `column.resizable` to override global table `resizable` option for specific columns.
- Added `column.sortable` to override global table `sortable` option for specific columns.
- Added `column.filterable` to override global table `filterable` option for specific columns.
- Added `defaultExpanded` table option.
- All callbacks can now be utilized without needing to hoist and manage the piece of state they export. That is what their prop counterparts are for, so now the corresponding prop is used instead of the callback to detect a "fully controlled" state.
- Prevent transitions while column resizing for a smoother resize effect.
- Disable text selection while resizing columns.


##### Breaking API Changes
- New Renderers:
  - `Cell` - deprecates and replaces `render`
  - `Header` - deprecates and replaces `header`
  - `Footer` - deprecates and replaces `footer`
  - `Filter`- deprecates and replaces `filterRender`
- Callbacks now provide the destination state as the primary parameter(s). This makes hoisting and controlling the state in redux or component state much easier. eg.
  - `onSorting` no longer requires you to build your own toggle logic
  - `onResize` no longer requires you to build your own resize logic
- Renamed `onChange` callback -> `onFetchData` which will always fire when a new data model needs to be fetched (or if not using `manual`, when new data is materialized internally).
- Renamed `filtering` -> `filtered`
- Renamed `sorting` -> `sorted`
- Renamed `expandedRows` -> `expanded`
- Renamed `resizing` -> `resized`
- Renamed `defaultResizing` -> `defaultResized`
- Renamed `defaultFiltering` -> `defaultFiltered`
- Renamed `defaultSorting` -> `defaultSorted`
- Renamed `onSortingChange` -> `onSortedChange`
- Renamed `onFilteringChange` -> `onFilteredChange`
- Renamed `onResize` -> `onResizedChange`
- Renamed `onExpandRow` -> `onExpandedChange`
- Renamed `showFilters` -> `filterable`
- Renamed `hideFilter` -> `filterable` (Column option. Note the true/false value is now flipped.)
- `cellInfo.row` and `rowInfo.row` now reference the materialize data for the table. To reference the original row, use `cellInfo.original` and `rowInfo.original`
- Removed `pivotRender` column option. You can now control how the value is displayed by overriding the `PivotValueComponent` or the individual column's `PivotValue` renderer. See [Pivoting Options Story](https://react-table.js.org/?selectedKind=2.%20Demos&selectedStory=Pivoting%20Options&full=0&down=1&left=1&panelRight=0&downPanel=kadirahq%2Fstorybook-addon-actions%2Factions-panel) for a reference on how to customize pivot column rendering.
